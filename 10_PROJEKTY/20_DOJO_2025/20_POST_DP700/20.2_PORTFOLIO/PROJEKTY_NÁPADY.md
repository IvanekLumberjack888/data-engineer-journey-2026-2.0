# Case Study: Data Platform pro Pronajímání Nářadí + Servis

## Kontext: HobbyTools CZ

Anonymizovaná společnost "HobbyTools CZ" - pronajímá profesionální nářadí a vybavení pro domácnosti a staveniště.

**Produk:** Vrtačky, pily, brusky, stroje na vysokotlakové čištění (Kärcher style), zahradní vybavení, průmyslové čističe.

**Byznys model:**
- Pronajímání nářadí (4h, 24h, týdenní, měsíční sazby)
- Servis a opravy pronajímaného vybavení (záruční, bez záruk, pojistné)
- Prodej doplňků a náhradních dílů
- Čištění a údržba nářadí po vrácení

**Problémy:**
- Data jsou rozptýlená (Excel, SharePoint, papírové formuláře)
- Neznámá ziskovost pronajímek (vs náklady na servis)
- Nemohou predikovat, které stroje se Often porouchají
- Neznají, kolik lidí v obchodě se věnuje servisům vs pronajímání
- Nemohou vidět korelace: počet rentálů vs počet zaměstnanců

---

## Zdroje dat

```
Ingestion Layer (Dataflow Gen2)
├── SharePoint Lists
│   ├── tools_inventory (vrt, pila, brušt...)
│   └── rental_customers (kontakty, historie)
├── Excel files (CloudStorage)
│   ├── weekly_rentals (pronajímky minulý týden)
│   ├── repairs_log (servis zápisy)
│   └── replacement_parts_sales (prodej dílů)
├── API
│   ├── HR system (zaměstnanci, dovolenou, přesčasy)
│   ├── Invoicing system (faktury, platby, DPH)
│   └── Customer feedback API (recenze pronajímek)
├── SQL Database (legacy system)
│   ├── tools_maintenance_history
│   ├── rental_transactions
│   └── customer_complaints
└── IoT Sensors (Kärcher-style equipment)
    ├── Usage hours counter (v nářadí)
    ├── Error codes (když se něco pokazí)
    └── GPS location (kde je nástroj pronajat - staveniště)
```

---

## Architektura: Fabric + Python

```
┌──────────────────────────────────────────┐
│    INGESTION (Dataflow Gen2 - bez kódu)  │
├──────────────────────────────────────────┤
│ SharePoint → rental_customers            │
│ Excel → weekly_rentals, repairs_log      │
│ HR API → staff_daily                     │
│ Invoicing API → invoices, payments       │
│ IoT Sensors → tools_telemetry            │
│ Legacy SQL → tool_maintenance_history    │
└──────────────────────────────────────────┘
                  ↓
┌──────────────────────────────────────────┐
│    BRONZE LAYER (Lakehouse - raw)        │
├──────────────────────────────────────────┤
│ bronze_rentals                           │
│ bronze_tools                             │
│ bronze_repairs                           │
│ bronze_staff                             │
│ bronze_invoices                          │
│ bronze_tools_telemetry                   │
│ bronze_replacement_parts_sales           │
└──────────────────────────────────────────┘
                  ↓
┌──────────────────────────────────────────┐
│ SILVER LAYER (Cleaned & Typed)           │
├──────────────────────────────────────────┤
│ silver_rentals (pronajímky + náklady)    │
│ silver_tools (inventář + stav)           │
│ silver_repairs (servis + náklady)        │
│ silver_staff_daily (zaměstnanci)         │
│ silver_maintenance_timeline              │
│ silver_rental_costs (komplexní)          │
└──────────────────────────────────────────┘
                  ↓
┌──────────────────────────────────────────┐
│ GOLD LAYER (KPI & Analytics)             │
├──────────────────────────────────────────┤
│ gold_rental_profitability                │
│ gold_tool_performance (který se často    │
│     porouchá, jaké jsou náklady)         │
│ gold_revenue_by_category                 │
│ gold_staff_productivity                  │
│ gold_maintenance_forecast                │
│ gold_customer_lifetime_value              │
└──────────────────────────────────────────┘
                  ↓
┌──────────────────────────────────────────┐
│    POWER BI DASHBOARDS                   │
├──────────────────────────────────────────┤
│ • Rental Performance                     │
│ • Tool Health & Maintenance              │
│ • Staff Productivity                     │
│ • Revenue vs Costs                       │
│ • Anomaly Detection                      │
└──────────────────────────────────────────┘
```

