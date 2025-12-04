# 📊 22-TÝDENNÍ POKROČILÝ STUDIJNÍ PLÁN: Data Modeling & Lakehouse

**Cíl:** Od fundamentů k Senior Junior Data Engineer s pochopením datového modelování, Lakehouse architecture a enterprise workflow

**Časový rámec:** Listopad 2025 - Březen 2026 (161 dní = ~23 týdnů)

**Výstup:**
- ✅ 3 portfoliové projekty (Local ETL → Cloud → Real-time)
- ✅ Porozumění Star Schema, Data Vault, Lakehouse
- ✅ Databricks/Delta Lake hands-on zkušenost
- ✅ Datová kvalita a governance
- ✅ AI-driven features (Natural Language, sentiment analysis)

---

## 🗓️ 22-TÝDENNÍ PLÁN (Detailní rozvrh)

### FÁZE 1: FUNDAMENTY A ARCHITEKTURA (Týdny 1-2)

#### Týden 1: Úvod do Data Engineeringu a Moderních Architektur

**Hlavní témata:**
- Co je Data Engineering? Role, odpovědnosti, kariérní cesty
- Evoluce: Data Warehouse → Data Lake → Lakehouse
- Klíčové pojmy: ETL vs ELT, Batch vs Streaming

**Učební cíle:**
- [ ] Rozumím rozdílu mezi DW, DL, Lakehouse
- [ ] Vím, co dělá Data Engineer vs Data Analyst vs Data Scientist
- [ ] Znám základní workflow: Source → Raw → Process → Insight

**Praktika:**
```python
# Diagram: Datové toky v Lakehouse
# Source (API, Database) 
#   ↓
# Raw (Bronze)
#   ↓
# Clean (Silver)
#   ↓
# Business Ready (Gold)
#   ↓
# BI/AI Applications
```

**Obsidian:**
- `Learn/01-Data-Engineering-Fundamentals.md`
- Zapiš si: architektury, role, workflow

**GitHub Task:**
```bash
git add docs/01-Lakehouse-Architecture.md
git commit -m "📊 Understanding Lakehouse architecture"
```

**Příští týden:** Data modelování - jak strukturovat data?

---

#### Týden 2: Základní Datové Modelování - Logické a Fyzické Modely

**Hlavní témata:**
- Logický model vs Fyzický model
- Modelování pro DW/OLAP systémy
- Fakta (Measures), Dimenze (Context)
- Popis, kardinalita, hierarchie

**Učební cíle:**
- [ ] Rozumím rozdílu mezi logickým a fyzickým modelem
- [ ] Vím, co je fakt a co je dimenze
- [ ] Znám typy faktů: additive, semi-additive, non-additive
- [ ] Vím, co je kardinalita a hierarchie dimenzí

**Praktika:**
```python
# Příklad: Tabulka objednávek (Sales Pipeline)

# FACT TABLE - Prodeje
SELECT order_id, date_id, customer_id, product_id, 
       quantity, revenue, cost
FROM fact_sales;

# DIMENSION TABLE - Čas
SELECT date_id, date, month, quarter, year
FROM dim_date;

# DIMENSION TABLE - Produkt
SELECT product_id, name, category, supplier_id
FROM dim_product;

# DIMENSION TABLE - Zákazník
SELECT customer_id, name, country, segment
FROM dim_customer;
```

**Obsidian:**
- `Learn/02-Logical-Physical-Models.md`
- Zapiš si: fact types, dimensions, hierarchy

**GitHub Task:**
```bash
git add projects/01-etl-local/data_model.md
git commit -m "📋 Creating dimensional model for sales"
```

**Příští týden:** Star Schema a normalizace!

---

### FÁZE 2: DIMENZIONÁLNÍ MODELOVÁNÍ (Týdny 3-7)

#### Týden 3: Star Schema - Nejjednodušší Přístup

**Hlavní témata:**
- Star Schema principy
- Centrální fact tabulka obklopená dimenzemi
- Denormalizace pro rychlost
- Index strategie

**Učební cíle:**
- [ ] Znám Star Schema pattern
- [ ] Vím, kdy použít Star vs Snowflake
- [ ] Rozumím denormalizaci v praxi
- [ ] Vím, jak designovat fact tabulku bez redundance

**Praktika:**
```sql
-- Star Schema: Fact + 4 Dimensions

-- FACT TABLE (malé, jen obchodní metriky)
CREATE TABLE fact_sales (
    order_id INT PRIMARY KEY,
    date_id INT,           -- FK do dim_date
    customer_id INT,       -- FK do dim_customer
    product_id INT,        -- FK do dim_product
    quantity INT,
    revenue DECIMAL(10,2),
    cost DECIMAL(10,2)
);

-- DIMENSION TABLES (velké, atributy)
CREATE TABLE dim_date (
    date_id INT PRIMARY KEY,
    date DATE,
    month VARCHAR(10),
    quarter INT,
    year INT
);

CREATE TABLE dim_customer (
    customer_id INT PRIMARY KEY,
    name VARCHAR(100),
    country VARCHAR(50),
    segment VARCHAR(20),
    registration_date DATE
);

-- Query: Tržby za kategorie produktů
SELECT 
    dp.category,
    SUM(fs.revenue) as total_revenue,
    COUNT(*) as order_count
FROM fact_sales fs
INNER JOIN dim_date dd ON fs.date_id = dd.date_id
INNER JOIN dim_product dp ON fs.product_id = dp.product_id
WHERE dd.year = 2025
GROUP BY dp.category
ORDER BY total_revenue DESC;
```

**Obsidian:**
- `Learn/03-Star-Schema.md`
- Zapiš si: design pattern, query examples

