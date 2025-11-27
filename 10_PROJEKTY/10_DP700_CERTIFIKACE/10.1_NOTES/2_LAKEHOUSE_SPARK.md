## 2️⃣ LAKEHOUSE & SPARK

**Cíl:** Pochopit Lakehouse a PySpark pro transformace

### 🔑 3-5 Key Bullet Points (EN)

- Apache Lakehouse is a hybrid architecture combining Data Lake flexibility with Data Warehouse structure, enabling both Spark compute and SQL query access on Delta Lake tables
- Lakehouse separates Files (raw unstructured data) from Tables (structured Delta format), allowing gradual transformation from bronze to gold layers
- Apache Spark is a distributed computing engine with lazy evaluation - transformations are queued but only executed when an action is called, optimizing resource usage
- PySpark DataFrame API provides SQL-like interface for distributed data processing with native support for complex transformations, aggregations, and machine learning
- OneLake integration with Fabric Lakehouse enables shared data access across all Fabric experiences (Data Engineering, Warehouse, Power BI) through the same logical lakehouse

### ❓ 5 DP-700 Style Exam Questions (EN)

1. You are designing a data ingestion pipeline in Microsoft Fabric. Users need both SQL and Spark access to the same dataset without duplication. Which Fabric component enables this shared access model?

2. A data engineering team is comparing performance between querying raw Parquet files and Delta Lake tables in a lakehouse. Why would the Delta Lake queries be faster in most scenarios?

3. You have written a PySpark transformation with 10 sequential steps (select, filter, groupBy, etc.). However, when you run the code, nothing happens until you call `.show()`. What is this behavior called in Spark?

4. Your team needs to implement a medallion architecture (Bronze/Silver/Gold) in Fabric Lakehouse. Which component of the Lakehouse structure would you use to store each layer?

5. You are troubleshooting why a PySpark notebook job is consuming more memory than expected. You notice there are many transformations chained together. What Spark optimization technique could help reduce memory pressure?

### ✅ Checklist: Co musím umět (CZ)

- ✅ Pochopit rozdíl mezi Files folder (raw) a Tables folder (Delta structured)
- ✅ Vysvětlit, proč je Lakehouse lepší než separátní Lake + Warehouse
- ✅ Napsat základní PySpark kód: read, select, filter, groupBy, write
- ✅ Rozlišit lazy evaluation a kdy se transformace skutečně provedou (actions)
- ✅ Implementovat OneLake shortcuts pro sdílená data
- ✅ Chápat roli Spark compute engine v architektuře
- ✅ Prakticky vytvořit lakehouse s Files + Tables strukturou

### 🔗 Linky
- Praxe: [[2_LAB_SPARK|Lab 2: Spark Notebook]]
- Následující: [[3_DELTA_LAKE|Note 3: Delta Lake]]
- Zpět: [[1_FABRIC_ARCHITEKTURA|Note 1: Fabric Architektura]]

---