---

## Krok 1: Ingestion – Dataflow Gen2 (bez kódu)

### 1.1 SharePoint List → Tools Inventory

```
List: "Inventář nářadí"

Columns:
├── tool_id (Kärcher_K5_001)
├── tool_category (pressure_washer, drill, grinder...)
├── tool_name (Kärcher K5 Standard)
├── purchase_date
├── purchase_price_czk
├── current_value_czk (amortizace)
├── location (Praha, Brno, Ostrava...)
├── status (available, rented, maintenance, sold)
└── maintenance_contract (yes/no)
```

**Dataflow akce:** Filtr status != "sold", ulož do `bronze_tools`

### 1.2 Excel → Rentals

```
File: weekly_rentals.xlsx (nahrávají pondělí)

Columns:
├── rental_id
├── tool_id
├── customer_id
├── rental_date
├── return_date
├── daily_rate_czk
├── damage_reported (true/false)
├── damage_cost_czk
└── customer_rating (1-5)
```

**Dataflow akce:** UTC timestamps, vyčisti nuly, ulož do `bronze_rentals`

### 1.3 Excel → Repairs Log

```
File: repairs_log.xlsx

Columns:
├── repair_id
├── tool_id
├── rental_id (pokud to byla pronajatá věc)
├── repair_date
├── failure_type (motor_failure, seal_leak, power_issue...)
├── repair_cost_czk
├── repair_hours
├── replacement_parts_cost_czk
├── repair_status (in_progress, completed, warranty)
└── warranty_claim (true/false)
```

**Dataflow akce:** Uprav datumy, ulož do `bronze_repairs`

### 1.4 HR API → Staff Daily

```
API: https://hr-system.hobbytools.local/api/staff/

Response per employee per day:
{
  "employee_id": "EMP001",
  "date": "2025-12-03",
  "location": "Praha",
  "department": "rental|service|sales",
  "time_in": "08:00",
  "time_out": "17:00",
  "overtime_hours": 1.5,
  "is_vacation": false,
  "is_sick_leave": false,
  "tasks": ["customer_service", "maintenance", "cleaning"]
}
```

**Dataflow akce:** Parseuj JSON, ulož do `bronze_staff`

### 1.5 Invoicing API → Faktury

```
API: https://invoicing.hobbytools.local/api/invoices/

Response:
{
  "invoice_id": "INV-2025-001",
  "rental_id": "RENT-5443",
  "amount_czk": 1200.00,
  "paid_amount_czk": 1200.00,
  "invoice_date": "2025-12-01",
  "payment_date": "2025-12-05",
  "days_overdue": 0,
  "vat_rate": 0.21
}
```

**Dataflow akce:** Vyčisti NULLy, přetypuj, ulož do `bronze_invoices`

### 1.6 IoT Sensors (Kärcher, Metabo, Bosch equipment)

```
Device telemetry (MQTT / HTTP):

{
  "device_id": "Karcher_K5_001",
  "timestamp": "2025-12-03T14:30:00Z",
  "usage_hours_total": 2456.5,
  "last_maintenance": "2025-11-15",
  "maintenance_due_days": 45,
  "error_code": null,
  "power_cycles": 15,
  "operating_temperature": 42.5,
  "filter_status": "good|warning|critical",
  "gps_location": {"lat": 50.0755, "lng": 14.4378},
  "last_used_date": "2025-12-03",
  "battery_percentage": 95
}
```

**Dataflow akce:**
- Ulož raw do `bronze_tools_telemetry`
- Agreguj denně: 1 řádka per tool per day
- Kalkuluj: `days_since_maintenance`, `is_maintenance_due`

---

## Krok 2: Silver Layer – Python Notebook

**Notebook:** `lh_tool_silver_clean.py`

### 2.1 Silver Rentals (pronajímky + náklady)