**GitHub Task:**
```bash
git add projects/01-etl-local/star_schema.sql
git commit -m "⭐ Implementing Star Schema for sales"
```

**Příští týden:** Snowflake Schema - komplexnější modely

---

#### Týden 4: Snowflake Schema - Normalizovaný Přístup

**Hlavní témata:**
- Snowflake Schema: normalizované dimenze
- Trade-off: méně redundance vs více joinů
- Kdy volit Snowflake vs Star
- Hierarchie dimenzí v Snowflake

**Učební cíle:**
- [ ] Znám Snowflake Schema pattern
- [ ] Vím, kdy je Snowflake lepší než Star
- [ ] Rozumím hierarchiím v Snowflake
- [ ] Vím o performance trade-offech

**Praktika:**
```sql
-- Snowflake Schema: Normalizované Dimenze

-- FACT TABLE (stejné jako Star)
CREATE TABLE fact_sales (
    order_id INT PRIMARY KEY,
    date_id INT,
    customer_id INT,
    product_id INT,
    quantity INT,
    revenue DECIMAL(10,2)
);

-- DIMENSION: Produkt (nyní normalizovaná!)
CREATE TABLE dim_product (
    product_id INT PRIMARY KEY,
    name VARCHAR(100),
    category_id INT  -- FK do dim_category
);

CREATE TABLE dim_category (
    category_id INT PRIMARY KEY,
    category_name VARCHAR(50),
    subcategory_id INT  -- FK do dim_subcategory
);

CREATE TABLE dim_subcategory (
    subcategory_id INT PRIMARY KEY,
    subcategory_name VARCHAR(50)
);

-- Query: Tržby za podkategorie
-- POZOR: Více joinů! Ale méně redundance
SELECT 
    ds.subcategory_name,
    dc.category_name,
    SUM(fs.revenue) as total_revenue
FROM fact_sales fs
INNER JOIN dim_product dp ON fs.product_id = dp.product_id
INNER JOIN dim_category dc ON dp.category_id = dc.category_id
INNER JOIN dim_subcategory ds ON dc.subcategory_id = ds.subcategory_id
GROUP BY ds.subcategory_name, dc.category_name;
```

**Obsidian:**
- `Learn/04-Snowflake-Schema.md`
- Porovnání: Star vs Snowflake

**GitHub Task:**
```bash
git add projects/01-etl-local/snowflake_schema.sql
git commit -m "❄️ Comparing Star vs Snowflake Schema"
```

**Příští týden:** SCD - jak se dimenze mění v čase?

---

#### Týden 5: Slowly Changing Dimensions (SCD) Type 1 & 2

**Hlavní témata:**
- SCD Type 0: Nechánout jak je (historii nehlídáme)
- SCD Type 1: Přepsat (žádná historie)
- SCD Type 2: Nová řádka (komplétní historie)
- SCD Type 3: Extra sloupce (limitovaná historie)

**Učební cíle:**
- [ ] Znám všechny SCD typy
- [ ] Vím, kdy použít Type 1 vs Type 2 vs Type 3
- [ ] Umím implementovat SCD v Pythonu/SQL
- [ ] Rozumím surrogate keys pro Type 2

**Praktika:**
```python
# Příklad: Dimenze Zákazník - SCD Type 2

# SCD Type 2: Nová řádka s historií
# Zákazník změní bydliště → nová řádka!

# Originální data:
customer_id=1, name="Jan", country="CZ", effective_date="2023-01-01", end_date=NULL

# Zákazník se stěhuje do Německa (2025-06-15)
# Nová řádka:
customer_id=1, name="Jan", country="CZ", effective_date="2023-01-01", end_date="2025-06-15"
customer_id=1, name="Jan", country="DE", effective_date="2025-06-16", end_date=NULL

# Výhoda: Historické analýzy fungují!
# "Kolik Čechů nám odjelo do zahraničí?"
```

```sql
-- Implementace SCD Type 2 v SQL (MERGE pattern)
MERGE INTO dim_customer dc
USING (SELECT * FROM staging_customer) sc
ON dc.customer_id = sc.customer_id AND dc.is_current = 1
WHEN MATCHED AND dc.country != sc.country THEN
    UPDATE SET is_current = 0, end_date = CURRENT_DATE
WHEN NOT MATCHED THEN
    INSERT (customer_id, name, country, effective_date, end_date, is_current)
    VALUES (sc.customer_id, sc.name, sc.country, CURRENT_DATE, NULL, 1);
```

**Obsidian:**
- `Learn/05-SCD-Types.md`
- Praktické příklady, diagramy

**GitHub Task:**
```bash
git add projects/01-etl-local/scd_implementation.py
git commit -m "📅 Implementing SCD Type 2 for slowly changing dimensions"
```

**Příští týden:** Speciální dimenze - Role-Playing, Junk, Degenerate

---

#### Týden 6: Speciální Dimenze a Pokročilé Koncepty

**Hlavní témata:**
- Degenerate Dimension (klíč bez tabulky)
- Junk/Garbage Dimension (nízko-kardinalitní vlajky)
- Role-Playing Dimension (jedna tabulka, více rolí)
- Fast Changing Dimension (mini-dimenze)

**Učební cíle:**
- [ ] Znám speciální dimenze patterny
- [ ] Vím, kdy je použít
- [ ] Rozumím deskriptivním atributům
- [ ] Vím, jak optimalizovat kardinalitu

