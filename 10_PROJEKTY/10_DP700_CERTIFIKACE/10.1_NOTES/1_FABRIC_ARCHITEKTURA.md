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

---

### Workspaces

Logical containers pro Fabric items.

**Workspace roles:**
- **Admin** — Full control
- **Member** — Can create items
- **Contributor** — Can edit existing items
- **Viewer** — Read-only access

---

### Capacity

Compute resource pool (billing unit).

**Capacity tiers:**
- **F2-F8** — Trial, small dev
- **F64** — Small production
- **F128-F256** — Medium production

**Capacity Units (CU):** Every operation consumes CUs

---

## 🔑 Key Bullet Points (EN)

- Microsoft Fabric is unified SaaS analytics platform combining Power BI, Data Factory, Synapse in single environment with shared capacity billing
- OneLake is single data lake foundation built on ADLS Gen2, automatically created with every Fabric tenant
- Fabric workspaces are logical containers for items with role-based access control (Admin, Member, Contributor, Viewer)
- Capacity-based compute model charges for CU consumption rather than per-item pricing
- All Fabric experiences share same OneLake storage, eliminating data duplication

---

## ❓ DP-700 Exam Questions (EN)

**Q1.** Your organization has multiple teams needing isolated environments but shared capacity. Which Fabric construct per team?

**Q2.** You need store data accessed by both Spark notebooks and SQL queries without duplication. Which component?

**Q3.** Project requires 1000 CU-hours monthly. Finance wants predictable costs. Recommend pay-as-you-go or capacity-based?

**Q4.** You want analyze costs for Data Engineering workload separately from Power BI. Which feature provides this?

**Q5.** Your team needs read-only access to lakehouse but shouldn't create new items. Which workspace role?

---

## ✅ Checklist: Co musím umět (CZ)

- [ ] Vysvětlit rozdíl mezi Fabric a samostatnými Azure službami
- [ ] Pochopit OneLake jako unified storage layer
- [ ] Vytvořit workspace a nastavit role
- [ ] Rozlišit Fabric experiences
- [ ] Pochopit Capacity Units (CU) a billing
- [ ] Znát základní Fabric items

---

## 🔗 Linky

- **Praxe:** [[10.2_LABS/1_LAB_LAKEHOUSE|Lab 1: Lakehouse]]
- **Další:** [[2_LAKEHOUSE_SPARK|Note 2: Lakehouse & Spark]]
- **Index:** [[10_INDEX|Index]]

---

NEXT → [[2_LAKEHOUSE_SPARK|2️⃣ Lakehouse & Spark]]