```python
from pyspark.sql import functions as F
from datetime import datetime

# LOAD
rentals_raw = spark.read.table("Lab01_Lakehouse.dbo.bronze_rentals")
tools_raw = spark.read.table("Lab01_Lakehouse.dbo.bronze_tools")
repairs_raw = spark.read.table("Lab01_Lakehouse.dbo.bronze_repairs")
invoices_raw = spark.read.table("Lab01_Lakehouse.dbo.bronze_invoices")

# CLEAN RENTALS
rentals_clean = (
    rentals_raw
    .filter("rental_id IS NOT NULL")
    .filter("tool_id IS NOT NULL")
    .withColumn("rental_duration_days", 
        F.datediff(F.col("return_date"), F.col("rental_date")))
    .filter("rental_duration_days >= 0")  # no bad dates
    .withColumn("daily_rate_czk", 
        F.regexp_replace("daily_rate_czk", ",", ".").cast("decimal(10,2)"))
    .withColumn("damage_cost_czk",
        F.coalesce(F.col("damage_cost_czk"), F.lit(0)).cast("decimal(10,2)"))
    .dropDuplicates(["rental_id"])
)

# JOIN WITH TOOLS
rentals_with_tools = (
    rentals_clean
    .join(tools_raw, "tool_id", "left")
    .select(
        rentals_clean.rental_id,
        rentals_clean.tool_id,
        tools_raw.tool_category,
        tools_raw.tool_name,
        tools_raw.location,
        rentals_clean.customer_id,
        rentals_clean.rental_date,
        rentals_clean.return_date,
        rentals_clean.rental_duration_days,
        rentals_clean.daily_rate_czk,
        rentals_clean.damage_reported,
        rentals_clean.damage_cost_czk,
        rentals_clean.customer_rating
    )
)

# CALCULATE RENTAL REVENUE
rentals_with_revenue = (
    rentals_with_tools
    .withColumn("rental_revenue_czk",
        F.col("daily_rate_czk") * F.col("rental_duration_days"))
)

# JOIN WITH REPAIRS (náklady na servis po vrácení)
repairs_cost_per_rental = (
    repairs_raw
    .filter("rental_id IS NOT NULL")
    .groupBy("rental_id")
    .agg(
        F.sum("repair_cost_czk").alias("total_repair_cost_czk"),
        F.sum("replacement_parts_cost_czk").alias("parts_cost_czk"),
        F.count("repair_id").alias("repair_count"),
        F.sum(F.when(F.col("warranty_claim") == True, 1).otherwise(0))
            .alias("warranty_repairs_count")
    )
)

rentals_final = (
    rentals_with_revenue
    .join(repairs_cost_per_rental, "rental_id", "left")
    .fillna(0, ["total_repair_cost_czk", "parts_cost_czk", "repair_count"])
    .withColumn("total_cost_czk",
        F.col("damage_cost_czk") + 
        F.col("total_repair_cost_czk") + 
        F.col("parts_cost_czk"))
    .withColumn("net_profit_czk",
        F.col("rental_revenue_czk") - F.col("total_cost_czk"))
    .withColumn("profit_margin_pct",
        (F.col("net_profit_czk") / F.greatest(F.col("rental_revenue_czk"), F.lit(1)) * 100))
)

# ULOŽ
rentals_final.write.format("delta") \
    .mode("overwrite") \
    .saveAsTable("silver_rentals")

print(f"✓ silver_rentals: {rentals_final.count()} řádků")
```

### 2.2 Silver Tools Health (stav nářadí)