**Praktika:**
```sql
-- Příklady:

-- 1. DEGENERATE DIMENSION
-- TransactionNo bez tabulky - existuje jen v faktu!
CREATE TABLE fact_transactions (
    transaction_no VARCHAR(20),  -- Degenerate DIM
    order_id INT,
    amount DECIMAL(10,2)
);

-- 2. JUNK DIMENSION
-- Kombinuje nízko-kardinalitní vlajky
CREATE TABLE dim_order_flags (
    order_flag_id INT PRIMARY KEY,
    is_rush_order BIT,           -- 2 hodnoty: 0/1
    is_priority_customer BIT,    -- 2 hodnoty: 0/1
    payment_method VARCHAR(10)   -- 5 možností
    -- Kombinace: 2 × 2 × 5 = 20 řádků maximálně!
);

-- 3. ROLE-PLAYING DIMENSION
-- Stejná tabulka hraje více rolí (různé datum)
-- Tabulka: dim_date
-- Fact table:
CREATE TABLE fact_orders (
    order_id INT,
    order_date_id INT,      -- FK do dim_date (Role 1: Kdy byla objednaná)
    ship_date_id INT,       -- FK do dim_date (Role 2: Kdy byla odeslána)
    delivery_date_id INT,   -- FK do dim_date (Role 3: Kdy dorazila)
    amount DECIMAL(10,2)
);
```

**Obsidian:**
- `Learn/06-Special-Dimensions.md`
- Diagramy a use cases

**GitHub Task:**
```bash
git add projects/01-etl-local/special_dimensions.sql
git commit -m "🎭 Implementing Role-Playing, Junk, Degenerate Dimensions"
```

**Příští týden:** Mini project - praktické modelování

---

#### Týden 7: Mini Project - Datové Modelování v Praxi

**Projekt:** Postavit dimenzionální model pro E-commerce (Star Schema)

**Specifikace:**
```
Source data:
- Orders (order_id, customer_id, product_id, order_date, quantity, price)
- Customers (customer_id, name, email, country, signup_date)
- Products (product_id, name, category, price, supplier_id)
- Calendar (date, month, quarter, year)

Výstup:
- fact_sales (order_id, date_id, customer_id, product_id, quantity, revenue, cost)
- dim_date (date_id, date, month, quarter, year)
- dim_customer (customer_id, name, email, country, segment, is_current)
- dim_product (product_id, name, category, supplier_id)
```

**Deliverable:**
- SQL script: CREATE TABLEs + indexy
- Dokumentace: Entity Relationship Diagram
- 5x sample queries

**GitHub Task:**
```bash
git add projects/Project-1-ETL-Local/ecommerce_model.sql
git add projects/Project-1-ETL-Local/README.md
git commit -m "🎯 E-commerce dimensional model complete"
```

**Příští týden:** Fáze 3 - Data Vault!

---

### FÁZE 3: DATA VAULT A MODERNÍ PŘÍSTUPY (Týdny 8-9)

#### Týden 8: Data Vault - Enterprise Approach

**Hlavní témata:**
- Data Vault metodologie: Hub-Link-Satellite
- Proč Data Vault? (flexibility, auditovatelnost, skalabilita)
- Hub: jedinečné business klíče
- Link: vztahy mezi hubem
- Satellite: atributy a historie

**Učební cíle:**
- [ ] Rozumím Data Vault struktuře (Hub-Link-Sat)
- [ ] Vím, kdy volit Data Vault vs Dimensional
- [ ] Znám výhody flexibilitu Vault
- [ ] Umím navrhovat Hub tabulky

**Praktika:**
```sql
-- Data Vault: Hub-Link-Satellite Pattern

-- HUB: Jedinečné business klíče
CREATE TABLE hub_customer (
    customer_key INT PRIMARY KEY SURROGATE,
    customer_id INT,              -- Business Key
    load_date TIMESTAMP,
    record_source VARCHAR(20)
);

-- HUB: Produkty
CREATE TABLE hub_product (
    product_key INT PRIMARY KEY SURROGATE,
    product_id INT,               -- Business Key
    load_date TIMESTAMP,
    record_source VARCHAR(20)
);

-- LINK: Vztahy (Customer koupit Product)
CREATE TABLE link_customer_product (
    link_key INT PRIMARY KEY SURROGATE,
    customer_key INT,             -- FK hub_customer
    product_key INT,              -- FK hub_product
    load_date TIMESTAMP,
    record_source VARCHAR(20)
);

-- SATELLITE: Atributy (změny v čase)
CREATE TABLE sat_customer_details (
    customer_key INT,             -- FK hub_customer
    load_date TIMESTAMP,
    name VARCHAR(100),
    email VARCHAR(100),
    country VARCHAR(50),
    end_date TIMESTAMP
);

CREATE TABLE sat_product_details (
    product_key INT,              -- FK hub_product
    load_date TIMESTAMP,
    name VARCHAR(100),
    category VARCHAR(50),
    price DECIMAL(10,2),
    end_date TIMESTAMP
);

-- Výhoda: Když se přidá nový produkt:
-- Stačí přidat řádku do hub_product a satelit
-- Nemusíš měnit ostatní struktury!
-- SUPER flexibilní pro enterprise
```

**Obsidian:**
- `Learn/08-Data-Vault.md`
- Hub-Link-Sat diagram, výhody

**GitHub Task:**
```bash
git add projects/01-etl-local/data_vault_model.sql
git commit -m "🏢 Implementing Data Vault Hub-Link-Satellite"
```

**Příští týden:** Lakehouse!

---

#### Týden 9: Lakehouse Fundamenty - Bronze, Silver, Gold

**Hlavní témata:**
- Lakehouse = DL + DW v jedné platformě
- Medallion Architecture: Bronze → Silver → Gold
- Delta Lake formát
- Unity Catalog pro governance

**Učební cíle:**
- [ ] Rozumím Medallion Architecture
- [ ] Vím, co patří do Bronze/Silver/Gold
- [ ] Znám výhody Lakehouse
- [ ] Vím, jak propojit s dimensional modeling

