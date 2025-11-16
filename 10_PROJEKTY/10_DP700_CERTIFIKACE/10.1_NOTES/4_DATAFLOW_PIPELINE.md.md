# 4️⃣ DATAFLOW & PIPELINE

## Teorie

### Dataflow Gen2

Cloud-based ETL tool (drag-and-drop transformations).

**Power Query Online interface:**
- Visual, no-code transformations
- Connect to 500+ data sources
- Schedule refreshes

**Transformations dostupné:**
- Filter (WHERE clause)
- Group by (aggregations)
- Merge (JOINs)
- Append (UNION)
- Pivot/Unpivot
- Split column
- Replace values
- Custom formulas

**Output:** Can load to:
- Lakehouse (Tables or Files)
- Warehouse
- Azure Data Lake
- etc.

### Pipeline (Data Factory)

Orchestration tool pro scheduling a koordinaci.

**Activities:**
- Copy data (one-time or scheduled)
- Run Dataflow (trigger transformation)
- Run notebook (Spark code)
- Run SQL script
- Wait (sleep)
- If/else conditions
- Loop (for each)
- itd.

**Flow control:**
```
Start → Copy data → Run Dataflow → Run Notebook → End
         ├─ Success → notify
         └─ Error → retry
```

### ETL vs ELT

**ETL (Extract, Transform, Load):**
1. Extract (get source data)
2. **Transform** (clean, aggregate, combine)
3. Load (to warehouse)

**ELT (Extract, Load, Transform):**
1. Extract (get source data)
2. Load (raw to lake)
3. **Transform** (in place, with SQL/Spark)

**Fabric approach:** Hybrid
- Load raw to Files (ELT part)
- Transform with Spark/SQL in Lakehouse (Transform part)
- Load clean to Warehouse or BI

### Scheduled refresh vs Pipeline

| Aspect | Dataflow refresh | Pipeline |
|--------|------------------|----------|
| **Trigger** | On schedule | On schedule + manual |
| **Complexity** | Single Dataflow | Multiple activities, logic |
| **Parallelism** | Sequential | Can run in parallel |
| **Use case** | Simple loads | Complex orchestration |

---

## Praxe

**Part 1: Dataflow Gen2**
- [ ] Create Dataflow
  - New item → Dataflow Gen2
- [ ] Connect to data source (CSV, API, SQL, etc.)
- [ ] Add transformations
  - Filter
  - Group by (aggregation)
  - Merge (JOIN)
- [ ] Set destination (Lakehouse table)
- [ ] Save & Refresh
- [ ] Check results

**Part 2: Pipeline**
- [ ] Create Pipeline
  - New item → Data pipeline
- [ ] Add activities
  - Copy data activity
  - Run Dataflow activity
  - Run notebook activity
- [ ] Connect activities (success/failure paths)
- [ ] Set schedule (daily, weekly, etc.)
- [ ] Test run

---

## Otázky

- Jaký je max refresh frequency v Dataflow?
- Jak se pipeline triggery stackují (co když běží dlouhodoběěžně)?

---

## Key Takeaways

1. **Dataflow** = No-code ETL (Power Query)
2. **Pipeline** = Orchestration engine (scheduling + logic)
3. **ETL vs ELT** = Transform before/after loading
4. **Fabric hybrid** = Load raw (ELT) + Transform (T)

---

## Next: [[5_MEDALLION_ARCHITEKTURA|5. Medallion Architektura]]