**Podrobný studijní průvodce**, **Kvíz s klíčem odpovědí**, **Esejistické otázky** a **Komplexní slovníček pojmů**.

--------------------------------------------------------------------------------

# 📚 Podrobný Studijní Průvodce DP-700

Tento průvodce slouží k revizi a syntéze informací z Vašeho 20denního studijního plánu, zaměřeného na tři hlavní domény zkoušky DP-700: **Implementace, Ingest a Transformace, a Monitoring s Optimalizací**.

## I. Základy a Architektura (Implementing & Managing)

### A. Hierarchie a Základní Koncepty

1. **Fabric Hierarchie:** Platforma je hierarchicky strukturována.

    ◦ **Tenant:** Vaše organizace (nejvyšší úroveň).

    ◦ **Capacity:** Určuje dostupný výpočetní výkon (**Compute Units - CU**) a fakturaci (F-SKUs).

    ◦ **Workspace:** Logický kontejner pro Fabric objekty (items), kde probíhá spolupráce.

2. **OneLake (Unified Data Lake):** Působí jako jednotné datové jezero pro celou organizaci.

    ◦ Klíčový princip: **Jediná kopie dat** (_single copy of data_) pro odstranění datových sil a duplicit.

    ◦ Standardní formát pro tabulková data je **Delta Parquet** (podporuje ACID transakce a verzování).

3. **Shortcuts a Mirroring (Virtualizace):**

    ◦ **Shortcuts:** Virtuální odkazy na data v jiných umístěních (interních nebo externích jako ADLS Gen2, Amazon S3, Google Cloud Storage) **bez replikace dat**.

    ◦ **Database Mirroring:** Vytváří **near real-time repliku** podporovaných databází (Azure SQL, Snowflake) do formátu Delta Parquet, minimalizující ETL.

### B. Řízení a Zabezpečení (Governance & Security)

1. **Access Control:** Vždy se řídí **Principem nejmenších práv** (_Principle of Least Privilege_).

    ◦ **Workspace Role:** Řídí přístup na široké úrovni. **Viewer** může číst data přes SQL endpoint, ale nemůže spouštět pipelines.

    ◦ **Item-level Access:** Přístup ke konkrétní položce (např. Data Warehouse).

2. **Granulární Zabezpečení (Warehouse/SQL Endpoint):**

    ◦ **Row-Level Security (RLS):** Omezuje přístup k datům na základě řádků (implementace pomocí **Table-Valued Function (TVF)** a **Security Policy** v T-SQL).

    ◦ **Column-Level Security (CLS):** Omezuje přístup k definovaným sloupcům (implementace pomocí `GRANT SELECT (sloupce)` v T-SQL).

    ◦ **Dynamic Data Masking (DDM):** Maskuje citlivé informace (např. email, plat) na úrovni **výsledku dotazu**, aniž by měnilo podkladová data; **nešifruje** data a lze jej obejít.

3. **Governance (Endorsements):** Pomáhá identifikovat důvěryhodná data.

    ◦ **Promoted:** Doporučeno tvůrcem položky (nízká úroveň důvěry).

    ◦ **Certified:** Splňuje firemní standardy kvality, vyžaduje schválení.

    ◦ **Master Data:** Jádro datového zdroje s nejvyšší důvěryhodností.

--------------------------------------------------------------------------------

## II. Ingest a Transformace (Ingesting & Transforming)

### A. Architektura Data Store

|   |   |   |   |
|---|---|---|---|
|Úložiště|Primární zaměření|Primární Jazyk|Klíčové Vlastnosti|
|**Lakehouse**|Flexibilní ELT, Nestrukturovaná data, ML/Data Science|PySpark/Spark SQL|Má sekci **Files** (surová data) a **Tables** (Delta tabulky). Podporuje pouze **Read-Only SQL Analytics Endpoint**.|
|**Data Warehouse (DW)**|BI Reporting, Gold Layer, Tabulková data|T-SQL|Podporuje **Multi-table transactions**. Podporuje Stored Procedures, Views, Schemas.|
|**Eventhouse (KQL DB)**|Real-time event data, Time-series, Logy|KQL|Optimalizováno pro rychlé dotazy. Spravuje se pomocí **Retention** a **Caching** policies.|

### B. Ingestion a Orchestrace

