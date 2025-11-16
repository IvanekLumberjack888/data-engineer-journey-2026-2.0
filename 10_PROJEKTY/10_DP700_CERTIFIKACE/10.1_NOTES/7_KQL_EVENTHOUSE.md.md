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

- `take 10` — First 10 rows
    
- `where` — Filter
    
- `project` — Select columns
    
- `summarize` — Aggregate
    
- `group by` — Grouping
    
- `sort by` — Ordering
    
- `join` — Table join
    

## Temporal Windows

Agregace dat do time buckets.

**Typy:**

- Tumbling (non-overlapping)
    
- Sliding (overlapping)
    
- Session (event-based)
    
- Hopping (customizable)
    

**Příklad:**
