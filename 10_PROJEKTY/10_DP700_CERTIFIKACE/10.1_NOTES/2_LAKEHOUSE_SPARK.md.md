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