**Praktika:**
```python
# Medallion Architecture v Databricks

# BRONZE: Raw data - "as-is" z source
# - API response → JSON v parquet
# - Database export → CSV v parquet
# - Streaming data → Delta
# Transformace: Jen conversions (JSON→tabular, dedup)

bronze_orders = spark.read.parquet("s3://bucket/bronze/orders/")
# Obsah: raw_data BLOB, ingestion_date, source_system

# SILVER: Enterprise view - čištění, konformace
# - Duplikáty odstraněny
# - Null valuesolved
# - Data types konvertovány
# - Business rules aplikovány
# - МОЖЕТ být začátek dim modelingu!

silver_orders = (
    bronze_orders
    .dropDuplicates(["order_id"])
    .filter("order_id IS NOT NULL")
    .withColumn("order_date", F.col("raw_date").cast("date"))
    .drop("raw_data", "ingestion_date")
)

# GOLD: Presentation layer - Business ready
# - Star Schema či Dimensional Model
# - Optimalizováno pro BI dotazy
# - Lze číst bezpečně (sem mají přístup analytici)

gold_fact_sales = (
    silver_orders
    .join(silver_customers, "customer_id")
    .join(silver_products, "product_id")
    .select("order_id", "customer_id", "product_id", "order_date", "quantity", "revenue")
)

# Write to Gold:
gold_fact_sales.write.mode("overwrite") \
    .option("mergeSchema", "true") \
    .format("delta") \
    .saveAsTable("gold.fact_sales")
```

**Obsidian:**
- `Learn/09-Lakehouse-Medallion.md`
- Bronze/Silver/Gold workflow, Python code

**GitHub Task:**
```bash
git add projects/01-etl-local/medallion_architecture.py
git commit -m "🏪 Medallion Architecture: Bronze → Silver → Gold"
```

**Příští fáze:** Orchestrace a pipeline!

---

### FÁZE 4: PIPELINE, WORKFLOW, ORCHESTRACE (Týdny 10-11)

#### Týden 10: ETL/ELT Orchestrace s Airflow a Databricks

**Hlavní témata:**
- Airflow DAGs pro orchestraci
- Databricks Workflows (native)
- Batch vs Streaming vs Micro-batch
- Idempotentní a inkrementální zátěž

**Učební cíle:**
- [ ] Znám Airflow DAG patterns
- [ ] Rozumím Watermarks (inkrementální zátěži)
- [ ] Vím, jak dělat MERGE (upsert)
- [ ] Znám batch vs streaming trade-offs

**Praktika:**
```python
# Airflow DAG: Bronze → Silver → Gold Pipeline

from airflow import DAG
from airflow.operators.python import PythonOperator
from datetime import datetime, timedelta

default_args = {
    'owner': 'data-engineering',
    'retries': 2,
    'retry_delay': timedelta(minutes=5)
}

dag = DAG(
    'etl_lakehouse_pipeline',
    default_args=default_args,
    description='Medallion ETL: Bronze → Silver → Gold',
    schedule_interval='@daily',
    start_date=datetime(2025, 11, 1)
)

def extract_to_bronze():
    """Load raw data from source to Bronze"""
    # API/Database → S3 Bronze layer (parquet)
    pass

def transform_to_silver():
    """Clean and validate data in Silver"""
    # Bronze → Silver (dedup, null handling, type casting)
    pass

def build_gold_layer():
    """Create dimensional model in Gold"""
    # Silver → Gold (Star Schema, fact + dimensions)
    pass

def publish_to_bi():
    """Publish to BI tools"""
    # Gold → PowerBI / Tableau refresh
    pass

# Define tasks
t1 = PythonOperator(task_id='extract_bronze', python_callable=extract_to_bronze, dag=dag)
t2 = PythonOperator(task_id='transform_silver', python_callable=transform_to_silver, dag=dag)
t3 = PythonOperator(task_id='build_gold', python_callable=build_gold_layer, dag=dag)
t4 = PythonOperator(task_id='publish_bi', python_callable=publish_to_bi, dag=dag)

# Define dependencies
t1 >> t2 >> t3 >> t4
```

```python
# Inkrementální zátěž s Watermarks (SQL)
# "Poslední synchronizace: 2025-11-01 10:00"

def incremental_load():
    """Načti jen nová data od poslední synchronizace"""
    
    # Čti watermark
    last_sync = spark.sql("SELECT MAX(load_date) FROM silver.load_watermark").collect()[0][0]
    
    # Čti nová data
    new_data = spark.sql(f"""
        SELECT * FROM bronze.orders 
        WHERE ingestion_date > '{last_sync}'
    """)
    
    # MERGE do Silver (upsert - insert if new, update if changed)
    new_data.write.format("delta").mode("merge") \
        .option("mergeSchema", "true") \
        .saveAsTable("silver.orders")
    
    # Update watermark
    spark.sql(f"""
        INSERT INTO silver.load_watermark 
        VALUES ('{datetime.now()}')
    """)
```

**Obsidian:**
- `Learn/10-Pipeline-Orchestration.md`
- DAG patterns, watermarks

**GitHub Task:**
```bash
git add projects/02-cloud-pipeline/airflow_dag.py
git commit -m "🔄 ETL/ELT orchestration with Airflow and incremental loads"
```

**Příští týden:** Datová kvalita a governance!

---

#### Týden 11: Data Quality, Governance, Unity Catalog

**Hlavní témata:**
- Data Quality checks (EXPECT, DROP, FAIL)
- PK/FK constraints (informativní)
- Identity Columns pro Surrogate Keys
- Unity Catalog pro centralizovanou správu