1. **Data Pipelines:** Primární nástroj pro **Orchestraci** a hromadný přesun dat (Batch ETL/ELT).

    ◦ Klíčová aktivita: **Copy Data** (pro ingest z 100+ zdrojů).

    ◦ Pokročilé vzorce: **Metadata-Driven Pipelines** se skládají z **Lookup** (načtení metadat) a **ForEach** (iterace).

    ◦ Lze spouštět i přes **Invoke Pipeline** (Parent-Child arch.).

2. **Dataflows Gen2 (DFG2):** **Low-Code/No-Code** ETL, poháněné Power Query (M language).

    ◦ Ideální pro analytiky a pro přístup k **On-Premise Sources** přes Data Gateway.

    ◦ Klíčové pro scénáře, které vyžadují **minimalizovat vývojové úsilí** (_minimize development effort_).

3. **Notebooks (Spark/PySpark):** **Full Code** řešení (Python/Spark SQL).

    ◦ Ideální pro: komplexní custom transformace, integraci s API, velký objem dat a Data Science/ML.

    ◦ **notebookutils** je klíčová knihovna pro interní Fabric úkoly (např. orchestrace jiných notebooků, čtení secretů).

4. **Loading Patterns:**

    ◦ **Incremental Load:** Implementuje se v Lakehouse primárně pomocí **Delta MERGE INTO** (pro UPSERT operace – insert, update, delete v jednom).

    ◦ **Full Load:** Přepíše cílovou tabulku (např. `mode("overwrite")`).

### C. Dimensional Modeling (DW/Lakehouse)

• **SCD Type 2:** Typ pomalu se měnící dimenze, který sleduje **celou historii** změn atributu (vytvoří nový řádek s `ValidFrom`/`ValidTo` nebo `IsCurrent` flagem).

• **Surrogate Keys (Náhradní klíče):** Používají se místo **Natural Keys** (zdrojové ID) pro podporu sledování historie a relací s Fact tabulkami.

--------------------------------------------------------------------------------

## III. Monitoring a Optimalizace

### A. Monitoring a Debugging

1. **Monitoring Hub:** Centrální místo pro sledování stavu **všech běhů** (Pipelines, Notebooks, Dataflows, Semantic Model Refreshes).

2. **Capacity Metrics App:** Power BI report pro Capacity Admins, slouží k monitorování spotřeby **CU (Capacity Units)**, identifikaci nadměrné spotřeby a detekci **Throttlingu** (snížení výkonu při přetížení).

3. **Pipeline Debugging:** Panel **Inputs/Outputs** v detailu běhu je klíčový pro ladění dynamických výrazů a chyb.

4. **Data Warehouse Monitoring:** **Query Activity tab** a **Query Insights** view sledují dlouho běžící a často spouštěné T-SQL dotazy.

5. **Spark Monitoring:** Pro detailní diagnostiku výkonu (skew) se používá **Spark History Server**.

### B. Optimalizace Dat

1. **Delta Lake Údržba (Lakehouse):**

    ◦ **OPTIMIZE****:** Slouží ke **kompakci** malých souborů Parquet do optimální velikosti, čímž zlepšuje výkon čtení.

    ◦ **VACUUM****:** Fyzicky maže staré soubory, které již nejsou odkazovány transakčním logem (uvolnění místa).

2. **V-Order:** Proprietární optimalizace aplikovaná na Delta soubory, zlepšující výkon čtení, zvláště pro **Direct Lake**.

3. **Spark Pools:** **Custom Spark Pool** se používá pro náročné a velké joby, i když má delší start-up čas než **Starter Pool**. **High Concurrency** umožňuje více jobům sdílet stejnou Spark Session.

### C. Real-Time a BI Integrace

1. **Eventstreams:** Low-Code nástroj pro streamovaná data, podporuje agregace přes **Time Windows** (např. **Tumbling Window** pro pevné nepřekrývající se intervaly).

2. **KQL (Kusto Query Language):** Read-only jazyk pro Eventhouse. **Materialized Views** se používají k ukládání předpočítaných agregací pro rychlý reporting.

3. **Direct Lake:** Nový režim připojení pro **Semantic Models** (Power BI), který kombinuje rychlost Importu a aktuálnost Direct Query. Data čte přímo z Delta Parquet souborů v OneLake.

    ◦ Klíčová funkce: **Fallback** (přepnutí) na Direct Query, pokud Direct Lake nemůže zpracovat dotaz (např. kvůli nepodporovaným View nebo DAX).

--------------------------------------------------------------------------------

# 🧠 Kvíz (10 Krátkých Otázek)

## Odpovězte na každou otázku v rozsahu 2–3 vět s ohledem na informace ve zdrojích.