```python
# LOAD TELEMETRY
telemetry_raw = spark.read.table("Lab01_Lakehouse.dbo.bronze_tools_telemetry")
tools_raw = spark.read.table("Lab01_Lakehouse.dbo.bronze_tools")

# CLEAN & AGGREGATE (nejnovější stav per tool)
tools_latest_telemetry = (
    telemetry_raw
    .withColumn("date", F.to_date("timestamp"))
    .groupBy("device_id", "date")
    .agg(
        F.first("usage_hours_total").alias("total_usage_hours"),
        F.first("maintenance_due_days").alias("days_until_maintenance"),
        F.first("filter_status").alias("filter_status"),
        F.first("operating_temperature").alias("last_temp_celsius"),
        F.first("power_cycles").alias("power_cycles"),
        F.first("last_maintenance").alias("last_maintenance_date"),
        F.first("error_code").alias("error_code")
    )
)

# FLAGS: Is maintenance due?
tools_health = (
    tools_latest_telemetry
    .withColumn("maintenance_overdue", F.col("days_until_maintenance") <= 0)
    .withColumn("has_error", F.col("error_code").isNotNull())
    .withColumn("filter_critical", F.col("filter_status") == "critical")
)

# JOIN WITH TOOLS MASTER
tools_health_full = (
    tools_health
    .join(tools_raw, F.col("device_id") == F.col("tool_id"), "left")
    .select(
        "date",
        "device_id",
        "tool_category",
        "tool_name",
        "location",
        "total_usage_hours",
        "days_until_maintenance",
        "maintenance_overdue",
        "has_error",
        "filter_status",
        "last_temp_celsius",
        "power_cycles"
    )
)

tools_health_full.write.format("delta") \
    .mode("overwrite") \
    .saveAsTable("silver_tools_health")

print(f"✓ silver_tools_health")
```

### 2.3 Silver Repairs Analysis

```python
repairs_raw = spark.read.table("Lab01_Lakehouse.dbo.bronze_repairs")

repairs_clean = (
    repairs_raw
    .filter("repair_id IS NOT NULL")
    .withColumn("repair_date_clean", F.to_date("repair_date"))
    .withColumn("repair_cost_czk", F.col("repair_cost_czk").cast("decimal(10,2)"))
    .withColumn("repair_hours", F.col("repair_hours").cast("decimal(5,2)"))
    .withColumn("total_repair_cost_czk",
        F.col("repair_cost_czk") + F.coalesce(F.col("replacement_parts_cost_czk"), F.lit(0)))
    .dropDuplicates(["repair_id"])
)

repairs_clean.write.format("delta") \
    .mode("overwrite") \
    .saveAsTable("silver_repairs")

print(f"✓ silver_repairs")
```

### 2.4 Silver Staff Daily

```python
staff_raw = spark.read.table("Lab01_Lakehouse.dbo.bronze_staff")

staff_clean = (
    staff_raw
    .filter("employee_id IS NOT NULL")
    .withColumn("worked_hours",
        (F.unix_timestamp("time_out") - F.unix_timestamp("time_in")) / 3600)
    .filter("worked_hours >= 0 AND worked_hours <= 12")
    .dropDuplicates(["employee_id", "date"])
)

# DAILY SUMMARY per location
staff_daily_summary = (
    staff_clean
    .groupBy("date", "location")
    .agg(
        F.count_distinct("employee_id").alias("total_staff"),
        F.count_distinct(F.when(F.col("department") == "rental", "employee_id"))
            .alias("rental_staff"),
        F.count_distinct(F.when(F.col("department") == "service", "employee_id"))
            .alias("service_staff"),
        F.sum("overtime_hours").alias("total_overtime_hours"),
        F.sum(F.when(F.col("is_vacation"), 1).otherwise(0))
            .alias("on_vacation_count"),
        F.sum(F.when(F.col("is_sick_leave"), 1).otherwise(0))
            .alias("sick_leave_count")
    )
)

staff_daily_summary.write.format("delta") \
    .mode("overwrite") \
    .saveAsTable("silver_staff_daily")

print(f"✓ silver_staff_daily")
```

---

## Krok 3: Gold Layer – KPI & Analytics

**Notebook:** `lh_tool_gold_analytics.py`

### 3.1 Gold: Rentabilita pronajímek

```python
from pyspark.sql import functions as F

silver_rentals = spark.read.table("Lab01_Lakehouse.dbo.silver_rentals")

# PROFITABILITY ANALYSIS
gold_rental_profitability = (
    silver_rentals
    .select(
        "rental_id",
        "tool_id",
        "tool_category",
        "tool_name",
        "location",
        "rental_date",
        "return_date",
        "rental_duration_days",
        "rental_revenue_czk",
        "total_cost_czk",
        "damage_cost_czk",
        "total_repair_cost_czk",
        "parts_cost_czk",
        "net_profit_czk",
        "profit_margin_pct",
        "customer_rating",
        
        # RISK SCORING
        F.when(F.col("profit_margin_pct") < -50, "high_loss")
            .when(F.col("profit_margin_pct") < 0, "loss")
            .when(F.col("profit_margin_pct") < 20, "low_margin")
            .otherwise("healthy")
            .alias("profitability_status")
    )
)

gold_rental_profitability.write.format("delta") \
    .mode("overwrite") \
    .saveAsTable("gold_rental_profitability")

print(f"✓ gold_rental_profitability")
```

