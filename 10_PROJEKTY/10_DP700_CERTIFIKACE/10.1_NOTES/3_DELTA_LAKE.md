# 3️⃣ DELTA LAKE

**Cíl:** Pochopit Delta Lake, ACID transactions, time-travel

---

## 📖 TEORIE

### Delta Lake Format

Open-source storage layer built on Parquet.

**Features:**
- ACID transactions
- Schema enforcement
- Time-travel
- UPSERT support
- Z-ordering optimization

**Architektura:**
```
delta_table/
├── _delta_log/          ← Transaction log
│   ├── 00000.json
│   └── 00001.json
└── part-*.parquet       ← Data files
```

---

### ACID Transactions

**Atomicity** — All or nothing (transaction buď celá nebo vůbec)  
**Consistency** — Data vždy v konzistentním stavu  
**Isolation** — Concurrent reads/writes se neovlivňují  
**Durability** — Committed data = permanently stored

**Příklad:**
```python
# Failed write WON'T corrupt table
df.write.format("delta").mode("append").save("Tables/sales")
# If this fails midway, previous state remains intact
```

---

### Time-Travel

Query historical versions of table.

**By version:**
```python
df = spark.read.format("delta")\
    .option("versionAsOf", 5)\
    .load("Tables/sales")
```

**By timestamp:**
```python
df = spark.read.format("delta")\
    .option("timestampAsOf", "2025-01-01")\
    .load("Tables/sales")
```

**View history:**
```sql
DESCRIBE HISTORY sales
```

---

### Schema Enforcement

Rejects writes that don't match schema.

**Example:**
```python
# Table schema: (id INT, name STRING, age INT)
# This WILL FAIL:
df_wrong = spark.createDataFrame([(1, "John", "thirty")])
df_wrong.write.format("delta").mode("append").save("Tables/users")
# ERROR: age must be INT, not STRING
```

**Schema evolution:**
```python
# Allow new columns
df.write.format("delta")\
    .mode("append")\
    .option("mergeSchema", "true")\
    .save("Tables/users")
```

---

### UPSERT (MERGE)

Update existing + Insert new records.

```python
from delta.tables import DeltaTable

deltaTable = DeltaTable.forPath(spark, "Tables/users")

deltaTable.alias("target").merge(
    updates.alias("source"),
    "target.id = source.id"
).whenMatchedUpdate(set = {
    "name": "source.name",
    "age": "source.age"
}).whenNotMatchedInsert(values = {
    "id": "source.id",
    "name": "source.name",
    "age": "source.age"
}).execute()
```

---

### Z-Ordering

Physical data organization for query optimization.

**Use case:** Frequent filtering on specific columns

```sql
OPTIMIZE sales ZORDER BY (customer_id, date)
```

**Benefit:** Reduces files scanned → faster queries

---

### VACUUM

Clean up old data files.

```sql
-- Remove files older than 7 days
VACUUM sales RETAIN 168 HOURS
```

**Warning:** Can't time-travel past VACUUM retention!

---

## 🔑 Key Bullet Points (EN)

- Delta Lake is open-source storage format built on Parquet that adds ACID transaction support, schema enforcement, and time-travel capabilities
- ACID transactions ensure data reliability even during concurrent reads/writes, preventing data corruption from failed writes
- Schema enforcement prevents accidental data type mismatches or unexpected column changes, automatically rejecting writes that violate schema
- Time-travel allows querying historical versions using `@version` or `@timestamp` syntax, enabling data lineage tracking and rollback
- Z-ordering optimizes query performance by physically organizing data for frequently filtered columns, dramatically reducing scan times

---

## ❓ DP-700 Exam Questions (EN)

**Q1.** A write operation fails midway. Some records written, others not. What Delta feature prevents table corruption?

**Q2.** Your team debugs data quality issue and needs to see table state 3 days ago. Which Delta feature enables this?

**Q3.** You load new data into existing Delta table, but schema changed (new column). Delta rejects write. Which feature prevents this?

**Q4.** Your table has 1M records with frequent queries filtering by `customer_id`. Performance degrades. Which optimization helps most?

**Q5.** You need slowly-changing dimension (SCD Type 2) in Delta Lake. Which feature allows tracking historical changes efficiently?

---

## ✅ Checklist: Co musím umět (CZ)

- [ ] Definovat ACID transactions a proč jsou důležité
- [ ] Vysvětlit schema enforcement
- [ ] Použít time-travel syntax pro historická data
- [ ] Aplikovat Z-ordering pro query optimization
- [ ] Pochopit versionování tabulky
- [ ] Implementovat UPSERT operace
- [ ] Monitorit table cleanup s VACUUM a OPTIMIZE

---

## 🔗 Linky

- **Praxe:** [[10.2_LABS/2_LAB_SPARK|Lab 2: Spark Notebook]]
- **Následující:** [[4_DATAFLOW_PIPELINE|Note 4: Dataflow & Pipeline]]
- **Zpět:** [[2_LAKEHOUSE_SPARK|Note 2]]
- **Index:** [[10_INDEX|Zpět na index]]

---

## NEXT → [[4_DATAFLOW_PIPELINE|4️⃣ Dataflow & Pipeline]]
