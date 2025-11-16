# 📚 DATA ENGINEER JOURNEY 2026

**Cíl:** DP-700 Certifikace + Kariérní rozvoj  
**Časový plán:** 40 dní + dlouhodobě  
**Přístup:** Learning by doing  

---

# 📍 FINÁLNÍ STRUKTURA OBSIDIANU

```
DATA-ENGINEER-JOURNEY-2026/
│
├── 00_MATRIX/
│   ├── 00_INDEX.md              # Domovská stránka
│   ├── 01_PLÁN.md               # Týdenní plány
│   └── 02_CHECKLIST.md          # Co mám udělat
│
├── 01_DENNÍ_LOGY/
│   ├── 2025-11-17.md            # Denní poznámky
│   ├── 2025-11-18.md
│   └── [pokračuje denně]
│
├── 10_PROJEKTY/
│   ├── 10_DP700_CERTIFIKACE/
│   │   ├── 10_INDEX.md          # Projekt: DP-700
│   │   ├── 10_NOTES/            # Teorie
│   │   │   ├── 1_FABRIC_ARCHITEKTURA.md
│   │   │   ├── 2_LAKEHOUSE_SPARK.md
│   │   │   ├── 3_DELTA_LAKE.md
│   │   │   ├── 4_DATAFLOW_PIPELINE.md
│   │   │   ├── 5_MEDALLION_ARCHITEKTURA.md
│   │   │   ├── 6_REAL_TIME.md
│   │   │   ├── 7_KQL_EVENTHOUSE.md
│   │   │   ├── 8_WAREHOUSE_SQL.md
│   │   │   ├── 9_MONITORING.md
│   │   │   ├── 10_BEZPEČNOST.md
│   │   │   ├── 11_CI_CD.md
│   │   │   ├── 12_ADMINISTRACE.md
│   │   │   └── 13_CASE_STUDIES.md
│   │   │
│   │   └── 10_LABS/             # Praktika
│   │       ├── 1_LAB_LAKEHOUSE.md
│   │       ├── 2_LAB_SPARK.md
│   │       ├── 3_LAB_DATAFLOW.md
│   │       ├── 4_LAB_WAREHOUSE.md
│   │       ├── 5_LAB_EVENTSTREAM.md
│   │       ├── 6_LAB_KQL.md
│   │       └── 7_LAB_SECURITY.md
│   │
│   └── 20_POST_DP700/
│       ├── 20_INDEX.md          # Co je po certifikaci
│       ├── 20_FABRIC_DOJO/      # Will's program
│       │   ├── 01_PLÁN_DOJO.md
│       │   ├── 02_PROJEKT_REÁLNÝ.md
│       │   └── 03_KOMUNITA.md
│       │
│       └── 20_PORTFOLIO/        # GitHub + LinkedIn
│           ├── PROJEKTY_NÁPADY.md
│           └── CASE_STUDIES.md
│
├── 20_OBLASTI/
│   └── 20_KARIÉRNÍ_RŮST.md      # Oblast: Dlouhodobý vývoj
│
├── 30_ZDROJE/
│   ├── SLOVNÍK_CZ.md            # EN→CZ pojmy
│   ├── KQL_PŘÍKAZY.md           # KQL snippety
│   ├── PYSPARK_KÓDY.md          # Python kódy
│   ├── SQL_SCRIPTS.md           # SQL scripty
│   ├── EXTERNÍ_LINKY.md         # Všechny linky
│   └── ŠABLONY/
│       ├── ŠABLONA_DENNÍ_LOG.md
│       ├── ŠABLONA_LAB.md
│       └── ŠABLONA_POZNÁMKA.md
│
└── 40_ARCHIV/
    └── [hotové věci]
```

---

# 📄 CORE SOUBORY

## 00_MATRIX/00_INDEX.md

