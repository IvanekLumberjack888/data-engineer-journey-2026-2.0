# 5️⃣ MEDALLION ARCHITEKTURA

**Cíl:** Data organization best practice

---

## 📖 TEORIE

### Tři vrstvy

**Bronze (Raw):**
- Kopie source dat
- Žádné transformace
- Minimální čistění
- Audit trail

**Silver (Cleansed):**
- Data quality checks
- Deduplikace
- Format standardizace
- Joins & enrichment
- Ready for analytics

**Gold (Business):**
- Aggregované metriky
- Business logic
- Denormalizované
- Performance optimized
- Dashboard ready

### Implementace

**Storage:**
```
lakehouse/
├── bronze/  (raw)
├── silver/  (cleaned)
└── gold/    (aggregated)
```

**Processing:**
- Bronze → Silver (ETL)
- Silver → Gold (Transformation)

### Výhody

- Data lineage jasný
- Quality gates
- Performance
- Scalability
- Governance

---

## 5️⃣ MEDALLION ARCHITEKTURA

**Cíl:** Pochopit 3-vrstvou architekturu: Bronze → Silver → Gold

### 🔑 3-5 Key Bullet Points (EN)

- Medallion architecture defines three layers: Bronze (raw ingested data as-is), Silver (cleaned, deduplicated, validated), and Gold (business-ready aggregations)
- Bronze layer receives all raw data with minimal transformation, serving as immutable data archive and audit trail for compliance and debugging
- Silver layer applies data quality rules, deduplication, joins reference data, and standardizes formats, creating trusted source for analytics
- Gold layer contains business-specific aggregations, dimensional tables, and fact tables optimized for specific use cases (reporting, ML, dashboards, APIs)
- Each layer can use different storage formats and partitioning strategies - Bronze typically uses raw files, Silver uses Delta tables, Gold uses optimized dimensional structures

### ❓ 5 DP-700 Style Exam Questions (EN)

1. Your data pipeline ingests 10 million JSON records daily with some missing fields and unexpected data types. Which medallion layer should apply cleansing?

2. You are building a real-time dashboard showing sales by region and product. Raw source has 50 columns but dashboard needs 5. Which layer would you query?

3. A compliance audit requires proving what data was ingested 6 months ago, including errors. Which medallion layer would you use?

4. Your organization has two use cases: (A) HR dashboard and (B) Supply chain ML model, both needing cleaned data but different aggregations. How to handle this?

5. Your Bronze layer receives 100GB daily, but only 5GB survives deduplication in Silver. Is this normal? Which layer is responsible?

### ✅ Checklist: Co musím umět (CZ)

- ✅ Pochopit 3-vrstvou architekturu: Bronze → Silver → Gold
- ✅ Definovat odpovědnost každé vrstvy
- ✅ Implementovat Bronze vrstvu s minimálními transformacemi
- ✅ Aplikovat data quality v Silver vrstvě
- ✅ Vytvořit Gold vrstvu optimalizovanou pro use cases
- ✅ Designovat partitioning strategii pro každou vrstvu
- ✅ Implementovat UPSERT/SCD logiku v Silver a Gold

### 🔗 Linky
- Praxe: [[5_LAB_EVENTSTREAM|Lab 5: Eventstream]]
- Následující: [[6_REAL_TIME|Note 6: Real-Time Intelligence]]
- Zpět: [[4_DATAFLOW_PIPELINE|Note 4: Dataflow & Pipeline]]

---