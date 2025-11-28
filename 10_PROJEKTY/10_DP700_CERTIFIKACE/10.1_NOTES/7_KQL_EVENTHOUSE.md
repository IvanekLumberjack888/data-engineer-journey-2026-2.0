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

**Operátory:**
- `take 10` — First 10 rows
- `where` — Filter
- `project` — Select columns
- `summarize` — Aggregate
- `group by` — Grouping
- `sort by` — Ordering
- `join` — Table join

### Temporal Windows

Agregace dat do time buckets.

**Typy:**
- Tumbling (non-overlapping)
- Sliding (overlapping)
- Session (event-based)
- Hopping (customizable)

**Příklad:**
```kql
BikeData
| summarize Bikes = sum(bike_count) by bin(timestamp, 5m)
```

### Materialized Views

Persistované query rezultáty.

**Výhody:**
- Předpočítané agregace
- Více dotazů na stejné data
- Backfill (naplnění historickými daty)

### Stored Functions

Reusable KQL dotazy s parametry.

```kql
.create function BikesInRegion(region_name: string) {
  BikeData
  | where region == region_name
  | summarize count() by station_id
}
```

---

## 7️⃣ KQL & EVENTHOUSE

**Cíl:** Pochopit KQL syntax a Eventhouse pro real-time analytics

### 🔑 3-5 Key Bullet Points (EN)

- KQL (Kusto Query Language) is designed specifically for time-series and event data with native support for filtering, aggregation, and pattern detection optimized for logs and metrics
- Eventhouse in Fabric is the specialized database optimized for real-time analytics, built on Kusto technology, with automatic retention policies and streaming ingestion
- KQL queries use pipe-based syntax (`| filter | summarize | project`) enabling operator chaining for complex transformations more efficiently than SQL
- Temporal operators in KQL (`between`, `ago`, `range`) enable easy time-window queries without complex date arithmetic, critical for monitoring scenarios
- Retention policies in Eventhouse automatically age out old data, balancing storage costs with historical data availability for compliance

### ❓ 5 DP-700 Style Exam Questions (EN)

1. You need to find all error events from last 7 days where response time exceeded 1 second. Would KQL be better than SQL, and why?

2. A KQL query aggregates 100 billion rows but takes 30 seconds. You need sub-second response. Which KQL feature would help most?

3. Your application logs 50 GB of events daily. Eventhouse retention is 30 days. How much storage should you budget?

4. You are migrating Application Insights to Fabric Eventhouse. What data format changes are required?

5. Your KQL query uses `summarize` over 1 billion rows to calculate percentiles. Should you use `percentiles_approx()` or `percentiles()`?

### ✅ Checklist: Co musím umět (CZ)

- ✅ Napsat KQL query s filter, project, summarize
- ✅ Používat temporal operátory (ago, between, range)
- ✅ Vytvořit materialized views v Eventhouse
- ✅ Pochopit partitioning pro optimalizaci
- ✅ Konfigurovat retention policies
- ✅ Implementovat alerting na KQL query
- ✅ Debugovat performance problémů v KQL

### 🔗 Linky
- Praxe: [[7_LAB_SECURITY|Lab 7: Security & RBAC]]
- Následující: [[8_WAREHOUSE_SQL|Note 8: Warehouse & SQL]]
- Zpět: [[6_REAL_TIME|Note 6: Real-Time Intelligence]]

---

## NEXT → [[8_WAREHOUSE_SQL]]