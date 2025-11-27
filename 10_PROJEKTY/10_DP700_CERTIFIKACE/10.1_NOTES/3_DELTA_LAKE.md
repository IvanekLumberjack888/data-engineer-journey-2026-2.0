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

## 3️⃣ DELTA LAKE

**Cíl:** Pochopit Delta Lake, ACID transactions, time-travel

### 🔑 3-5 Key Bullet Points (EN)

- Delta Lake is an open-source storage format built on Parquet that adds ACID transaction support, schema enforcement, and time-travel capabilities to data lakes
- ACID transactions (Atomicity, Consistency, Isolation, Durability) ensure data reliability even during concurrent reads/writes, preventing data corruption from failed writes
- Schema enforcement prevents accidental data type mismatches or unexpected column changes, automatically rejecting writes that violate the defined schema
- Time-travel functionality allows querying historical versions of a table using `@timestamp` or `@version` syntax, enabling data lineage tracking and rollback capabilities
- Z-ordering and liquid clustering optimize query performance by physically organizing data for frequently filtered columns, dramatically reducing scan times

### ❓ 5 DP-700 Style Exam Questions (EN)

1. A write operation in Delta Lake fails midway through. Some records are written, others are not. What Delta Lake feature prevents this partial state from corrupting the table?

2. Your team is debugging a data quality issue and needs to see what the table looked like 3 days ago. Which Delta Lake feature enables this investigation?

3. You are loading new data into an existing Delta table, but the schema has slightly changed (new column added). Delta Lake rejects the write. Which Delta Lake feature is preventing this?

4. Your organization stores 1 million records and performs frequent queries filtering by `customer_id`. Performance is degrading. Which Delta Lake optimization technique would help most?

5. You need to implement a slowly-changing dimension (SCD Type 2) in Delta Lake. Which Delta Lake feature would allow you to track historical changes efficiently?

### ✅ Checklist: Co musím umět (CZ)

- ✅ Definovat ACID transactions a proč jsou důležité v data lakech
- ✅ Vysvětlit schema enforcement a ochrana proti data corruption
- ✅ Použít time-travel syntax pro historická data
- ✅ Aplikovat Z-ordering pro optimalizaci queries
- ✅ Pochopit versionování tabulky
- ✅ Implementovat UPSERT operace s Delta Lake
- ✅ Monitorit table cleanup s VACUUM a OPTIMIZE

### 🔗 Linky
- Praxe: [[3_LAB_DATAFLOW|Lab 3: Dataflow Gen2]]
- Následující: [[4_DATAFLOW_PIPELINE|Note 4: Dataflow & Pipeline]]
- Zpět: [[2_LAKEHOUSE_SPARK|Note 2: Lakehouse & Spark]]

---