**Učební cíle:**
- [ ] Znám DQ check patterns
- [ ] Vím, jak implementovat constraints
- [ ] Rozumím Unity Catalog
- [ ] Znám Environment-aware ACLs

**Praktika:**
```python
# Data Quality v Databricks

from databricks.sdk.runtime import sql

# Constraint 1: NOT NULL
spark.sql("""
    ALTER TABLE silver.orders 
    ADD CONSTRAINT order_id_not_null 
    CHECK (order_id IS NOT NULL)
""")

# Constraint 2: Surrogate key
spark.sql("""
    CREATE TABLE gold.dim_customer (
        customer_key INT GENERATED BY DEFAULT AS IDENTITY,
        customer_id INT NOT NULL,
        name VARCHAR(100) NOT NULL,
        country VARCHAR(50)
    )
""")

# Data Quality Checks (Delta Live Tables)
import dlt

@dlt.table(quality='silver')
def orders_with_quality():
    return spark.sql("""
        SELECT 
            order_id,
            customer_id,
            order_date,
            amount
        FROM bronze.orders
        WHERE order_id IS NOT NULL
            AND amount > 0
            AND order_date BETWEEN '2020-01-01' AND CURRENT_DATE
    """)

# Unity Catalog: Centralizovaná správa

# Level 1: CATALOG (prostředí: prod, staging, dev)
# Level 2: SCHEMA (business area: finance, marketing, sales)
# Level 3: TABLE/VIEW (konkrétní objekt)

# Příklad:
# prod.finance.fact_revenue
# staging.marketing.dim_campaign
# dev.sales.stg_orders

# ACL: Kdo má přístup?
spark.sql("""
    GRANT SELECT ON SCHEMA prod.finance TO finance_team
    GRANT MODIFY ON TABLE prod.finance.fact_revenue TO finance_admin
    GRANT READ_METADATA ON CATALOG prod TO all_users
""")

# Lineage tracking (automaticky!)
# Databricks vidí: bronze.orders → silver.orders → gold.fact_sales
```

**Obsidian:**
- `Learn/11-Data-Quality-Governance.md`
- DQ patterns, constraints, ACLs

**GitHub Task:**
```bash
git add projects/02-cloud-pipeline/data_quality_checks.py
git commit -m "✅ Data Quality checks and Unity Catalog governance"
```

**Následující fáze:** Cloud platforms!

---

### FÁZE 5: CLOUD PLATFORMY A INTEGRACE (Týdny 12-13)

#### Týden 12: Cloud Platforms - AWS, Azure, GCP

**Hlavní témata:**
- AWS (S3, Redshift, Glue, EMR)
- Azure (Blob, Synapse, Data Factory)
- GCP (Storage, BigQuery, Dataflow)
- Databricks na všech cloud platformách

**Učební cíle:**
- [ ] Znám cloud services pro data eng
- [ ] Vím, jak zvolit cloud platformu
- [ ] Rozumím hybridním přístupům
- [ ] Znám Databricks availability

**Praktika:**
```python
# AWS: S3 + Glue + Redshift

# 1. Data v S3 (Bronze layer)
s3_path = "s3://my-bucket/bronze/orders/"

# 2. Glue Crawler: Automatické schema discovery
# AWS Glue → crawls S3 → detects schema → Glue Catalog

# 3. SQL v Athena (query S3 přímo bez ETL)
spark.sql("""
    SELECT order_id, customer_id, amount 
    FROM s3_bronze_orders 
    WHERE order_date = '2025-11-01'
""")

# 4. Redshift: DW pro analytics
# UNLOAD data do Redshift pro BI
```

```python
# Azure: Blob Storage + Synapse + Data Factory

# 1. Data v Azure Blob (Bronze)
blob_path = "wasbs://container@account.blob.core.windows.net/bronze/"

# 2. Azure Synapse: SQL DW (like Redshift)
# Dedicated SQL Pool pro data warehouse

# 3. Azure Data Factory: Orchestration (like Airflow)
# Visual ETL builder
```

```python
# GCP: BigQuery (Serverless DW!) + Cloud Storage + Dataflow

# 1. Data v Cloud Storage (Bronze)
gcs_path = "gs://my-bucket/bronze/orders/"

# 2. BigQuery: SQL DW bez provisioning!
spark.sql("""
    SELECT order_id, SUM(amount) 
    FROM `project.dataset.fact_sales` 
    GROUP BY order_id
""")

# 3. Dataflow: Stream processing (like Spark Streaming)
```

**Obsidian:**
- `Learn/12-Cloud-Platforms.md`
- AWS vs Azure vs GCP porovnání

**GitHub Task:**
```bash
git add docs/cloud-platforms-comparison.md
git commit -m "☁️ Cloud platforms: AWS, Azure, GCP comparison"
```

**Příští týden:** Integrace + dbt!

---

#### Týden 13: Integrace (Fivetran, dbt Labs) a Transformace

**Hlavní témata:**
- Fivetran: ELT (Extract-Load-Transform)
- dbt: SQL transformace, testing, docs
- CI/CD s dbt
- Change Data Capture (CDC)

**Učební cíle:**
- [ ] Znám Fivetran workflow (ELT pattern)
- [ ] Umím psát dbt modely
- [ ] Vím, jak dělat dbt testing
- [ ] Rozumím CDC pro real-time

**Praktika:**
```yaml
# Fivetran: Deklarativní ETL
# Config v YAML - vše se synchronizuje!

connector: salesforce
destination: snowflake
sync_frequency: 1440  # každých 24h

schema_settings:
  Account:
    - Id
    - Name
    - Revenue
  Opportunity:
    - Id
    - AccountId
    - Amount
    - StageName
    - CloseDate

# Fivetran automatic:
# - Crawluje schema ze Salesforce
# - Pushuje do Snowflake (DBT format)
# - Dělá SCD Type 2 automaticky!
```

