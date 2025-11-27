# 4️⃣ DATAFLOW & PIPELINE

**Cíl:** ETL/ELT orchestration

---

## 📖 TEORIE

### Dataflow Gen2 (Power Query Online)

ETL transformation tool.

**Workflow:**
1. Source (data import)
2. Transform (Power Query)
3. Destination (load)

**Transformace:**
- Column operations
- Merge queries
- Group & aggregate
- Custom formulas
- Error handling

### Data Pipeline

Orchestration engine.

**Komponenty:**
- Activities (jobs)
- Control flow (if/for)
- Error handling
- Scheduling

**Activity Types:**
- Copy data
- Dataflow
- Spark job
- Notebook
- SQL query
- Python script

### ETL vs ELT

**ETL:**
- Transform before load
- Slower (transform first)
- Better for warehouses

**ELT:**
- Load then transform
- Faster (load raw)
- Better for lakes

---

## 4️⃣ DATAFLOW & PIPELINE

**Cíl:** Pochopit Data Factory pipelines a Dataflow Gen2 orchestraci

### 🔑 3-5 Key Bullet Points (EN)

- Data Factory Pipelines orchestrate complex ETL workflows with support for activities like Copy, Dataflow, Spark notebook, and SQL script execution with conditional branching and error handling
- Dataflow Gen2 provides visual Power Query interface for data transformation without coding, supporting data source connections, filters, joins, and aggregations with automatic optimization
- Dataflow can be scheduled, triggered on-demand, or integrated with notebooks and warehouses for downstream processing of refined data
- Pipeline variables and parameters enable dynamic workflow configuration (connection strings, file paths, table names) without hardcoding values
- Activity dependencies and control flow (success, failure, completion paths) enable sophisticated orchestration patterns including error handling, retries, and conditional execution

### ❓ 5 DP-700 Style Exam Questions (EN)

1. You need to transform 100GB of CSV data weekly with 20 transformation steps. Would you recommend Dataflow Gen2 or a Spark notebook, and why?

2. A Data Factory Pipeline runs a Dataflow at 2 AM daily, but it randomly fails. You need to automatically retry it 3 times before alerting. Which pipeline feature enables this?

3. Your ETL pipeline needs to load different files depending on weekday or weekend. Which pipeline component handles conditional logic?

4. You are building a pipeline that loads data from Azure Blob Storage to a Lakehouse table. The source file path changes monthly. How would you make this dynamic?

5. Your team has a legacy SSIS package to migrate to Fabric with minimal code changes. Should you use Dataflow Gen2 or Python notebook, and why?

### ✅ Checklist: Co musím umět (CZ)

- ✅ Vytvořit jednoduchou pipeline: source → transform → sink
- ✅ Nakonfigurovat Dataflow Gen2 s Power Query transformacemi
- ✅ Nastavit aktivační podmínky (schedule, manual, event-based)
- ✅ Implementovat error handling s retry logikou
- ✅ Používat pipeline variables pro dynamické hodnoty
- ✅ Propojit pipeline s notebookem/warehouse
- ✅ Monitorit pipeline runs a debugovat chyby

### 🔗 Linky
- Praxe: [[4_LAB_WAREHOUSE|Lab 4: Warehouse]]
- Následující: [[5_MEDALLION_ARCHITEKTURA|Note 5: Medallion Architektura]]
- Zpět: [[3_DELTA_LAKE|Note 3: Delta Lake]]

---