```markdown
# 🚀 DATA ENGINEER JOURNEY 2026

Příprava na **DP-700** + **Kariérní rozvoj**  
Start: 17.11.2025  
Cíl: Certifikace + Real-world skill

---

## Aktuální projekty

- [ ] **[[10_PROJEKTY/10_DP700_CERTIFIKACE/10_INDEX|DP-700 Certifikace]]** (40 dní)
  - Teorie: [[10_PROJEKTY/10_DP700_CERTIFIKACE/10_NOTES/1_FABRIC_ARCHITEKTURA|Start tady]]
  - Praktika: [[10_PROJEKTY/10_DP700_CERTIFIKACE/10_LABS/1_LAB_LAKEHOUSE|Labs start]]

- [ ] **[[10_PROJEKTY/20_POST_DP700/20_INDEX|Po DP-700]]** (od 15.12)
  - Fabric Dojo: [[10_PROJEKTY/20_POST_DP700/20_FABRIC_DOJO/01_PLÁN_DOJO]]
  - Real projekt: [[10_PROJEKTY/20_POST_DP700/20_FABRIC_DOJO/02_PROJEKT_REÁLNÝ]]
  - Portfolio: [[10_PROJEKTY/20_POST_DP700/20_PORTFOLIO/PROJEKTY_NÁPADY]]

---

## Dlouhodobé oblasti

**[[20_OBLASTI/20_KARIÉRNÍ_RŮST|Kariérní růst v data engineeringu]]**
- Vzdělávání, portfolia, síťování, relevance na trhu

---

## Kde začít

1. **Dnes:** [[01_DENNÍ_LOGY/2025-11-17|Dnešní log]]
2. **Učit se:** [[10_PROJEKTY/10_DP700_CERTIFIKACE/10_NOTES/1_FABRIC_ARCHITEKTURA|Teorie]]
3. **Dělat:** [[10_PROJEKTY/10_DP700_CERTIFIKACE/10_LABS/1_LAB_LAKEHOUSE|Praktika]]
4. **Slova:** [[30_ZDROJE/SLOVNÍK_CZ|Slovník]]
5. **Linky:** [[30_ZDROJE/EXTERNÍ_LINKY|Zdroje]]

---

## Linky

- Learn: https://aka.ms/DP-700onLearn
- Dojo: https://www.skool.com/fabricdojo
- Docs: https://learn.microsoft.com/fabric
```

---

## 10_PROJEKTY/10_DP700_CERTIFIKACE/10_INDEX.md

```markdown
# 🎯 PROJEKT: DP-700 CERTIFIKACE

**Cíl:** Projít zkoušku  
**Timeline:** 40 dní (17.11 - 31.12)  
**Přístup:** Learning by doing  

---

## Co dělám

1. **Teorie** - [[10_NOTES]] - 13 modulů
2. **Praktika** - [[10_LABS]] - 7 labs
3. **Případové studie** - Real-world scenáře
4. **Zkouška** - Mock exams

---

## Teorie (13 modulů)

Číti [[10_NOTES]]:

- [[1_FABRIC_ARCHITEKTURA|1. Fabric architektura]]
- [[2_LAKEHOUSE_SPARK|2. Lakehouse & Spark]]
- [[3_DELTA_LAKE|3. Delta Lake]]
- [[4_DATAFLOW_PIPELINE|4. Dataflow & Pipeline]]
- [[5_MEDALLION_ARCHITEKTURA|5. Medallion architektura]]
- [[6_REAL_TIME|6. Real-time intelligence]]
- [[7_KQL_EVENTHOUSE|7. KQL & Eventhouse]]
- [[8_WAREHOUSE_SQL|8. Warehouse & SQL]]
- [[9_MONITORING|9. Monitoring]]
- [[10_BEZPEČNOST|10. Bezpečnost]]
- [[11_CI_CD|11. CI/CD]]
- [[12_ADMINISTRACE|12. Administrace]]
- [[13_CASE_STUDIES|13. Case studies]]

---

## Praktika (7 Labs)

Dělej [[10_LABS]]:

- [ ] [[1_LAB_LAKEHOUSE|Lab 1: Lakehouse]]
- [ ] [[2_LAB_SPARK|Lab 2: Spark]]
- [ ] [[3_LAB_DATAFLOW|Lab 3: Dataflow]]
- [ ] [[4_LAB_WAREHOUSE|Lab 4: Warehouse]]
- [ ] [[5_LAB_EVENTSTREAM|Lab 5: Eventstream]]
- [ ] [[6_LAB_KQL|Lab 6: KQL]]
- [ ] [[7_LAB_SECURITY|Lab 7: Security]]

---

## Checklist před zkouškou

- [ ] Všech 13 modulů přečteno
- [ ] Všechny 7 labs hotové
- [ ] 4+ case studies zvládnute
- [ ] KQL syntaxe OK
- [ ] Medallion pochopen
- [ ] T-SQL basics OK

---

## Next: [[20_POST_DP700/20_INDEX|Po DP-700]]
```