```sql
-- dbt: SQL transformace s verzí kontorem

-- models/staging/stg_orders.sql
SELECT 
    order_id,
    customer_id,
    CAST(order_date AS DATE) as order_date,
    ROUND(quantity * unit_price, 2) as revenue
FROM {{ source('raw', 'orders') }}
WHERE order_id IS NOT NULL

-- tests/stg_orders_tests.yml
models:
  - name: stg_orders
    columns:
      - name: order_id
        tests:
          - unique
          - not_null
      - name: revenue
        tests:
          - assert_positive_revenue

-- models/marts/fact_sales.sql
SELECT 
    {{ dbt_utils.surrogate_key(['order_id', 'order_date']) }} as sales_key,
    order_id,
    customer_id,
    order_date,
    revenue
FROM {{ ref('stg_orders') }}

-- dbt run → builds all models
-- dbt test → runs all tests
-- dbt docs generate → auto documentation!
```

**Obsidian:**
- `Learn/13-Fivetran-dbt-Integration.md`
- ELT vs ETL, dbt workflow

**GitHub Task:**
```bash
git add projects/02-cloud-pipeline/dbt_project/
git commit -m "🏗️ dbt transformations with testing and documentation"
```

**Následující fáze:** BI, AI, a pokročilé optimalizace!

---

### FÁZE 6: BI, AI, A POKROČILÉ OPTIMALIZACE (Týdny 14-17)

#### Týden 14: BI, Natural Language, a DatabricksIQ

**Hlavní témata:**
- BI reporting: Power BI, Tableau, Databricks SQL
- Natural Language Queries
- DatabricksIQ: AI pro semantic layer
- AI Functions (sentiment analysis v SQL)

**Učební cíle:**
- [ ] Umím psát BI dotazy
- [ ] Vím, jak queryovat přirozeným jazykem
- [ ] Rozumím DatabricksIQ
- [ ] Znám AI functions

**Praktika:**
```python
# Natural Language Query v Databricks SQL

# Normální SQL:
SELECT 
    DATE_TRUNC('MONTH', order_date) as month,
    SUM(revenue) as total_revenue,
    COUNT(*) as order_count
FROM gold.fact_sales
WHERE order_date >= DATE_SUB(CURRENT_DATE, INTERVAL 12 MONTH)
GROUP BY 1
ORDER BY 1 DESC;

# Přirozený jazyk (DatabricksIQ):
# "Show me monthly revenue trend for past year"
# → AI přeloží na SQL výše! 🤯

# AI Functions: Sentiment analysis
SELECT 
    customer_id,
    feedback_text,
    AI.SENTIMENT_ANALYSIS(feedback_text) as sentiment_score,
    CASE 
        WHEN sentiment_score > 0.7 THEN 'Positive'
        WHEN sentiment_score < 0.3 THEN 'Negative'
        ELSE 'Neutral'
    END as sentiment
FROM gold.customer_feedback;
```

**Obsidian:**
- `Learn/14-BI-Natural-Language.md`
- NLQ examples, DatabricksIQ

**GitHub Task:**
```bash
git add projects/02-cloud-pipeline/bi_queries.sql
git commit -m "📊 BI queries and Natural Language support"
```

**Příští týden:** ML operations a RAG!

---

#### Týden 15: MLflow, RAG, a AI Operations

**Hlavní témata:**
- MLflow: Experiment tracking, model registry
- RAG (Retrieval Augmented Generation) s daty
- Feature stores
- Model deployment

**Učební cíle:**
- [ ] Znám MLflow workflow
- [ ] Umím buildovat RAG pipeline
- [ ] Vím, jak deployovat ML modely
- [ ] Rozumím feature stores

**Praktika:**
```python
# MLflow: Experiment tracking

import mlflow
from sklearn.ensemble import RandomForestRegressor

mlflow.start_run()

# Hyperparameters
n_estimators = 100
max_depth = 10

# Train model
model = RandomForestRegressor(
    n_estimators=n_estimators,
    max_depth=max_depth
)
model.fit(X_train, y_train)

# Log metrics
score = model.score(X_test, y_test)
mlflow.log_metric("r2_score", score)
mlflow.log_param("n_estimators", n_estimators)
mlflow.log_param("max_depth", max_depth)

# Log model
mlflow.sklearn.log_model(model, "random_forest_model")

mlflow.end_run()

# Všechny experimenty se trackují! (UI pro comparison)
```

```python
# RAG Pipeline: Retrieval + Generation

# 1. Data z Gold layer → embeddings
from langchain.embeddings import OpenAIEmbeddings
from langchain.vectorstores import Chroma

# Load your company data
documents = spark.sql("SELECT * FROM gold.company_knowledge_base").toPandas()

# Embed a store v vector DB
embeddings = OpenAIEmbeddings()
vectordb = Chroma.from_documents(documents, embeddings)

# 2. User query → retrieve relevant docs
query = "What is our Q3 revenue?"
relevant_docs = vectordb.similarity_search(query, k=3)

# 3. LLM s context → generate answer
from langchain.chat_models import ChatOpenAI
from langchain.prompts import PromptTemplate

prompt = PromptTemplate(
    input_variables=["context", "question"],
    template="Based on {context}, answer: {question}"
)

llm = ChatOpenAI(model="gpt-4")
answer = llm.predict(
    text=prompt.format(
        context=relevant_docs,
        question=query
    )
)

# Result: AI-generated answer based on YOUR data! (not hallucinations!)
```

**Obsidian:**
- `Learn/15-MLflow-RAG.md`
- Experiment tracking, RAG workflow

