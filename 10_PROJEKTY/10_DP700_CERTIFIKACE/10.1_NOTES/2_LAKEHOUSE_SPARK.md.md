# 2️⃣ LAKEHOUSE & SPARK

**Cíl:** Pochopit Lakehouse a PySpark pro transformace

---

## 📖 TEORIE

### Co je Lakehouse?

Hybrid mezi Data Lake (flexibilita) a Data Warehouse (struktura).

**Struktura:**
- Files folder (raw data)
- Tables folder (structured data)
- SQL Analytics endpoint (queryable)
- Spark compute engine

**Výhody:**
- Flexibilita lake + struktura warehouse
- ACID transactions (Delta Lake)
- SQL + Spark access
- Versionování

**Vztah:**
- Lakehouse → [[3_DELTA_LAKE.md]]
- Lakehouse → [[5_MEDALLION_ARCHITEKTURA.md]]

### Files vs Tables

**Files (Raw Data):**
- Fyzické soubory (CSV, Parquet, JSON)
- Bez schématu
- Není indexed
- Pomalý na queries

**Tables (Structured):**
- Delta Lake format
- Mají schéma
- Indexed
- Rychlé queries
- ACID support

### Apache Spark

Distribuovaný computing engine.

**Komponenty:**
- Driver (coordinator)
- Executors (workers)
- Spark SQL engine
- PySpark (Python API)

**Základy:**
- RDD (Resilient Distributed Dataset)
- DataFrame (tabulární data)
- Lazy evaluation
- Transformace vs Akce

### PySpark Syntax

**DataFrame create:**
```python
df = spark.read.parquet("path/to/file")
df = spark.sql("SELECT * FROM table")
```

**Transformace:**
```python
df.select("col1", "col2")
df.filter(df.age > 30)
df.groupBy("category").count()
```

**Akce:**
```python
df.show()
df.write.saveAsTable("table_name")
```

---

## 🛠️ PRAXE

Úkoly:

- [ ] Create Lakehouse (viz [[1_LAB_LAKEHOUSE.md]])
- [ ] Upload sample CSV
- [ ] Query via SQL endpoint
- [ ] Create Spark notebook
- [ ] Load DataFrame z table
- [ ] Transform data (filter, select)
- [ ] Write back to table

---

## 🔗 INTERNÍ LINKY

- Praxe: [[1_LAB_LAKEHOUSE.md]], [[2_LAB_SPARK.md]]
- Next: [[3_DELTA_LAKE.md]]
- Back: [[1_FABRIC_ARCHITEKTURA.md]]
- Resources: [[PYSPARK_KÓDY.md]]

---

## 🔗 EXTERNÍ LINKY

**Learn:**
- Lakehouse: https://learn.microsoft.com/fabric/data-engineering/create-lakehouse
- PySpark: https://spark.apache.org/docs/latest/api/python/
- Spark SQL: https://learn.microsoft.com/fabric/data-engineering/workspace-admin

**Docs:**
- Delta Lake: https://docs.delta.io/latest/quick-start.html
- PySpark API: https://spark.apache.org/docs/latest/api/python/reference/

**Videos:**
- Lakehouse Tutorial: https://www.youtube.com/results?search_query=Fabric+Lakehouse+tutorial
- PySpark Basics: https://www.youtube.com/results?search_query=PySpark+tutorial
---
## NEXT -> [[3_DELTA_LAKE.md]]