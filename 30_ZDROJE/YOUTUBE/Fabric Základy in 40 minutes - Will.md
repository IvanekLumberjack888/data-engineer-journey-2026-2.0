# Microsoft Fabric – studijní příručka (základní přehled)

Zdroj: [https://youtu.be/J4i5lcROJcs?si=_MuHL7FoYbhOzruJ](https://youtu.be/J4i5lcROJcs?si=_MuHL7FoYbhOzruJ) [web:2]

---

## 1. Co je Microsoft Fabric

Microsoft Fabric je end‑to‑end datová a analytická platforma, která sjednocuje ingest, ukládání, zpracování, analýzu i reporting do jednoho produktu. [web:2][web:10] Cílem je odstranit datová sila, omezit zbytečné kopírování dat mezi systémy a zjednodušit práci napříč rolemi (data engineer, data scientist, BI, business). [web:2][web:10]

Fabric všechny služby staví nad jedním společným datovým základem (OneLake) a poskytuje integrované prostředí pro dávkové, interaktivní i real‑time scénáře. [web:2][web:10] Umožňuje tak postavit kompletní data platformu bez nutnosti skládat mnoho separátních Azure služeb. [web:10][web:11]

---

## 2. Jaké problémy Fabric řeší

Typická organizace má data rozbitá mezi různé databáze, data lakes, souborové share, SaaS aplikace a BI nástroje, což vede k duplicitám, nekonzistentním výsledkům a složité správě. [web:2][web:11] Každé oddělení často buduje vlastní datové řešení, takže vznikají silá a není jasné, které číslo je „jediný zdroj pravdy“. [web:2][web:11]

IT týmy musí spravovat mnoho separátních technologií, přístupová práva, infra a billing, zatímco business čeká na data a těžko experimentuje. [web:2][web:11] Fabric tuto roztříštěnost řeší sjednocením úložiště, nástrojů i governance do jedné SaaS platformy. [web:2][web:10]

---

## 3. Základní koncepty: OneLake, Delta, workspaces

### 3.1 OneLake

OneLake je jednotné, logické datové jezero pro celou organizaci, které slouží jako společná vrstva pro všechny Fabric workloads. [web:10][web:13] Je postavený na Azure Data Lake Storage Gen2, ale uživatelé ho vnímají jako SaaS službu podobnou OneDrive pro data. [web:13][web:20]

Všechna data z lakehouse, warehouse, KQL databází a dalších itemů jsou ukládána do OneLake, což umožňuje sdílený přístup a jednoduchou spolupráci napříč týmy. [web:10][web:13] OneLake podporuje i „shortcuts“, tedy virtuální odkazy na externí úložiště bez fyzického kopírování dat. [web:13][web:19]

### 3.2 Delta Parquet

Fabric ukládá tabulková data v Delta Parquet formátu, který kombinuje výkon sloupcového formátu Parquet s transakčními vlastnostmi Delta Lake. [web:13][web:19] Tento formát umožňuje ACID transakce, time‑travel, efektivní updaty a mazání, a zároveň vysoký výkon při analytických dotazech. [web:19][web:10]

Díky jednotnému Delta formátu mohou různé enginy (T‑SQL, Spark, KQL, VertiPaq) pracovat nad stejnými fyzickými daty bez nutnosti ETL mezi službami. [web:10][web:13] To zásadně snižuje počet datových kopií a zjednodušuje architekturu. [web:13][web:14]

### 3.3 Workspaces a items

Workspaces slouží jako logické kontejnery pro data, reporty a objekty (lakehouse, warehouse, pipelines, notebooks, semantic models). [web:10][web:13] Umožňují řídit přístupová práva, vlastnictví a životní cyklus řešení na úrovni týmu nebo domény. [web:13][web:20]

Každý workspace běží na určité Fabric kapacitě a všechny jeho items ukládají data do OneLake, což zajišťuje jednotnou správu i fakturaci. [web:10][web:13]

---

## 4. Sedm experiences ve Fabric

Fabric nabízí několik „experience“ (workloads), které společně pokrývají celý end‑to‑end data lifecycle. [web:10][web:2]

### 4.1 Data Factory

Data Factory ve Fabric poskytuje:

- Dataflows Gen2: no‑code/low‑code transformace v Power Query (M), stovky konektorů do SaaS, databází a souborů. [web:10][web:9]  
- Pipelines: orchestraci aktivit (copy, notebooky, SQL skripty, trigery, větvení, parametry, plánování). [web:9][web:20]

Používá se pro ingest a ETL/ELT procesy od jednoduchých kopií až po komplexní workflow s monitoringem a alertingem. [web:9][web:17]

### 4.2 Data Warehouse

Data Warehouse je plnohodnotný relační datový sklad založený na T‑SQL enginu Polaris, uložený nad OneLake. [web:10][web:17] Umožňuje vytvářet tabulky, schémata, views, indexy a procedury, a je optimalizovaný pro analytické dotazy s vysokou konkurencí. [web:10][web:17]

Výhodou je, že data skladu jsou zároveň Delta tabulky v OneLake, takže k nim mohou přistupovat i jiné workloads, včetně Power BI přes Direct Lake. [web:10][web:13]

### 4.3 Data Engineering

Data Engineering experience staví na Lakehouse a Spark engine:

- Lakehouse kombinuje výhody data lake (souborový systém) a databáze (tabulkový pohled). [web:10][web:13]  
- Spark notebooks (PySpark, Scala, SQL) slouží k čištění, transformaci a obohacování dat, typicky v medallion architektuře (bronze/silver/gold). [web:9][web:19]

Je to základ pro výpočetně náročné transformace, batch pipeline a přípravu dat pro další vrstvy (DW, BI, ML). [web:9][web:17]

### 4.4 Data Science

Data Science experience poskytuje prostředí pro:

- Notebooks pro explorativní analýzu a tvorbu modelů (Python, R). [web:9][web:10]  
- Experiment tracking (např. přes MLflow) a model registry pro správu verzí a nasazení modelů. [web:9][web:19]

Data scientist pracuje nad stejnými daty v OneLake, která používá i zbytek organizace, což zjednodušuje operationalizaci modelů. [web:10][web:11]

### 4.5 Real‑Time Analytics

Real‑Time Analytics je založené na KQL (Kusto Query Language) a databázích podobných Azure Data Explorer. [web:10][web:9] Umožňuje ingestovat streamy eventů (telemetrie, logy, IoT) a psát ad‑hoc i dashboardové dotazy pro near real‑time analýzu. [web:10][web:19]

Event streams a KQL DB se integrují s OneLake i Power BI, takže je možné kombinovat historická batch data s realtime daty v jednom prostředí. [web:10][web:13]

### 4.6 Power BI

Power BI ve Fabric zajišťuje:

- Semantic models (dříve datasets) jako analytickou vrstvu nad Lakehouse, DW nebo přímo Delta tabulkami v OneLake. [web:10][web:8]  
- Reports a dashboards pro vizualizaci a sdílení insightů s business uživateli. [web:10][web:11]

Díky Direct Lake může Power BI číst Delta tabulky v OneLake bez nutnosti klasického importu, což kombinuje výkon in‑memory enginu s aktuálností dat. [web:8][web:14]

### 4.7 Data Activator

Data Activator slouží k definici pravidel typu „if this then that“ nad tabulkovými i realtime daty. [web:2][web:9] Umožňuje detekovat situace (např. prahové hodnoty, anomálie) a spouštět akce jako e‑maily, webhooks nebo Power Automate flows. [web:2][web:9]

Tím uzavírá smyčku mezi analýzou dat a operativní reakcí bez nutnosti psát vlastní integrační kód. [web:2][web:11]

---

## 5. Compute enginy a jazyky

Fabric integruje několik výpočetních enginů, které sdílí stejná data v OneLake:

- T‑SQL engine (Polaris) pro Data Warehouse a SQL endpointy. [web:10][web:17]  
- Spark engine pro Data Engineering a Data Science notebooks a joby. [web:9][web:19]  
- KQL engine pro Real‑Time Analytics. [web:10][web:19]  
- VertiPaq engine pro Power BI semantic models. [web:10][web:8]

Uživatel pracuje v jazyce, který zná (T‑SQL, Python, Scala, R, KQL, DAX/M v Power BI), ale všechny enginy zapisují a čtou Delta data v OneLake. [web:10][web:13] Tím odpadá potřeba opakovaných datových přesunů mezi službami jen kvůli změně nástroje. [web:13][web:14]

---

## 6. Licencování a jak začít

Fabric používá kapacitní licenční model, kde se platí za sdílenou výpočetní kapacitu (F‑kapacity) pro workspaces. [web:10][web:3] Organizace s Power BI Premium kapacitami mohou Fabric využívat nad těmito kapacitami a postupně přecházet z čistě BI scénářů na full data platformu. [web:10][web:8]

Pro samostudium lze využít:

- Fabric trial (časově omezený, ale plně funkční). [web:10][web:9]  
- M365 developer tenant, kde lze aktivovat Fabric a získat sandbox bez dopadu na produkční prostředí. [web:10][web:9]

---

## 7. Exam‑like otázky (styl DP‑700)

1. Vysvětli rozdíl mezi OneLake a klasickým data lake na ADLS Gen2 z pohledu správy, sdílení dat a práce s více workloads. [web:10][web:13]  
2. Kdy zvolíš Lakehouse a kdy Data Warehouse, pokud řešíš analytiku pro enterprise reporting vs. data science sandbox? [web:10][web:17]  
3. Jaké výhody přináší Delta Parquet formát v prostředí s více enginy (T‑SQL, Spark, KQL, Power BI)? [web:13][web:19]  
4. Navrhni end‑to‑end pipeline v Data Factory pro denní zpracování: zdroje, transformace, cílové úložiště a napojení na Power BI. [web:9][web:20]  
5. Jak bys integroval Real‑Time Analytics (KQL DB) do řešení, kde už existuje Lakehouse a Power BI reporting? [web:10][web:19]  
6. Jak mohou data engineers a data scientists společně využívat Lakehouse a notebooks k přípravě dat a trénování modelů? [web:9][web:11]  
7. V jakých situacích dává smysl použít Data Activator místo klasického reportového alertingu? [web:2][web:9]  
8. Jak bys navrhl řízení přístupů k datům ve více workspaces, pokud máš interní uživatele a externího partnera? [web:10][web:20]

---

## 8. Checklist skillů, které bys měl ovládat

### 8.1 Architektura a koncepty

- Vysvětlit roli OneLake, Delta formátu a shortcuts v architektuře Fabric. [web:10][web:13]  
- Rozlišit Lakehouse, Data Warehouse a KQL DB a přiřadit je k typickým use‑cases. [web:10][web:19]

### 8.2 Data Factory (ingest + orchestraci)

- Vytvořit dataflow pro načtení dat ze zdrojů (SQL, API, files) a aplikaci základních transformací v Power Query. [web:9][web:20]  
- Vytvořit pipeline, která orchestruje dataflows/notebooky/SQL scripts, má plán, retry politiku a logging. [web:9][web:17]

### 8.3 Data Engineering (Lakehouse)

- Založit Lakehouse a navrhnout bronze/silver/gold vrstvy pro staging, očištěná a business‑ready data. [web:9][web:19]  
- Používat Spark notebooks (PySpark) pro joiny, agregace, deduplikace, typové konverze a zápis do Delta tabulek. [web:9][web:19]

### 8.4 Data Warehouse

- Navrhnout schéma (star schema), vytvořit tabulky, views a T‑SQL transformace ve warehouse. [web:17][web:20]  
- Popisovat, jak DW data využívá Power BI přes Direct Lake nebo import. [web:8][web:10]

### 8.5 Power BI / semantic models

- Napojit semantic model na Lakehouse nebo DW a definovat relace, measures a základní kalkulace. [web:8][web:10]  
- Vytvořit report, který odpovídá konkrétním business otázkám a je optimalizovaný pro výkon. [web:10][web:11]

### 8.6 Real‑Time Analytics & Data Activator

- Založit KQL DB, ingestovat stream/log data a psát základní KQL dotazy. [web:10][web:19]  
- Vytvořit v Data Activatoru trigger na události v datech a navázat akci (např. e‑mail, webhook, Power Automate). [web:2][web:9]

---

## 9. Mini‑projekt: Automotive analytika ve Fabric

### 9.1 Scénář

Organizace provozuje automotive dealership (prodej + servis) a chce jednotný reporting a pokročilou analytiku nad prodeji a servisními daty. [web:17][web:20]

### 9.2 Ingest dat

- Prodejní data (vozidla, ceny, prodejci, lokality) z databáze nebo CSV načti přes Data Factory do Lakehouse (bronze). [web:9][web:17]  
- Servisní data (zakázky, náklady, typy oprav) přidej jako další zdroj a sjednoť klíče zákazníků/vozidel. [web:17][web:20]

### 9.3 Datový model

- V Lakehouse vytvoř silver vrstvu s očištěnými tabulkami (fakt a dimenze) a gold vrstvu s business pohledem pro reporting. [web:9][web:19]  
- Alternativně nad gold vytvoř Data Warehouse a přesuň transformační logiku do T‑SQL skriptů. [web:17][web:20]

### 9.4 Orchestrace

- V Data Factory vytvoř pipeline, která podle plánu: načte data, spustí notebook/SQL script, aktualizuje gold tabulky a nakonec refreshne semantic model. [web:9][web:17]

### 9.5 Reporting

- V Power BI semantic modelu nadefinuj metriky jako tržby, marže, počet prodaných vozů, využití servisu a opakované návštěvy. [web:10][web:11]  
- Vytvoř report pro management s pohledem podle značek, dealerství, prodejců a období. [web:10][web:11]

### 9.6 Rozšíření o real‑time (volitelné)

- Simuluj stream leadů z webu nebo telemetrie vozidel do KQL DB. [web:10][web:19]  
- V Data Activatoru nastav pravidlo pro eskalaci, pokud počet kritických eventů překročí definovaný práh. [web:2][web:9]

---

## 10. Jak z příručky udělat osobní studijní plán

- Rozděl si sekce 1–6 jako teoretický základ na první týden (čtení, poznámky, vlastní shrnutí v češtině). [web:10][web:9]  
- V druhém týdnu se zaměř na checklist skillů (kap. 8) a manuálně si odškrtávej, co jsi reálně zkusil ve Fabric. [web:9][web:20]  
- Ve třetím týdnu postav mini‑projekt z kapitoly 9 end‑to‑end a použij exam‑like otázky z kapitoly 7 jako self‑test před DP‑700. [web:17][web:20]