### 3.2 Gold: Výkon nářadí (které se často porouchá)

```python
silver_tools_health = spark.read.table("Lab01_Lakehouse.dbo.silver_tools_health")
silver_repairs = spark.read.table("Lab01_Lakehouse.dbo.silver_repairs")
silver_rentals = spark.read.table("Lab01_Lakehouse.dbo.silver_rentals")

# TOOL RELIABILITY SCORE
tool_reliability = (
    silver_rentals
    .groupBy("tool_id", "tool_category", "tool_name")
    .agg(
        F.count("rental_id").alias("total_rentals"),
        F.sum(F.when(F.col("damage_reported"), 1).otherwise(0))
            .alias("damaged_count"),
        F.avg("customer_rating").alias("avg_rating"),
        F.sum("total_repair_cost_czk").alias("total_repair_costs_czk"),
        F.sum("net_profit_czk").alias("total_profit_czk")
    )
    .withColumn("damage_rate_pct",
        (F.col("damaged_count") / F.col("total_rentals") * 100))
    .withColumn("repair_cost_per_rental",
        F.col("total_repair_costs_czk") / F.col("total_rentals"))
    .withColumn("health_score",
        # 0-100: vyšší = lepší
        F.round(
            F.least(F.lit(100),
                F.col("avg_rating") * 20 - F.col("damage_rate_pct") * 2
            )
        )
    )
    .orderBy(F.col("health_score").asc())
)

tool_reliability.write.format("delta") \
    .mode("overwrite") \
    .saveAsTable("gold_tool_reliability")

print(f"✓ gold_tool_reliability – které nástroje jsou problémové")
```

### 3.3 Gold: Revenue by Category

```python
# WHICH CATEGORY IS MOST PROFITABLE?
gold_category_performance = (
    silver_rentals
    .groupBy("tool_category")
    .agg(
        F.count("rental_id").alias("total_rentals"),
        F.sum("rental_revenue_czk").alias("total_revenue_czk"),
        F.sum("total_cost_czk").alias("total_costs_czk"),
        F.sum("net_profit_czk").alias("total_profit_czk"),
        F.avg("profit_margin_pct").alias("avg_margin_pct"),
        F.avg("customer_rating").alias("avg_rating")
    )
    .withColumn("roi_pct",
        (F.col("total_profit_czk") / F.col("total_costs_czk") * 100))
    .orderBy(F.col("total_profit_czk").desc())
)

gold_category_performance.write.format("delta") \
    .mode("overwrite") \
    .saveAsTable("gold_category_performance")

print(f"✓ gold_category_performance")
```

### 3.4 Gold: Staff Productivity

```python
silver_staff = spark.read.table("Lab01_Lakehouse.dbo.silver_staff_daily")
silver_rentals = spark.read.table("Lab01_Lakehouse.dbo.silver_rentals")

# DAILY RENTALS BY LOCATION
rentals_by_day = (
    silver_rentals
    .groupBy(F.to_date("rental_date").alias("date"), "location")
    .agg(
        F.count("rental_id").alias("daily_rentals"),
        F.sum("rental_revenue_czk").alias("daily_revenue_czk")
    )
)

# JOIN WITH STAFF
staff_vs_rentals = (
    rentals_by_day
    .join(silver_staff, ["date", "location"], "left")
    .fillna(0, ["rental_staff", "service_staff"])
    .withColumn("revenue_per_staff",
        F.col("daily_revenue_czk") / F.greatest(F.col("total_staff"), F.lit(1)))
    .withColumn("rentals_per_staff",
        F.col("daily_rentals") / F.greatest(F.col("total_staff"), F.lit(1)))
)

staff_vs_rentals.write.format("delta") \
    .mode("overwrite") \
    .saveAsTable("gold_staff_productivity")

print(f"✓ gold_staff_productivity – výkon zaměstnanců")
```

