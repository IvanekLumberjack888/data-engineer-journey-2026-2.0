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

## 🛠️ PRAXE

- [ ] Basic KQL: take, where, project
- [ ] Aggregation: summarize, group by
- [ ] Sorting: sort by asc/desc
- [ ] Joins: inner, left, right
- [ ] Temporal windows: bin()
- [ ] Create materialized view
- [ ] Create stored function
- [ ] Call function with parameters

---

## 🔗 EXTERNÍ LINKY

- KQL Documentation: https://learn.microsoft.com/en-us/kusto/query/
- KQL Tutorial: https://learn.microsoft.com/en-us/kusto/query/tutorials/learn-common-operators
- Temporal Windows: https://learn.microsoft.com/en-us/kusto/query/summarizeoperator

---

## NEXT → [[8_WAREHOUSE_SQL]]