**GitHub Task:**
```bash
git add projects/03-realtime-rag/mlflow_tracking.py
git commit -m "🤖 MLflow experiments and RAG pipeline"
```

**Příští týden:** Optimalizace a streaming!

---

#### Týden 16: Pokročilé Optimalizace - Z-Order, Photon, Serverless

**Hlavní témata:**
- Z-Order indexing (clustered index)
- Photon Engine (MPP query engine)
- Predictive I/O (AI-driven optimization)
- Serverless compute (autoscaling)

**Učební cíle:**
- [ ] Vím, jak optimalizovat queries
- [ ] Znám Z-Order pattern
- [ ] Rozumím Photon Engine
- [ ] Vím, jak nastavit auto-scaling

**Praktika:**
```python
# Z-Order indexing: "Smart" clustering

# Normální: data jsou náhodně distribuovány
# Z-Order: data jsou clustered podle sloupců

spark.sql("""
    OPTIMIZE gold.fact_sales
    USING Z_ORDER BY (customer_id, order_date)
""")

# Teď query:
# "Dej mi objednávky zákazníka 123 za 2025"
# Jen prohledá "malý" cluster místo celé tabulky! ⚡

# Výsledek: Queries jsou 10-100x rychlejší!
```

```python
# Predictive I/O: Databricks AI autopilot

# Databricks vidí tvé dotazy a automaticky:
# - Clustere data
# - Optimalizuje výkon
# - Bez tvého zásahu!

# Filestore v Python:
optimized_tables = spark.sql("""
    SELECT * FROM system.statistics.table_stats
    WHERE optimization_opportunity > 0.5  -- 50% speedup možný!
""")
```

**Obsidian:**
- `Learn/16-Optimization.md`
- Z-Order, Photon, VACUUM patterns

**GitHub Task:**
```bash
git add projects/02-cloud-pipeline/optimization.sql
git commit -m "⚡ Z-Order indexing and query optimization"
```

**Příští týden:** Streaming & Real-time!

---

#### Týden 17: Streaming Data - Micro-batch, Auto Loader, Real-time ETL

**Hlavní témata:**
- Micro-batch vs True Streaming
- Auto Loader (cloud-native SFTP)
- Structured Streaming v Spark
- Real-time fact tables

**Učební cíle:**
- [ ] Znám streaming architectury
- [ ] Umím psát Spark Streaming
- [ ] Vím, jak deployovat real-time ETL
- [ ] Rozumím Event Time vs Processing Time

**Praktika:**
```python
# Auto Loader: Kontinuální ingest z cloud storage

df = spark.readStream \
    .format("cloudFiles") \
    .option("cloudFiles.format", "parquet") \
    .option("cloudFiles.schemaLocation", "/checkpoints/schema") \
    .load("/mnt/streaming-source/")

df.writeStream \
    .format("delta") \
    .outputMode("append") \
    .option("checkpointLocation", "/checkpoints/stream") \
    .table("bronze.streaming_events")

# Auto Loader automaticky:
# - Detekuje nové soubory
# - Ingestuje je
# - Trackuje progres (checkpoint)
```

```python
# Structured Streaming: Real-time transformace

events = spark.readStream.table("bronze.streaming_events")

# Group by v real-time
summary = events \
    .groupBy(
        F.window("timestamp", "5 minutes"),  # 5-minute windows
        "event_type"
    ) \
    .agg(
        F.count("*").alias("count"),
        F.avg("value").alias("avg_value")
    )

# Write real-time results
summary.writeStream \
    .format("delta") \
    .outputMode("update") \
    .option("checkpointLocation", "/checkpoints/summary") \
    .table("silver.event_summary")

# Výsledek: Každých 5 minut = nový update v tabulce!
```

**Obsidian:**
- `Learn/17-Streaming-Real-time.md`
- Micro-batch, Auto Loader, windowing

**GitHub Task:**
```bash
git add projects/03-realtime-rag/streaming_pipeline.py
git commit -m "🌊 Real-time streaming with Spark Structured Streaming"
```

**Následující fáze:** Case studies a career!

---

### FÁZE 7: CASE STUDIES, PRAKTIKA A KARIÉRA (Týdny 18-22)

#### Týden 18: Case Study - Airbnb Data Platform

**Téma:** Jak Airbnb builduje svůj data platform?

**Učební body:**
- Airbnb má **50+ PB** dat ročně
- Real-time bookings analytics
- Marketplace pricing engine
- Quality assurance pro hosts

**Architektura:**
```
Events (JS, app, server) 
  ↓ Kafka (streaming)
  ↓
Hadoop Ecosystem (HDFS, Spark, Hive)
  ↓
Real-time: Kafka → Spark Streaming → HBase
Batch: HDFS → Spark SQL → Hive
  ↓
BI: Tableau, internal tools
ML: Feature stores, models
```

**Tvůj zápis:**
- [ ] Jaké jsou hlavní data sources?
- [ ] Proč Hadoop? Teď by se možná volili Databricks...
- [ ] Jak dělají real-time (Kafka)?
- [ ] Jakou architekturu bys zvolil dnes?

**Obsidian Task:**
```
Learn/18-Case-Study-Airbnb.md
- Architecture diagram
- Key learnings
- Modern alternatives
```

---

#### Týden 19: Case Study - Uber Data & Analytics

**Téma:** Jak Uber používá data pro real-time dispatch?

**Učební body:**
- Uber generuje **13+ milionů** tripů denně
- Real-time dispatch engine
- Surge pricing
- Driver ratings, customer behavior

**Architektura:**
```
Ride requests (app)
  ↓ Real-time processing
  ↓
Kafka → Flink/Spark Streaming → Feature stores
  ↓
ML Model: Price optimization
  ↓
Decision: Assign driver, set price, route
```