1. **Popište vztah mezi Tenant, Capacity a Workspace v hierarchii Microsoft Fabric.**

2. **Jaká je hlavní architektonická výhoda používání OneLake, pokud jde o správu dat v rámci organizace?**

3. **Jaký je kritický rozdíl mezi Data Warehouse a Lakehouse, pokud jde o podporu transakcí?**

4. **Vysvětlete, jaký je účel Shortcut Cache a u jakých externích zdrojů se primárně používá.**

5. **V jakém scénáři byste upřednostnili Dataflow Gen2 před Notebookem (PySpark) pro ETL/ELT a proč?**

6. **K čemu slouží knihovna** **notebookutils** **a jaká je jedna její klíčová funkce?**

7. **Jaký Delta Lake příkaz je klíčový pro implementaci inkrementálního načítání (Incremental Load) v Lakehouse a co provádí?**

8. **Vysvětlete hlavní rozdíl mezi Row-Level Security (RLS) a Dynamic Data Masking (DDM).**

9. **Který Fabric nástroj musí použít Capacity Admin, aby monitoroval spotřebu CU a detekoval throttling?**

10. **Popište klíčovou výhodu Direct Lake módu pro Power BI Semantic Models a co je to Fallback funkce?**

--------------------------------------------------------------------------------

## ✅ Klíč Odpovědí

1. **Popište vztah mezi Tenant, Capacity a Workspace v hierarchii Microsoft Fabric.** **Tenant** je nejvyšší úroveň, která představuje organizaci. Každý Tenant hostuje **Capacities**, které alokují **Compute Units (CU)** a definují výpočetní výkon. **Workspaces** jsou kolaborativní kontejnery, které žijí uvnitř Capacity a drží všechny Fabric položky (items).

2. **Jaká je hlavní architektonická výhoda používání OneLake, pokud jde o správu dat v rámci organizace?** Hlavní výhodou OneLake je, že funguje jako jednotné datové jezero a prosazuje princip **jediné kopie dat** (_single copy of data_). To pomáhá eliminovat datová sila a duplicity (replikaci dat), které jsou běžné ve starších architekturách.

3. **Jaký je kritický rozdíl mezi Data Warehouse a Lakehouse, pokud jde o podporu transakcí?** **Data Warehouse** podporuje **multi-table transactions** (transakce napříč více tabulkami), které zajišťují konzistenci dat, což je klíčové pro Gold vrstvu. **Lakehouse** tuto funkci v současnosti nepodporuje, což znamená, že transakční integrita se musí řešit na úrovni jedné tabulky (Delta) nebo pomocí orchestrace.

4. **Vysvětlete, jaký je účel Shortcut Cache a u jakých externích zdrojů se primárně používá.** **Shortcut Cache** je nastavení na úrovni Workspace, které ukládá často přístupná data z externích cloudových úložišť lokálně v OneLake. Hlavním účelem je snížit náklady na egress (poplatky za odchozí data), a primárně se používá pro **Amazon S3** a **Google Cloud Storage**.

5. **V jakém scénáři byste upřednostnili Dataflow Gen2 před Notebookem (PySpark) pro ETL/ELT a proč?** Dataflow Gen2 (DFG2) byste upřednostnili ve scénářích, které vyžadují **low-code/no-code** přístup a potřebují **minimalizovat vývojové úsilí**. DFG2 je také ideální pro přístup k **on-premise zdrojům** prostřednictvím Data Gateway, což Notebooky bez dalších kroků nezvládají.

6. **K čemu slouží knihovna** **notebookutils** **a jaká je jedna její klíčová funkce?** `notebookutils` je vestavěný Python balík, který zefektivňuje běžné úlohy v Notebooku. Jedna klíčová funkce je **orchestrace jiných notebooků** (např. pomocí `notebookutils.notebook.run_multiple`), dále slouží ke čtení secretů (credentials) nebo operacím se souborovým systémem.

7. **Jaký Delta Lake příkaz je klíčový pro implementaci inkrementálního načítání (Incremental Load) v Lakehouse a co provádí?** Klíčový příkaz je **Delta MERGE INTO**. Tento příkaz provádí **UPSERT** operaci, což znamená, že dokáže v jediné operaci zpracovat vložení nových řádků, aktualizace existujících řádků a mazání záznamů v cílové Delta tabulce.

