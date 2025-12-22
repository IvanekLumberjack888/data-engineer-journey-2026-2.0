# 1️⃣ FABRIC ARCHITEKTURA

**Cíl:** Pochopit základní architekturu Microsoft Fabric a OneLake

---

## 📖 TEORIE

### Microsoft Fabric

Unified SaaS analytics platform - všechno v jednom.

**Co zahrnuje:**
- Power BI (reporting)
- Data Factory (pipelines)
- Synapse (data engineering)
- Data Activator (alerting)
- Real-Time Intelligence (streaming)

**Výhody:**
- Jeden login, jeden billing
- Sdílené OneLake storage
- Integrated security
- No data duplication

---

### OneLake

Unified data lake pro celý Fabric tenant.

**Key Features:**
- Built on Azure Data Lake Storage Gen2
- Every tenant has ONE OneLake
- All Fabric workloads share same storage
- Delta Lake as native format
- Shortcuts pro external data

**Struktura:**
```
OneLake/
├── Workspace1/
│   ├── Lakehouse1/
│   │   ├── Files/
│   │   └── Tables/
│   └── Warehouse1/
└── Workspace2/
    └── Lakehouse2/
```

---

### Workspaces

Logical containers pro Fabric items.

**Workspace roles:**
- **Admin** — Full control
- **Member** — Can create items
- **Contributor** — Can edit existing items
- **Viewer** — Read-only access

**Best practices:**
- Separate workspaces per team/project
- Use Dev/Test/Prod workspaces
- Assign roles based on least privilege

---

### Capacity

Compute resource pool (billing unit).

**Capacity tiers:**
- **F2-F8** — Trial, small dev
- **F64** — Small production
- **F128-F256** — Medium production
- **F512+** — Enterprise

**Capacity Units (CU):**
- Every operation consumes CUs
- Pipeline run = 0.1 CU per GB
- Spark notebook = 1-10 CU per hour
- Query = varies

**Monitoring:**
- Capacity Metrics App
- Throttling alerts
- 14-day history

---

### Fabric Items

Co můžeš vytvořit v workspace:

- **Lakehouse** — Hybrid storage (Files + Tables)
- **Warehouse** — SQL-only analytics
- **Notebook** — PySpark code
- **Pipeline** — Orchestration
- **Dataflow** — Visual ETL
- **Eventstream** — Real-time ingestion
- **Eventhouse** — KQL database
- **Semantic Model** — Power BI dataset
- **Report** — Power BI report

---

## 🔑 Key Bullet Points (EN)

- Microsoft Fabric is unified SaaS analytics platform combining Power BI, Data Factory, Synapse, and Data Activator in single environment with shared capacity billing
- OneLake is single data lake foundation built on ADLS Gen2, automatically created with every Fabric tenant, providing unified namespace for all workloads
- Fabric workspaces are logical containers for related items with role-based access control (Admin, Member, Contributor, Viewer)
- Capacity-based compute model charges for CU consumption rather than per-item pricing, enabling predictable cost management
- All Fabric experiences share same OneLake storage, eliminating data duplication

---

## ❓ DP-700 Exam Questions (EN)

**Q1.** Your organization has multiple teams needing isolated environments but shared capacity. Which Fabric construct should you create per team?

**Q2.** You need to store data that will be accessed by both Spark notebooks and SQL queries without duplication. Which Fabric storage component enables this?

**Q3.** A project requires 1000 CU-hours monthly. Finance wants predictable costs. Should you recommend pay-as-you-go or capacity-based pricing?

**Q4.** You want to analyze costs for Data Engineering workload separately from Power BI. Which Fabric feature provides this visibility?

**Q5.** Your team needs read-only access to lakehouse but shouldn't create new items. Which workspace role should you assign?

---

## ✅ Checklist: Co musím umět (CZ)

- [x] Vysvětlit rozdíl mezi Fabric a samostatnými Azure službami
- [x] Pochopit OneLake jako unified storage layer
- [x] Vytvořit workspace a nastavit role
- [x] Rozlišit Fabric experiences (Data Engineering, Warehouse, atd.)
- [x] Pochopit Capacity Units (CU) a billing model
- [x] Znát základní Fabric items (lakehouse, warehouse, notebook, pipeline)
- [x] Implementovat základní workspace governance

---

## 🔗 Linky

- **Praxe:** [[10.2_LABS/1_LAB_LAKEHOUSE|Lab 1: Lakehouse Setup]]
- **Následující:** [[2_LAKEHOUSE_SPARK|Note 2: Lakehouse & Spark]]
- **Index:** [[10_INDEX|Zpět na index]]

---

## NEXT → [[2_LAKEHOUSE_SPARK|2️⃣ Lakehouse & Spark]]
