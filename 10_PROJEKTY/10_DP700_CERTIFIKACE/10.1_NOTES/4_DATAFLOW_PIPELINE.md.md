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

## 🛠️ PRAXE

- [ ] Create Dataflow
- [ ] Add CSV source
- [ ] Add transformations
- [ ] Set destination
- [ ] Create Pipeline
- [ ] Add Dataflow activity
- [ ] Schedule pipeline
- [ ] Monitor execution

---

## 🔗 INTERNÍ LINKY

- Back: [[3_DELTA_LAKE.md]]
- Next: [[5_MEDALLION_ARCHITEKTURA.md]]
- Praxe: [[3_LAB_DATAFLOW.md]]
- Cheatsheet: [[30_ZDROJE/EXTERNÍ_LINKY]]

---

## 🔗 EXTERNÍ LINKY

- Dataflow Gen2: https://learn.microsoft.com/power-query/dataflows/dataflows-overview
- Pipelines: https://learn.microsoft.com/fabric/data-factory/create-your-first-pipeline
- ETL vs ELT: https://learn.microsoft.com/fabric/data-engineering/star-schema-vs-medallion

---
## NEXT -> [[5_MEDALLION_ARCHITEKTURA.md]]