8. **Vysvětlete hlavní rozdíl mezi Row-Level Security (RLS) a Dynamic Data Masking (DDM).** **Row-Level Security (RLS)** **omezuje přístup** k datům na základě **řádků** (např. uživatel vidí jen své záznamy). **Dynamic Data Masking (DDM)** pouze **maskuje** zobrazení citlivých dat (např. hvězdičkami) na úrovni výsledku dotazu, ale neomezuje přístup k datům a nešifruje je.

9. **Který Fabric nástroj musí použít Capacity Admin, aby monitoroval spotřebu CU a detekoval throttling?** Capacity Admin musí použít nástroj **Capacity Metrics App**. Tato aplikace poskytuje detailní Power BI report, který sleduje spotřebu **Capacity Units (CU)**, pomáhá identifikovat přetížení a detekuje, kdy dochází k **Throttlingu** (snížení výkonu).

10. **Popište klíčovou výhodu Direct Lake módu pro Power BI Semantic Models a co je to Fallback funkce?** Klíčovou výhodou **Direct Lake** je, že kombinuje rychlost Import módu s aktuálností Direct Query, protože čte data **přímo z Delta Parquet souborů v OneLake** bez nutnosti refreshů. **Fallback** je automatická funkce, kdy se Direct Lake přepne do režimu Direct Query, pokud narazí na nepodporovanou operaci (např. View nebo komplexní DAX).

--------------------------------------------------------------------------------

# 📝 Esejistické Otázky

## Následujících pět otázek vyžaduje syntézu znalostí z více oblastí Fabric a simulují scénáře zkoušky DP-700.

1. **Architektura Gold Vrstvy:** Navrhněte kompletní architekturu Gold vrstvy pro finanční reporting v Microsoft Fabric, která využívá DW a Semantic Model. Popište, jak zajistíte **Multi-table Transaction Consistency**, implementujete **Row-Level Security (RLS)** a jakou roli hraje **Direct Lake** v následném BI reportingu, včetně popisu možných limitů a jejich řešení.

2. **End-to-End Inkrementální Pipeline:** Navrhněte **Metadata-Driven Data Pipeline** pro inkrementální ingest 50 tabulek ze zdrojové databáze do Lakehouse Bronze vrstvy. Popište klíčové aktivity orchestrace (**Lookup/ForEach**), jak implementujete **UPSERT** logiku v Lakehouse Silver vrstvě a jaké nástroje (Notebook vs. Pipeline Copy Data) použijete pro efektivní přesun dat.

3. **Real-Time Analýza a Validace Kvality:** Popište, jak byste navrhli real-time řešení pro monitoring telemetrie ze senzorů v Eventhouse. Vysvětlete roli **Eventstreams** a jak byste využili **Materialized Views** pro zrychlení dashboardingu. Dále navrhněte, jak zajistit **validaci schématu a obsahu** příchozích streamovaných dat pomocí code-based řešení (Spark) a jak byste logovali chyby (Failure Strategy).

4. **Optimalizace a Throttling:** Váš produkční systém trpí nepravidelným **Throttlingem** a pomalým během Spark Notebooků. Jako Data Engineer, jaké dva hlavní nástroje použijete pro **monitoring spotřeby CU a diagnostiku výkonu Sparku**? Detailně popište kroky, které provedete pro **optimalizaci Delta tabulek** v Lakehouse a vysvětlete funkci **V-Order** v kontextu čtení dat.

5. **CI/CD a Správa Schematu:** Navrhněte kompletní CI/CD strategii pro Fabric řešení, které zahrnuje **Data Warehouse (schema) a Data Pipelines (kód)**, s přechodem mezi Dev, Test a Prod Workspace. Vysvětlete, jaká je role **Git Integration** a jak se liší od **Deployment Pipelines**. Jak zajistíte, že schéma Data Warehouse je verzováno a nasazeno pomocí standardizovaného artefaktu (**DACPAC**)?

--------------------------------------------------------------------------------

# 📇 Slovníček Klíčových Pojmů (Glossary)

## Tento slovníček obsahuje klíčovou anglickou terminologii (Core Terms a Fráze) z oblastí DP-700 pokrytých ve zdrojích, s českým vysvětlením a citací.

