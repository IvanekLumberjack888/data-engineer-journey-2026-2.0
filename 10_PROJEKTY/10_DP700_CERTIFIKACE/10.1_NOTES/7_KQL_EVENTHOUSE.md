# 7️⃣ KQL & EVENTHOUSE

**Cíl:** Psát KQL dotazy a pracovat s Eventhouses

---

## 📖 TEORIE

### KQL (Kusto Query Language)

Textový query language optimalizovaný pro time-series data.

**Syntaxe:**
```kql
Table
| where condition
| project columns
| summarize aggregates by grouping
| sort by column
```

**Základní operátory:**
- `take 10` — First 10 rows
- `where` — Filter rows
- `project` — Select columns
- `summarize` — Aggregate data
- `group by` — Grouping
- `sort by` — Ordering
- `join` — Table join

**Příklad:**
```kql
BikeData
| where timestamp > ago(1d)
| project station_id, bike_count, timestamp
| summarize TotalBikes = sum(bike_count) by station_id
| sort by TotalBikes desc
```

---

### Temporal Windows

Agregace dat do time buckets.

**Typy:**
- **Tumbling** — Non-overlapping windows (5min, 1h)
- **Sliding** — Overlapping windows (každých 30s, window 5min)
- **Session** — Event-based (gap threshold)
- **Hopping** — Customizable overlap

**Příklad:**
```kql
BikeData
| summarize Bikes = sum(bike_count) by bin(timestamp, 5m)
```

---

### Materialized Views

Persistované query rezultáty pro rychlejší opakované queries.

**Výhody:**
- Předpočítané agregace
- Více dotazů na stejné data
- Backfill (naplnění historickými daty)
- Auto-refresh při novém data ingestion

**Vytvoření:**
```kql
.create materialized-view StationSummary on table BikeData
{
  BikeData
  | summarize TotalBikes = sum(bike_count) by station_id
}
```

---

### Stored Functions

Reusable KQL dotazy s parametry.

**Vytvoření:**
```kql
.create function BikesInRegion(region_name: string) {
  BikeData
  | where region == region_name
  | summarize count() by station_id
}
```

**Použití:**
```kql
BikesInRegion("Downtown")
```

---

### Eventhouse

Fabric component pro real-time analytics.

**Features:**
- Built on Azure Data Explorer (Kusto)
- Automatic retention policies
- High-performance ingestion (millions events/sec)
- KQL native support
- Integration s Eventstream

**Retention policies:**
```kql
.alter table BikeData policy retention 
```json
{
  "SoftDeletePeriod": "30.00:00:00",
  "Recoverability": "Enabled"
}
```
```

---

## 🔑 Key Bullet Points (EN)

- KQL (Kusto Query Language) is designed specifically for time-series and event data with native support for filtering, aggregation, and pattern detection optimized for logs and metrics
- Eventhouse in Fabric is specialized database optimized for real-time analytics, built on Kusto technology, with automatic retention policies and streaming ingestion
- KQL queries use pipe-based syntax (`| filter | summarize | project`) enabling operator chaining for complex transformations more efficiently than SQL
- Temporal operators in KQL (`between`, `ago`, `range`) enable easy time-window queries without complex date arithmetic, critical for monitoring scenarios
- Retention policies in Eventhouse automatically age out old data, balancing storage costs with historical data availability for compliance

---

## ❓ DP-700 Exam Questions (EN)

**Q1.** You need to find all error events from last 7 days where response time exceeded 1 second. Would KQL be better than SQL, and why?

**Q2.** A KQL query aggregates 100 billion rows but takes 30 seconds. You need sub-second response. Which KQL feature would help most?

**Q3.** Your application logs 50 GB of events daily. Eventhouse retention is 30 days. How much storage should you budget?

**Q4.** You are migrating Application Insights to Fabric Eventhouse. What data format changes are required?

**Q5.** Your KQL query uses `summarize` over 1 billion rows to calculate percentiles. Should you use `percentiles_approx()` or `percentiles()`?

---

## ✅ Checklist: Co musím umět (CZ)

- [ ] Napsat KQL query s filter, project, summarize
- [ ] Používat temporal operátory (ago, between, range)
- [ ] Vytvořit materialized views v Eventhouse
- [ ] Pochopit partitioning pro optimalizaci
- [ ] Konfigurovat retention policies
- [ ] Implementovat alerting na KQL query
- [ ] Debugovat performance problémů v KQL
- [ ] Rozlišit kdy KQL vs SQL

---

## 🔗 Linky

- **Praxe:** [[10.2_LABS/6_LAB_KQL|Lab 6: KQL Queries]]
- **Následující:** [[8_WAREHOUSE_SQL|Note 8: Warehouse & SQL]]
- **Zpět:** [[6_REAL_TIME|Note 6: Real-Time Intelligence]]
- **Index:** [[10_INDEX|Zpět na index]]

---

## NEXT → [[8_WAREHOUSE_SQL|8️⃣ Warehouse & SQL]]