---

## 10_PROJEKTY/20_POST_DP700/20_INDEX.md

```markdown
# 📚 CO JE PO DP-700

Jakmile mám certifikaci (31.12), budu pokračovat v:

1. **Fabric Dojo od Willa** - Real-world projekt (10 týdnů)
2. **Portfolio** - GitHub + LinkedIn
3. **Kariérní růst** - Dlouhodobě

---

## Fabric Dojo

**Start:** Cca 15.12 (nebo po DP-700)

- [[20_FABRIC_DOJO/01_PLÁN_DOJO|Plán Dojo]]
- [[20_FABRIC_DOJO/02_PROJEKT_REÁLNÝ|Real projekt]]
- [[20_FABRIC_DOJO/03_KOMUNITA|Komunita & LIVE sessions]]

**Cost:** $30/měsíc  
**Value:** Real project na CV + Network

---

## Portfolio

- [[20_PORTFOLIO/PROJEKTY_NÁPADY|Nápady na projekty]]
- [[20_PORTFOLIO/CASE_STUDIES|Case studies]]
- GitHub sync
- LinkedIn showcase

---

## Kariérní růst

Viz: [[20_OBLASTI/20_KARIÉRNÍ_RŮST|Dlouhodobý rozvoj]]
```

---

## 20_OBLASTI/20_KARIÉRNÍ_RŮST.md

```markdown
# Oblast: Kariérní růst v data engineeringu 🚀

**Popis:**  
Tato oblast představuje trvalý směr a zodpovědnost v profesním vývoji jako Data Engineer. Neřeší konkrétní projekty, ale dlouhodobý rozvoj, který vede k úspěchu v IT a datovém inženýrství.

---

## Klíčové oblasti (sub-oblasti)

### 1️⃣ Neustálé vzdělávání

- Udržovat přehled o trendech (Azure, SQL, ETL/ELT, datové architektury…)
- Participace na kurzech, bootcampech a certifikačních programech
- Experimentování s novými technologiemi a frameworky

**Akce:**
- [ ] DP-700 Certifikace (do 31.12.2025)
- [ ] Fabric Dojo (od 15.12)
- [ ] Sledovat nové Fabric features

---

### 2️⃣ Budování portfolia a osobní značky

- Práce na veřejně dostupných projektech (GitHub)
- Prezentace svého vývoje a vědomostí (LinkedIn, blog, dokumentace)
- Vytváření příkladů a case studies z praxe

**Akce:**
- [ ] GitHub profile setup
- [ ] Real project (Dojo)
- [ ] Case studies dokumentovat
- [ ] LinkedIn posts o učení

---

### 3️⃣ Síťování a komunita

- Připojování ke komunitám a odborným skupinám
- Spolupráce s ostatními data inženýry a specialisty
- Sdílení znalostí a učení se od zkušenějších

**Akce:**
- [ ] Fabric Dojo komunita (Will's)
- [ ] Reddit/Discord
- [ ] Local meetups
- [ ] Help others s otázkami

---

### 4️⃣ Zvyšování relevantnosti na trhu

- Sledování poptávky a trendů v oboru
- Rozšiřování dovedností podle potřeb
- Přizpůsobování se evolucím v datovém ekosystému

**Akce:**
- [ ] Job postings stále sledovat
- [ ] Trendy v data eng. (Databricks, dbt, Data Mesh...)
- [ ] Azure certifikace později
- [ ] Real-world project experience

---

## Status

- **DP-700:** 🔴 V přípravě
- **Portfolio:** 🟡 Po certifikaci
- **Komunita:** 🟢 Fabric Dojo - in progress
- **Trh:** 🟢 Sleduji

---

*Tato oblast je dlouhodobá - rozvíjí se během celé kariéry*
```

---

## 01_DENNÍ_LOGY/ŠABLONA.md

