# 3️⃣ DELTA LAKE

**Cíl:** ACID transactions, time travel, optimizace

---

## 📖 TEORIE

### Co je Delta Lake?

Open-source storage format s ACID properties.

**ACID:**
- **A**tomicity — All or nothing
- **C**onsistency — Valid state
- **I**solation — No dirty reads
- **D**urability — Persisted

### Key Features

**Time Travel:**
```sql
SELECT * FROM table TIMESTAMP AS OF '2025-11-17'
SELECT * FROM table VERSION AS OF 0
```

**Schema Evolution:**
- Adding columns
- Renaming columns
- Nullable changes

**Transactions:**
- Multi-part writes
- Rollback support
- Conflict resolution

### Optimizace

**VACUUM** — Remove old files:
```sql
VACUUM table_name
```

**OPTIMIZE** — Compact files:
```sql
OPTIMIZE table_name
```

**Z-order** — Clustered index:
```sql
OPTIMIZE table_name ZORDER BY (col1, col2)
```

---

## 🛠️ PRAXE

- [ ] Create Delta table
- [ ] Insert data (transactional)
- [ ] Update rows
- [ ] Delete rows
- [ ] Time travel query (old version)
- [ ] OPTIMIZE table
- [ ] Check transaction log
- [ ] Schema evolution test

---

## 🔗 INTERNÍ LINKY

- Back: [[2_LAKEHOUSE_SPARK]]
- Next: [[4_DATAFLOW_PIPELINE]]
- Praxe: [[3_LAB_DATAFLOW]]
- Resources: [[SQL_SCRIPTS.md]]

---

## 🔗 EXTERNÍ LINKY

- Delta Lake Docs: https://docs.delta.io
- ACID Transactions: https://docs.delta.io/latest/delta-transactions.html
- Time Travel: https://docs.delta.io/latest/delta-utility.html
- Learn Path: https://learn.microsoft.com/en-us/training/modules/analyze-data-delta-lake/

---
## NEXT -> [[4_DATAFLOW_PIPELINE]]