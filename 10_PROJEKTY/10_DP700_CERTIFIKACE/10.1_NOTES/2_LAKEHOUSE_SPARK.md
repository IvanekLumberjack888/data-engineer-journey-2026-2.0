# 2️⃣ LAKEHOUSE & SPARK

**Cíl:** Pochopit Lakehouse architekturu a PySpark transformace

---

## 📖 TEORIE

### Lakehouse Architecture

Hybrid mezi Data Lake a Data Warehouse.

**Struktura:**
```
Lakehouse/
├── Files/          ← Raw unstructured data
│   ├── raw/
│   ├── bronze/
│   └── staging/
└── Tables/         ← Structured Delta tables
    ├── bronze/
    ├── silver/
    └── gold/
```

**Files folder:**
- Unstructured data (CSV, JSON, images, videos)
- No schema enforcement
- Direct Spark access

**Tables folder:**
- Delta Lake tables
- Schema enforced
- SQL + Spark access
- ACID transactions

---

### Apache Spark

Distributed computing engine pro big data.

**Key Concepts:**

**1. Lazy Evaluation**
```python
# Tyto operace se NEPROVEDOU hned:
df.filter(col("age") > 18)   # Transformation
df.select("name", "city")     # Transformation
df.groupBy("city").count()    # Transformation

# TEĎ se provede všechno:
df.show()  # Action - triggers execution
```

**2. Actions vs Transformations**
- **Transformations** (lazy): filter, select, join, groupBy
- **Actions** (execute): show, count, write, collect

**3. DataFrames**
```python
# Read data
df = spark.read.format("csv")\
    .option("header", "true")\
    .load("Files/raw/data.csv")

# Transform
df_clean = df.filter(col("age") > 18)\
    .select("name", "age", "city")

# Write
df_clean.write.format("delta")\
    .mode("overwrite")\
    .saveAsTable("silver.customers")
```

---

### PySpark Common Operations

**Read:**
```python
# CSV
df = spark.read.csv("Files/data.csv", header=True)

# Delta
df = spark.read.table("silver.sales")

# Parquet
df = spark.read.parquet("Files/data.parquet")
```

**Transform:**
```python
# Filter
df.filter(col("revenue") > 1000)

# Select columns
df.select("customer_id", "revenue", "date")

# Rename
df.withColumnRenamed("old_name", "new_name")

# Add column
df.withColumn("year", year(col("date")))

# Group & aggregate
df.groupBy("category")\
  .agg(sum("revenue").alias("total"))
```

**Write:**
```python
# To Delta table
df.write.format("delta")\
    .mode("overwrite")\
    .saveAsTable("gold.sales_summary")

# Modes: overwrite, append, ignore, error
```

---

### OneLake Shortcuts

Virtual links k external data.

**Use cases:**
- Link to Azure Blob Storage
- Link to AWS S3
- Link to another Lakehouse
- Avoid data duplication

**Vytvoření:**
1. Lakehouse → Files → New shortcut
2. Vyber source (Azure, AWS, OneLake)
3. Zadej credentials + path

---

## 🔑 Key Bullet Points (EN)

- Apache Lakehouse is hybrid architecture combining Data Lake flexibility with Data Warehouse structure, enabling both Spark compute and SQL query access
- Lakehouse separates Files (raw unstructured data) from Tables (structured Delta format), allowing gradual transformation from bronze to gold layers
- Apache Spark uses lazy evaluation - transformations are queued but only executed when action is called, optimizing resource usage
- PySpark DataFrame API provides SQL-like interface for distributed data processing with native support for complex transformations and aggregations
- OneLake integration enables shared data access across all Fabric experiences through same logical lakehouse

---

## ❓ DP-700 Exam Questions (EN)

**Q1.** You are designing data ingestion pipeline. Users need both SQL and Spark access to same dataset without duplication. Which component enables this?

**Q2.** A data engineering team compares performance between querying raw Parquet files and Delta Lake tables. Why would Delta be faster?

**Q3.** You have PySpark code with 10 sequential steps (select, filter, groupBy). Nothing happens until you call `.show()`. What is this behavior?

**Q4.** Your team implements medallion architecture in Lakehouse. Which component stores each Bronze/Silver/Gold layer?

**Q5.** PySpark notebook consumes too much memory. Many transformations chained together. What optimization technique helps?

---

## ✅ Checklist: Co musím umět (CZ)

- [x] Pochopit rozdíl mezi Files (raw) a Tables (Delta)
- [x] Vysvětlit proč je Lakehouse lepší než separátní Lake + Warehouse
- [x] Napsat základní PySpark: read, select, filter, groupBy, write
- [x] Rozlišit lazy evaluation vs actions
- [x] Implementovat OneLake shortcuts
- [x] Chápat roli Spark compute engine v architektuře
- [x] Prakticky vytvořit lakehouse s Files + Tables

---

## 🔗 Linky

- **Praxe:** [[10.2_LABS/1_LAB_LAKEHOUSE|Lab 1: Lakehouse]] + [[10.2_LABS/2_LAB_SPARK|Lab 2: Spark]]
- **Následující:** [[3_DELTA_LAKE|Note 3: Delta Lake]]
- **Zpět:** [[1_FABRIC_ARCHITEKTURA|Note 1]]
- **Index:** [[10_INDEX|Zpět na index]]

---

## NEXT → [[3_DELTA_LAKE|3️⃣ Delta Lake]]
