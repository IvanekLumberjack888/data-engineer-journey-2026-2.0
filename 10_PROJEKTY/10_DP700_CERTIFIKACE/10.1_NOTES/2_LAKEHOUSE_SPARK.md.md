# 2️⃣ LAKEHOUSE & SPARK

## Teorie

### Co je Lakehouse?

Kombinace **Data Lake** (flexibility, schema-on-read) + **Data Warehouse** (structure, ACID).

**Lakehouse = Lake + House = Best of both worlds**

**Data Lake (WITHOUT warehouse features):**
- ✅ Flexibility (any data format)
- ✅ Cheap storage
- ❌ Slow queries
- ❌ No transactions
- ❌ Data quality issues

**Data Warehouse:**
- ✅ Fast queries
- ✅ ACID transactions
- ✅ Quality control
- ❌ Schema-first (rigid)
- ❌ Expensive

**Lakehouse:**
- ✅ Flexibility (like lake)
- ✅ Fast queries (like warehouse)
- ✅ ACID transactions
- ✅ Cheap storage
- ✅ Data quality

### Files vs Tables

**Files (Raw data):**
- Raw CSV, Parquet, JSON, etc.
- Nesortované, bez indexů
- Use case: Raw ingestion, backups
- Slower to query
- Example: `/lakehouse_name/Files/raw_data.parquet`

**Tables (Managed data):**
- Organized, indexed, metastored
- Delta Lake format underneath
- Use case: Transformed, business-ready data
- Faster to query
- Example: SELECT * FROM sales_table

**Best practice:** 
- Raw data → Files
- Transformed data → Tables

### Delta Lake Format

Standard format pro Lakehouse tables.

**Features:**
- **ACID Transactions** — Guarantees data consistency
- **Schema Enforcement** — Checks data types
- **Time Travel** — Query data from any point in time
- **Unified Batch & Streaming** — Both works
- **Optimization** — Auto compaction

**Under the hood:**
- Parquet files + transaction log
- Metadata stored v `_delta_log/` folder

### Apache Spark

Distributed computing framework pro velké datasety.

**Spark SQL:**
```python
df = spark.sql("SELECT * FROM my_table WHERE amount > 100")
display(df)
```

**PySpark (Python API):**
```python
df = spark.read.parquet("/path/to/data.parquet")
df_filtered = df.filter(df.amount > 100)
df_filtered.write.mode("overwrite").parquet("/path/to/output")
```

**Výhody:**
- Parallel processing (400+ nodes)
- Lazy evaluation (optimized execution plans)
- RDD, DataFrame, SQL API

### Notebooks

Interactive environment pro Spark code.

**Cells:**
- Code cell (Python, SQL, Scala)
- Markdown cell (documentation)

**Magic commands:**
- `%sql` — SQL cell
- `%py` — Python cell (default)
- `%md` — Markdown cell
- `%run` — Run another notebook

**display():**
```python
display(df)  # Nice formatted output
```

vs

```python
df.show()  # Terminal-like output
```

---

## Praktika

- [ ] Create Lakehouse
  - Workspace → New item → Lakehouse
  - Name: "Sales_Lakehouse"
  - Create
- [ ] Upload sample CSV
  - Download sample data (nebo použij kterýkoliv CSV)
  - Lakehouse → Files → Upload
- [ ] Create table from CSV
  - Right-click CSV → Load to Table
- [ ] Query via SQL
  ```sql
  SELECT TOP 100 * FROM csv_table_name
  ```
- [ ] Create Notebook
  - New item → Notebook
  - Write PySpark code
  ```python
  df = spark.sql("SELECT * FROM csv_table_name")
  display(df)
  ```
- [ ] Screenshot results

---

## Otázky

- Jaký je optimální file size pro Parquet?
- Jak Delta Lake ošetřuje concurrent writes?

---

## Key Takeaways

1. **Lakehouse** = Flexibility + Performance + ACID
2. **Files** = Raw data (unstructured)
3. **Tables** = Transformed data (structured, queryable)
4. **Delta Lake** = Format with ACID, time travel, schema enforcement
5. **Spark** = Distributed processing engine
6. **Notebooks** = Interactive development environment

---
## Next: [[3_DELTA_LAKE|3. Delta Lake]]