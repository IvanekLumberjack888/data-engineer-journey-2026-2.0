# 1️⃣ FABRIC ARCHITEKTURA

**Cíl:** Pochopit Fabric jako platformu a její klíčové komponenty

---

## 📖 TEORIE

### Co je Microsoft Fabric?

SaaS platforma pro end-to-end data analytics a engineering.

- Všechno v jednom stacku
- Jednotný datový model
- Integrované nástroje
- Cloud-native řešení

**Zkratky:**
- SaaS = Software as a Service
- ETL = Extract, Transform, Load
- OneLake = Centrální data repository

### OneLake - Centrální úložiště

Jeden data lake na tenant.

**Charakteristiky:**
- Hierarchická struktura (folder-like)
- Delta Lake format (standard)
- OneCopy - fyzicky jeden, logicky více
- Všechny experiences ho sdílí
- Verzování obsahu

**Vztah:**
- OneLake ↔ [[20_OBLASTI/20_KARIÉRNÍ_RŮST|Dlouhodobý rozvoj]]
- OneLake ↔ Azure ADLS Gen2

### Workspace

Container pro všechny Fabric items.

**Vlastnosti:**
- Permissions (kdo má přístup)
- Capacity (kolik resources)
- Members (uživatelé)
- Settings (konfigurace)

### Fabric Experiences (6 hlavních)

Jednotlivé tools v Fabric:

1. **Data Factory** — Pipelines, orchestrace
2. **Data Engineering** — Lakehouse, Spark notebooks
3. **Data Warehouse** — SQL queries
4. **Real-Time Intelligence** — Eventstreams, KQL
5. **Power BI** — Reports, dashboards
6. **Databases** — SQL databases

### Capacity & Licensing

**Fabric SKU:**
- F2, F4, F8, F16, F32... (Fabric units)
- Pay per hour
- Auto-scale (volitelné)

**License types:**
- Premium capacity
- Trial (60 dní zdarma)

---

## 🛠️ PRAXE

Úkoly k provedení:

- [ ] Login do Fabric trial: https://app.fabric.microsoft.com
- [ ] Create workspace (název: "Learning")
- [ ] Prozkoumej OneLake (File menu)
- [ ] View workspace settings
- [ ] Check capacity information
- [ ] Screenshot uložit

---

## 🔗 INTERNÍ LINKY

- Next: [[2_LAKEHOUSE_SPARK|2. Lakehouse & Spark]]
- Back: [[10_INDEX|Projekt DP-700]]
- Checklist: [[02_CHECKLIST|Co musím zvládnout]]

---

## 🔗 EXTERNÍ LINKY

**Microsoft Learn:**
- Fabric Overview: https://learn.microsoft.com/en-us/fabric/get-started/microsoft-fabric-overview
- Workspace Setup: https://learn.microsoft.com/fabric/admin/admin-overview

**Official Docs:**
- Fabric Documentation: https://learn.microsoft.com/fabric
- OneLake: https://learn.microsoft.com/fabric/onelake/onelake-overview

**YouTube:**
- Fabric Intro: https://www.youtube.com/results?search_query=Microsoft+Fabric+introduction
- Workspace Setup: https://www.youtube.com/results?search_query=Fabric+workspace+creation

---

## ❓ OTÁZKY

| Otázka | Odpověď | Status |
|--------|---------|--------|
| Jaký je max file size v OneLake? | Vyřešit | 🟡 |
| Jak se mění capacity v průběhu? | Vyřešit | 🟡 |

---

obsidian://open?vault=data-engineering-journey-2026-2.0&file=10_PROJEKTY%2F10_DP700_CERTIFIKACE%2F10.1_NOTES%2F2_LAKEHOUSE_SPARK.md