### 3.5 Gold: Maintenance Forecast

```python
# WHICH TOOLS NEED MAINTENANCE SOON?
from pyspark.sql.window import Window

tools_health = spark.read.table("Lab01_Lakehouse.dbo.silver_tools_health")

# TREND: Usage hours per day
tools_usage_trend = (
    tools_health
    .withColumn("usage_per_day",
        F.col("total_usage_hours") / 
        (F.datediff(F.current_date(), F.col("last_maintenance_date")) + 1))
    .withColumn("days_to_next_maintenance",
        (100 / F.greatest(F.col("usage_per_day"), F.lit(0.1))))  # Assume 100h cycle
    .select(
        "device_id",
        "tool_name",
        "location",
        "total_usage_hours",
        "last_maintenance_date",
        "days_until_maintenance",
        "maintenance_overdue",
        "days_to_next_maintenance",
        F.when(F.col("maintenance_overdue"), "URGENT")
            .when(F.col("days_to_next_maintenance") < 14, "SOON")
            .when(F.col("days_to_next_maintenance") < 30, "SCHEDULE")
            .otherwise("OK")
            .alias("maintenance_status")
    )
    .orderBy(F.col("days_to_next_maintenance").asc())
)

tools_usage_trend.write.format("delta") \
    .mode("overwrite") \
    .saveAsTable("gold_maintenance_forecast")

print(f"✓ gold_maintenance_forecast – predikce poruch")
```

---

## Krok 4: Data Quality Checks

**Notebook:** `lh_tool_quality_checks.py`

```python
from pyspark.sql import functions as F
import datetime

silver_rentals = spark.read.table("Lab01_Lakehouse.dbo.silver_rentals")
silver_tools = spark.read.table("Lab01_Lakehouse.dbo.silver_tools_health")

# CHECK 1: Negative profits
negative_profit = (
    silver_rentals
    .filter("net_profit_czk < -500")  # Výrazně ztrátové pronajímky
    .count()
)
print(f"⚠️  Rentals with negative profit > 500 CZK: {negative_profit}")

# CHECK 2: Missing rental duration
missing_duration = (
    silver_rentals
    .filter("rental_duration_days IS NULL OR rental_duration_days < 0")
    .count()
)
print(f"⚠️  Rentals with invalid duration: {missing_duration}")

# CHECK 3: Tools overdue for maintenance
overdue_maintenance = (
    silver_tools
    .filter("maintenance_overdue == True")
    .count()
)
print(f"⚠️  Tools overdue for maintenance: {overdue_maintenance}")

# CHECK 4: Data freshness
last_rental = (
    silver_rentals
    .agg(F.max("rental_date"))
    .collect()[0][0]
)
days_old = (datetime.date.today() - last_rental.date() if last_rental else None).days
print(f"ℹ️  Last rental data: {days_old} days old")

# CHECK 5: High damage rate per tool
high_damage_tools = (
    silver_rentals
    .groupBy("tool_id", "tool_name")
    .agg(
        F.sum(F.when(F.col("damage_reported"), 1).otherwise(0))
            .alias("damage_count"),
        F.count("rental_id").alias("total_rentals")
    )
    .withColumn("damage_rate", F.col("damage_count") / F.col("total_rentals"))
    .filter("damage_rate > 0.3")  # >30% damage rate
    .count()
)
print(f"⚠️  Tools with >30% damage rate: {high_damage_tools}")

# WRITE REPORT
quality_report = spark.createDataFrame([{
    "check_date": datetime.datetime.now(),
    "negative_profit_rentals": negative_profit,
    "invalid_duration": missing_duration,
    "overdue_maintenance_tools": overdue_maintenance,
    "data_age_days": days_old,
    "high_damage_tools": high_damage_tools
}])

quality_report.write.format("delta") \
    .mode("append") \
    .saveAsTable("quality_check_history")

print("✓ Quality checks completed")
```

---

## Krok 5: Automace – Scheduler

V Fabricu (Lakehouse → Notebooks):