```markdown
# 📝 2025-11-17 (Neděle)

**Projekt:** [[10_PROJEKTY/10_DP700_CERTIFIKACE/10_INDEX|DP-700]]  
**Co jsem měl dnes dělat:**
- [ ] Fabric Architecture - přečíst
- [ ] Setup Obsidian
- [ ] Fabric trial account
- [ ] Lab 1 - start

---

## Co jsem dělal

### Učení
- Přečetl jsem: [[10_PROJEKTY/10_DP700_CERTIFIKACE/10_NOTES/1_FABRIC_ARCHITEKTURA|Fabric Architecture]]
- Pochopil jsem: OneLake = centrální repository
- Otázka: Co je Consumer Group? (vyřešit později)

### Praktika
- Vytvořil jsem Obsidian vault
- Fabric trial ready
- Lab 1 začat (Lakehouse création)

### Příště
- Pokračovat Lab 1 - load data
- Přečíst: [[10_PROJEKTY/10_DP700_CERTIFIKACE/10_NOTES/2_LAKEHOUSE_SPARK|Lakehouse & Spark]]

---

*Denní log - prostě co se stalo*
```

---

## 10_PROJEKTY/10_DP700_CERTIFIKACE/10_NOTES/1_FABRIC_ARCHITEKTURA.md

```markdown
# 1️⃣ FABRIC ARCHITEKTURA

## Teorie

### Co je Fabric?

SaaS platforma pro analytics + data engineering.

**Stack:**
- Data Factory (Pipelines)
- Data Engineering (Lakehouse, Spark)
- Data Warehouse (SQL)
- Real-Time Intelligence (Events, KQL)
- Power BI (Dashboards)

### OneLake

Jeden centrální data repository.

- Hierarchická struktura
- Delta Lake format (standard)
- Všechny experiences ho sdílí

### Workspace

Container pro items.

- Permissions
- Capacity
- Members

---

## Praktika

- [ ] Login Fabric trial
- [ ] Create workspace
- [ ] View OneLake structure
- [ ] Screenshot

---

## Otázky

- Co je Consumer Group?
- OneLake vs ADLS? (Solve: Tomorrow)

---

## Next: [[2_LAKEHOUSE_SPARK]]
```

---

## 10_PROJEKTY/10_DP700_CERTIFIKACE/10_LABS/1_LAB_LAKEHOUSE.md

```markdown
# 1️⃣ LAB: LAKEHOUSE

## Co dělám

Vytvoř lakehouse, nahraj data, queryuj.

---

## Kroky

### Fáze 1: Create
```
Workspace → New item → Lakehouse
Name: "Sales_DW"
Create
```
- [ ] Hotovo

### Fáze 2: Load Data
```
Upload files (CSV/Parquet)
To: Tables
```
- [ ] Hotovo

### Fáze 3: Query
```sql
SELECT TOP 100 * FROM table_name
```
- [ ] Hotovo

---

## Co jsem zjistil

Files vs Tables:
- Files: raw
- Tables: indexed, queryable

---

## Next: [[2_LAB_SPARK]]
```

---

## 30_ZDROJE/SLOVNÍK_CZ.md

```markdown
# 📚 SLOVNÍK - EN → ČJ

| EN | CZ | Kontext |
|----|----|----|
| Aggregate | Agregovat | summarize |
| Architecture | Architektura | design |
| Authentication | Ověřování | login |
| Backfill | Zpětné naplnění | mat. view |
| Bronze | Bronze | layer 1 |
| Capacity | Kapacita | resources |
| Cluster | Shluk | Spark |

...doplňuji jak potřebuji
```

---

## 30_ZDROJE/EXTERNÍ_LINKY.md

```markdown
# 🌐 LINKY

**Learn:**
- DP-700: https://aka.ms/DP-700onLearn
- Fabric Docs: https://learn.microsoft.com/fabric

**Community:**
- Fabric Dojo: https://www.skool.com/fabricdojo
- YouTube: https://www.youtube.com/results?search_query=Microsoft+Fabric

**Labs:**
- Lab 7: https://microsoftlearning.github.io/dp-700-data-engineer/Instructions/Labs/07-create-a-lakehouse.html
```

---

# ✅ SETUP - 5 MINUT

```
1. Obsidian download: obsidian.md
2. Create vault: "DATA-ENGINEER-JOURNEY-2026"
3. Create folder structure výše
4. Copy-paste soubory
5. [[00_MATRIX/00_INDEX|START - Index]]
```

---

# 🎬 ZAČÍNÁŠ

1. **Obsidian setup** (5 min)
2. **Vault create** (5 min)
3. **Struktura copy** (5 min)
4. **Jdi na Learn**
5. **Zapiš si poznámky**

**LEARNING BY DOING! 🚀**