**Tvůj zápis:**
- [ ] Jak se processují miliony eventů?
- [ ] Latency requirements?
- [ ] Jak se integruje ML do real-time systému?
- [ ] Data retention policies?

**Obsidian Task:**
```
Learn/19-Case-Study-Uber.md
- Real-time requirements
- ML integration
- Pricing algorithm
```

---

#### Týden 20: Praktická Cvičení - Build End-to-End Pipeline

**Projekt:** Tvůj vlastní Lakehouse pipeline

**Specifikace:**
```
1. Data ingestion: API → Bronze (Python + requests)
2. Transformation: Bronze → Silver (SQL, dbt)
3. Dimensional modeling: Silver → Gold (Star Schema)
4. BI: Queries v DatabricksSQL
5. Monitoring: Data quality checks
```

**Příklad:** Stock market data pipeline
```
API: Alpha Vantage (stock prices)
  ↓
Bronze: RAW ticker data (parquet)
  ↓
Silver: Cleaned, typed, deduplicated
  ↓
Gold: dim_stock, fact_price (Star Schema)
  ↓
BI: Daily price trends, moving averages
```

**Deliverable:**
- Python ingestion script
- SQL transformations (dbt)
- Star Schema DDL
- 5x BI queries
- Data quality checks
- README s architecture

**GitHub Task:**
```bash
git add projects/03-realtime-rag/
git commit -m "🎯 End-to-end Lakehouse pipeline: ingestion → transformation → BI"
```

---

#### Týden 21: Interview Prep - Behavioral & Technical

**Technické otázky:**
```
1. "Design a data pipeline for 1 billion events/day"
   - Odpověď: Medallion arch, auto-loader, Delta, Databricks
   
2. "Dimenzionální model pro e-commerce"
   - fact_orders, dim_date, dim_customer, dim_product
   - SCD Type 2 pro products
   
3. "Jak optimalizujete slow query?"
   - EXPLAIN PLAN, Z-Order, VACUUM, partitioning
   
4. "Star vs Snowflake Schema?"
   - Star: denormalizovaná, rychlá, redundance
   - Snowflake: normalizovaná, modulární, více joinů
```

**Behavioral:**
```
1. "Tell me about your biggest challenge"
2. "How do you handle pressure?"
3. "Give an example of collaboration"
4. "Biggest mistake? What did you learn?"
```

**Obsidian:**
```
Docs/Interview-Prep.md
- Technical Q&A
- System design templates
- Behavioral frameworks
```

---

#### Týden 22: Shrnutí, Certifikace a Career Plan

**Co jste se naučili:**
- ✅ Datové modelování (Star, Snowflake, Vault)
- ✅ Lakehouse architecture (Bronze-Silver-Gold)
- ✅ ETL/ELT orchestrace (Airflow)
- ✅ Data quality a governance
- ✅ Real-time streaming
- ✅ BI a AI integration

**Portfolio na GitHub:**
- ✅ 5+ projektů
- ✅ 300+ commitů
- ✅ Komplexní architektura
- ✅ Professional README

**Career Options:**
```
Option 1: Junior Data Engineer (55-70k CZK)
- Budete dělat ETL/ELT pipelines
- Maintenance existujících modelů
- Data quality monitoring

Option 2: Analytics Engineer (60-75k CZK)
- dbt focus
- SQL optimization
- BI ad-hoc reporty

Option 3: Python/Data Platform Engineer (70-85k CZK)
- More coding (Python/Scala)
- Infrastructure
- Performance optimization

Option 4: Specialization (6-12 měsíců)
- Streaming Engineer (Kafka, Flink)
- ML Engineer (feature stores, models)
- Data Architect (design systems)
```

**Certifikace doporučená:**
- Databricks Certified Data Engineer
- AWS Certified Data Analytics
- dbt Fundamentals

**LinkedIn Profile:**
- 300+ connections
- 20+ posts o learningi
- 5 case studies
- 10+ recommendations (doufáme!)

---

## 📊 POROVNÁNÍ: 23-TÝDENNÍ vs 22-TÝDENNÍ PLÁN

| Aspekt | Originální (23 týdnů) | Pokročilý (22 týdnů) |
|--------|----------------------|----------------------|
| **Fundamenty** | Týdny 1-8 | Týdny 1-2 |
| **Python & SQL** | Týdny 6-9 | Integrováno |
| **Cloud (GCP)** | Týdny 11-16 | Týdny 10-13 (AWS/Azure/GCP) |
| **Modelování** | Základy v 16 | Hluboko v 3-9 |
| **Lakehouse** | Jenom zmínka | Fáze 3-4 |
| **Real-time** | Project 3 | Týden 17 |
| **AI/ML** | Bonus | Fáze 6 |
| **Career** | Zmínka | Týden 22 |

**Zvolte si:**
- **Originální**: Если chcete základy + time na práci
- **Pokročilý**: Pokud chcete enterprise-ready znalosti

---

## ✅ CHECKLIST: Co máte?

- [x] 22-týdenní plán
- [x] Vědomosti: Star/Snowflake/Vault
- [x] Lakehouse Medallion Architecture
- [x] ETL/ELT orchestrace
- [x] Real-time streaming
- [x] BI & AI integration
- [x] Cloud comparison
- [x] Case studies
- [x] Interview prep
- [x] Career guidance

**Teď jen IMPLEMENTUJTE!** 🚀

---

**Poslední slova:**
Tento plán je vaši "zkušební skála" k datovému inženýrství. Není teoretický - je praktický, foundation-first, a enterprise-ready. Do března 2026 budete mít skills, které si IT firmy velmi ceňují.

**Začněte DNES. Commitujte DENNĚ. Na březen budete READY!** 💪