```
lh_tool_silver_clean.py
├── Schedule: Každý den v 7:00
└── Timeout: 30 minut

lh_tool_gold_analytics.py
├── Schedule: Každý den v 7:30
└── Timeout: 20 minut

lh_tool_quality_checks.py
├── Schedule: Každý den v 8:00
└── Timeout: 10 minut
```

---

## Krok 6: Power BI Dashboards

### Dashboard 1: Rental Performance

```
Slicers:
├── Location (Praha, Brno, Ostrava)
├── Tool Category (pressure_washer, drill, grinder)
├── Date Range

Visuals:
├── Revenue vs Costs (bar chart) ← gold_category_performance
├── Profit Margin % (gauge)
├── Damaged Rentals % (KPI card)
├── Top/Bottom tools by profit (table) ← gold_tool_reliability
├── Rental trend (line) by date
└── Customer Rating Distribution (histogram)
```

### Dashboard 2: Tool Health & Maintenance

```
Slicers:
├── Location
├── Category

Visuals:
├── Maintenance Due (list of tools) ← gold_maintenance_forecast
├── Tools by Usage Hours (scatter)
├── Error Rate per Tool (bar) ← silver_tools_health
├── Maintenance Cost vs Rental Revenue (scatter per tool)
├── Filter Status Alert (card showing "critical" count)
└── Days Since Last Maintenance (sorted list)
```

### Dashboard 3: Staff Productivity

```
Slicers:
├── Location
├── Date Range

Visuals:
├── Revenue per Staff Member (KPI)
├── Rentals per Staff (trend line)
├── Staff Overtime vs Revenue (correlation scatter)
├── Employees on Vacation (line over time)
├── Revenue by Department (rental vs service)
└── Staff Utilization Heat Map (by day/location)
```

### Dashboard 4: Financial

```
Visuals:
├── Category Profitability (pie chart)
├── ROI by Category (bar) ← gold_category_performance
├── Unpaid Invoices (card)
├── Revenue Trend (line)
├── Repair Cost as % of Rental Revenue (line)
└── Warranty Claims vs Non-Warranty (pie)
```

---

## Analýzy, které dělají smysl

### Analýza 1: Která nářadí se dají odprodávat?

```python
# Nástroje s vysokou damage rate a nízkou rating
gold_tool_reliability.filter(
    (F.col("damage_rate_pct") > 40) & 
    (F.col("avg_rating") < 3)
)
```

**Insight:** Tyto nástroje výdělávají ztráty – přeměnit na náhradní díly nebo odprodávat.

### Analýza 2: Kdy je nejrušněji?

```python
# Která data (dny týdne) mají nejvíce pronajímek
silver_rentals
    .withColumn("day_of_week", F.dayofweek("rental_date"))
    .groupBy("day_of_week")
    .agg(F.count("rental_id").as_("rentals_count"))
```

**Insight:** Zaměřit personál na busy dny, věnovat péči na tiché dny servisům.

### Analýza 3: Korelace: Počet zaměstnanců vs Tržby

```python
# Correlation analysis
gold_staff_productivity
    .select(
        F.corr("total_staff", "daily_revenue_czk")
            .over(Window.partitionBy("location"))
    )
```

**Insight:** Jestli je to > 0.7 correlace, stojí to za najímání víc lidí.

### Analýza 4: Predictive: Kdy se daný nástroj porouchá?

```python
# Time to failure prediction
tools_failure_prediction = (
    gold_maintenance_forecast
    .filter("maintenance_overdue == True")
    .select("device_id", "tool_name", "days_to_next_maintenance")
)
```

**Insight:** Dát nářadí do preventivního servisu PŘED poruchou.

### Analýza 5: Customer Lifetime Value

```python
# Which customers rent the most?
silver_rentals
    .groupBy("customer_id")
    .agg(
        F.count("rental_id").as_("rental_count"),
        F.sum("rental_revenue_czk").as_("lifetime_value"),
        F.avg("customer_rating").as_("avg_satisfaction")
    )
    .orderBy(F.col("lifetime_value").desc())
    .limit(20)
```

**Insight:** Segmentuj zákazníky, dej jim VIP obsluhu.

---

## GitHub struktura

