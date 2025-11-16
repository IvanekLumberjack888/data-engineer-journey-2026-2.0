# 1️⃣ FABRIC ARCHITEKTURA

## Teorie

### Co je Microsoft Fabric?

Unified SaaS platforma pro end-to-end data analytics.

**Všechno v jednom místě:**
- Data loading (ingestion)
- Transformace (ETL/ELT)
- Data warehouse (SQL queries)
- Real-time analytics (events, streaming)
- Business intelligence (dashboards, reports)
- Machine learning (notebooks, models)

### OneLake

Jeden centrální data repository pro celou organizaci.

**Jak funguje:**
- Jeden OneLake per tenant (organization)
- Hierarchická struktura (folder-like)
- Delta Lake format (standardní)
- Všechny Fabric experiences ho sdílí
- Single source of truth

**Výhoda:** Všichni v org. mají přístup ke stejným datům, bez duplikátů

### Fabric Experiences

Různé tools pro různé role a use case:

| Experience | Primární role | Co to dělá |
|------------|---------------|-----------|
| **Data Factory** | Data Engineer, Admin | Pipelines, orchestration, scheduling |
| **Data Engineering** | Data Engineer | Lakehouse, Spark notebooks, transformace |
| **Data Warehouse** | Data Analyst, DBA | SQL queries, T-SQL, BI queries |
| **Real-Time Intelligence** | Data Engineer, Analyst | Eventstreams, KQL, real-time dashboards |
| **Power BI** | BI Developer, Analyst | Reports, dashboards, visualizations |

### Workspace

Container pro všechny Fabric items v jedné logické jednotce.

**Workspace obsahuje:**
- Lakehouses
- Warehouses
- Dataflows
- Pipelines
- Reports
- Notebooks
- Eventstreams
- itd.

**Permissions:**
- Admin (full access)
- Member (create + edit)
- Contributor (limited)
- Viewer (read-only)

### Capacity

Compute resources potřebné pro běh Fabric.

**Fabric SKUs:**
- F2 (1 CU - compute unit)
- F4 (2 CU)
- F8 (4 CU)
- F16 (8 CU)
- P1-P5 (premium - 4-32 CU)

**Co kapacita zajišťuje:**
- Refresh rates (Dataflows, pipelines)
- Query performance (SQL, KQL)
- Notebook compute (Spark)
- Real-time processing

**Auto-scale:** Opcionálně povolíš, aby se kapacita automatic scala

### Domains (Optional)

Organizační struktura pro větší organizace.

**Use case:** Rozdělení Fabric assetu po týmech/odděleních

---

## Praxe

Co dělat:

- [ ] Login do Fabric trial (https://fabric.microsoft.com)
- [ ] Create workspace (dej mu jméno "DP700-Learning")
- [ ] Prozkoumej OneLake struktura
- [ ] Klikni na každou Experience (jen se koukat, ne editovat)
- [ ] Screenshot workspace struktura
- [ ] Podívej se do Workspace settings (permissions, capacity)

---

## Otázky k vyřešení později

- Jaká je cena za Fabric per měsíc?
- Jaký je F2 vs P1 rozdíl konkrétně?
- Jak dlouho trvá trial?

---

## Key Takeaways

1. **Fabric = Unified Platform** — Data Factory + Warehouse + BI + Real-time ALL in one
2. **OneLake = Central Hub** — Všechna data na jednom místě, všichni mají přístup
3. **Experiences = Tools** — Různé nástroje pro různé lidi (data engineer, analyst, etc.)
4. **Workspace = Container** — Logické seskupení všech itemů
5. **Capacity = Resources** — Pay for compute, not storage

---

## Next: [[2_LAKEHOUSE_SPARK|2. Lakehouse & Spark]]