|   |   |   |
|---|---|---|
|Pojem (English)|Definice (Czech)|Reference|
|**Capacity**|Výpočetní výkon (CU - Capacity Units), který určuje dostupnou rychlost zpracování dat a fakturaci v rámci Fabric.||
|**Compute Units (CU)**|Jednotky představující výpočetní výkon, jejichž spotřebu je nutné sledovat (např. pomocí Capacity Metrics App).||
|**Throttling**|Snížení výkonu nebo odmítání úloh systémem, pokud je kapacita (CU) dlouhodobě přetížená.||
|**OneLake**|Jednotné datové jezero ve Fabric, které zajišťuje princip jediné kopie dat (_single copy of data_) a ukládá data ve formátu Delta Parquet.||
|**Delta Parquet**|Otevřený standardní formát pro tabulková data v OneLake, který podporuje ACID transakce, verzování a zajišťuje interoperabilitu mezi enginy.||
|**Shortcuts**|Virtuální odkazy na data uložená jinde (interně v Fabric nebo externě – S3/ADLS Gen2) bez nutnosti fyzické replikace.||
|**SQL Analytics Endpoint**|Read-only T-SQL rozhraní, které umožňuje dotazovat data (Tables) v Lakehouse pomocí T-SQL.||
|**Multi-table Transaction**|Transakce napříč více tabulkami, kterou podporuje Data Warehouse, ale ne Lakehouse, a zajišťuje tak konzistenci dat.||
|**Copy Data Activity**|Klíčová aktivita v Data Pipeline, která slouží primárně pro hromadný přesun dat (ingest) z mnoha zdrojů do Fabric data stores.||
|**Data Gateway**|On-premise komponenta, která je nutná pro připojení **Dataflows Gen2** (a ve Scénářích Copy Data) k datovým zdrojům umístěným v lokální síti organizace.||
|**Metadata-Driven**|Vzorec orchestrace, kde **Data Pipeline** používá aktivity **Lookup** a **ForEach** k dynamickému zpracování mnoha datových sad na základě metadat.||
|**Full Load**|Strategie načítání dat, při které je celá cílová tabulka při každém spuštění přepsána (overwrite).||
|**Incremental Load**|Strategie načítání dat, při které se přenášejí a zpracovávají pouze změněná data (insert, update, delete) od posledního běhu.||
|**MERGE INTO (Delta)**|Delta Lake příkaz používaný v Lakehouse pro efektivní implementaci **UPSERT** operací (vložení/aktualizace/mazání).||
|**SCD Type 2**|Typ pomalu se měnící dimenze, který udržuje **úplnou historii** změn dimenzí vytvořením nového řádku s časovými razítky (`ValidFrom`, `ValidTo`).||
|**Tumbling Window**|Typ časového okna používaného v **Eventstreams** pro agregaci streamovaných dat v pevných, **nepřekrývajících se** časových intervalech.||
|**KQL**|**Kusto Query Language**, jazyk dotazů pouze pro čtení (_read-only request language_) používaný pro filtrování, analýzu a vizualizaci dat v **Eventhouse** (KQL Databáze).||
|**Materialized View**|Předpočítaný pohled na KQL Databázi, který uchovává agregované výsledky, sloužící k dramatickému zrychlení real-time dashboardů a často spouštěných dotazů.||
|**Dynamic Data Masking (DDM)**|Bezpečnostní funkce, která maskuje citlivá data na úrovni **výsledku dotazu** pro neoprávněné uživatele, aniž by data šifrovala.||
|**Row-Level Security (RLS)**|Bezpečnostní funkce, která **omezuje přístup** uživatelů k datům na základě **řádků**.||
|**Capacity Metrics App**|Power BI aplikace pro Capacity Admins, určená ke sledování spotřeby CU, nákladů a detekci **throttlingu**.||
|**V-Order**|Proprietární optimalizace Delta souborů v Lakehouse/DW, která zlepšuje výkon čtení, zvláště u Semantic Models využívajících **Direct Lake**.||
|**OPTIMIZE**|Příkaz pro údržbu Delta tabulek (v Lakehouse), který provádí **kompakci** malých Parquet souborů a zvyšuje rychlost čtení.||
|**VACUUM**|Příkaz pro údržbu Delta tabulek (v Lakehouse), který fyzicky maže staré soubory, které už nejsou potřeba pro time travel (uvolňuje tak místo v úložišti).||
|**DACPAC**|Artefakt (soubor), do kterého se kompilují změny schématu Data Warehouse provedené v **SQL Database Project** (VS Code) pro automatizované nasazení.||
|**Direct Lake**|Nový režim připojení Power BI, který kombinuje rychlost Importu s aktuálností Direct Query čtením dat přímo z Delta souborů v OneLake.||
|**Fallback**|Automatická funkce v režimu **Direct Lake**, kdy se systém přepne na Direct Query, pokud narazí na nepodporovanou operaci (např. složitý DAX nebo View).||