```
hobbytools-analytics/
├── README.md
│   ├── Case study kontext
│   ├── Architecture diagram
│   ├── Setup instructions (jak si to spustit lokálně)
│   └── KPI definitions
│
├── docs/
│   ├── Data_Dictionary.md (sloupce, typy, business pravidla)
│   ├── KPI_Definitions.md (co znamená "health_score")
│   ├── Data_Lineage.md (ASCII diagramy - bronze→silver→gold)
│   ├── Architecture.md (detailní popis vrstev)
│   ├── Troubleshooting.md (když si to spustíš a nefunguje to)
│   └── Cost_Analysis.md (kolik to stojí)
│
├── notebooks/
│   ├── 01_INGESTION_Dataflow_Gen2.md
│   │   └── Screenshots bez kódu – jak se to nastaví v Fabricu
│   ├── 02_lh_tool_silver_clean.py
│   ├── 03_lh_tool_gold_analytics.py
│   ├── 04_lh_tool_quality_checks.py
│   └── README.md (jak spustit)
│
├── sql_queries/
│   ├── analysis_tool_failure_prediction.sql
│   ├── analysis_staff_impact.sql
│   ├── analysis_customer_segments.sql
│   └── maintenance_alerts.sql
│
├── power_bi/
│   ├── reports/
│   │   ├── 01_Rental_Performance.pbix
│   │   ├── 02_Tool_Health_Maintenance.pbix
│   │   ├── 03_Staff_Productivity.pbix
│   │   └── 04_Financial_Dashboard.pbix
│   └── README.md (jak se dashboardy připojují k gold tabulkám)
│
├── synthetic_data/
│   ├── bronze_rentals_sample.csv (20 řádků na vyzkoušení)
│   ├── bronze_tools_sample.csv
│   ├── bronze_repairs_sample.csv
│   ├── bronze_staff_sample.csv
│   └── generate_synthetic_data.py (Python skript na vygenerování dat)
│
├── tests/
│   ├── test_data_quality.py
│   ├── test_schema_validation.py
│   └── test_calculations.py
│
└── LICENSE (MIT)
```

---

## Co se dělá v praxi – role Data Engineera

### Týden 1-2: Discovery & Understanding
- Seznámit se s byznysem (jak HobbyTools funguje?)
- Mapovat data sources
- Pochopit pain points (co je teď v Excelu vs co by mohlo být automatizované?)

### Týden 3: Architecture Design
- Nakreslit diagramy (bronze/silver/gold)
- Navrhnout skriptování
- Diskutovat s vedením: Jaké KPI jsou nejdůležitější?

### Týden 4-6: Implementation
- Dataflow Gen2 pipelines (ingestion)
- Python notebooks (transformace)
- SQL queries (agregace)
- Data quality checks

### Týden 7: Power BI Integrace
- Pomoct BI analytikovi připojit datasety
- Vytvořit sample dashboardy
- Doladit výkon (partitioning, indexing)

### Týden 8+: Monitoring & Optimization
- Kontrolovat data freshness
- Alarm na anomálie
- Optimalizovat compute costs
- Feedback od uživatelů → změny

---

## Real-world insights (co by z toho mohla firma zjistit)

1. **Drills jsou ztrátující business** – 40% damage rate, 80 CZK/rental overhead
   → Řešení: Vyprodaj, nahraď levnějším modelem

2. **Pondelí-pátek je business, víkendy mrtvé**
   → Řešení: Personál jen na work days

3. **5 zaměstnanců by stačilo** (místo nynějších 8) s 95% satisfaction
   → Řešení: Efektivita, lepší proces

4. **Praha je 3x ziskovější než Brno**
   → Řešení: Zkopírovat proces z Prahy do Brna

5. **Nářadí se porouchá 20 dní PŘED maintenance**
   → Řešení: Preventivní servis, snížení downtime

---

## Jak to spustit s veřejnými daty

Možnosti:
1. **Synthetic data**: `generate_synthetic_data.py` v repo → CSV
2. **Kaggle**: Użij "Predictive Maintenance Equipment Dataset"
3. **Vlastní data**: Exportuj z Excel, anonimizuj

Je to ready na GitHub. Public, free, a real-world relevantní!

Chceš, abych ti vytvořil **Python skript na generování synthetic dat**? Pak se to dá klidně spustit bez připojení na produkční DB.
