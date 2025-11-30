# 📅 20denní studijní plán: Microsoft Fabric Data Engineer (DP-700)
[[PLÁN JE JEDNA VĚC (JAK NA NĚJ?)]]

## 🚀 Fáze 1: Základy a architektura (Dny 1–4)

|   |   |   |
|---|---|---|
|Den|Téma|Klíčové Fabric Itemy|
|**1**|Úvod do Fabric a zkoušky|Tenant, Capacity, Workspace|
|**2**|OneLake a úložiště|OneLake, Shortcuts, Delta/Parquet|
|**3**|Lakehouse: Jádro DE|Lakehouse, Files, Tables (Delta)|
|**4**|Data Warehouse (DW)|Warehouse, T-SQL Endpoint, Schemas|

### Den 1: Úvod, rozsah zkoušky a základní koncepty

|   |   |
|---|---|
|Sekce|Obsah|
|**Theory Focus (English)**|**DP-700 Exam Scope & Fabric Hierarchy** The DP-700 exam measures skills across three domains: implementing and managing an analytic solution, ingesting and transforming data, and monitoring and optimizing the solution. Microsoft Fabric is structured hierarchically. The highest level is the **Tenant** (your organization), which hosts **Capacities** (compute resources) that determine the available processing power and billing (F-SKUs). **Workspaces** act as collaborative containers for all Fabric items (Lakehouse, Pipelines, etc.) within a Capacity.|
|**České vysvětlení pojmů**|Zkouška DP-700 pokrývá tři hlavní oblasti: správu a implementaci (např. nastavení zabezpečení), načítání a transformaci dat (např. Pipelines, PySpark, KQL), a sledování výkonu a optimalizace. **Tenant** je Vaše organizace. **Kapacita** (Capacity) je výpočetní výkon (CU - Capacity Units), který platíte. **Workspace** je logický kontejner pro všechny Fabric objekty (items).|
|**Mini-praktická úloha**|Identifikujte ve Vašem testovacím Fabric prostředí, kde se nastavují **Workspace Settings** (např. **Spark settings** nebo **Domains**) a kdo spravuje **Capacity Settings** (Capacity Admin).|
|**Exam-style Question**|_Which Fabric entity primarily determines the available compute power and resource allocation for data processing workloads in your organization?_ (A) Workspace, (B) Item, (C) Capacity, (D) Tenant.|
|**Mikro lekce angličtiny**|**Core Terms:** _Compute_, _Resource Allocation_, _Workload_, _Tenant_. **Fráze:** _Implementing Data Solutions_ (implementace datových řešení), _Ingest and Transform_ (načítání a transformace), _Monitoring and Optimization_ (sledování a optimalizace).|
|**Souhrn a Domácí procvičení (10 min)**|Dnes umíte popsat základní hierarchii Fabricu (Tenant → Capacity → Workspace) a znáte tři hlavní domény zkoušky DP-700. **Domácí úkol:** Projděte si oficiální DP-700 Study Guide (úvodní sekce) a zapište si 5 klíčových nástrojů, které patří do sekce **Ingest and Transform** (např. Notebooks, Pipelines, Dataflows Gen2).|

--------------------------------------------------------------------------------

### Den 2: OneLake a úložiště

|   |   |
|---|---|
|Sekce|Obsah|
|**Theory Focus (English)**|**OneLake and Open Data Format** **OneLake** acts as the single unified data lake for the entire organization (often called "OneDrive for data"). All structured data in OneLake is stored in the open **Delta Parquet** format, which ensures interoperability between different Fabric engines (SQL, Spark, KQL). **Shortcuts** are virtual links that allow accessing data physically stored in external sources (like ADLS Gen2, AWS S3, or Google Cloud Storage) or in another Fabric item, without replicating the data.|
|**České vysvětlení pojmů**|**OneLake** je centrální datové jezero, kde je uložena **jediná kopie dat** (single copy of data), čímž se eliminují datová sila a duplicity. **Delta Parquet** je standardní formát pro tabulková data, který je optimalizovaný pro analýzu a podporuje transakce (ACID) a verzování (time travel). **Shortcuts** slouží k **virtualizaci dat**; odkazují na data v jiném umístění (interním i externím), aniž by je kopírovaly.|
|**Mini-praktická úloha**|Navrhněte, jak byste zpřístupnili historická data, která jsou aktuálně uložena v **Amazon S3** (externí úložiště), do Vašeho Fabric Lakehouse, aniž byste je museli přesouvat (správná volba je **Shortcut**).|
|**Exam-style Question**|_A company wants to unify data access without creating multiple copies across departments. Which core Fabric component enables this "single copy of data" principle?_ (A) Deployment Pipelines, (B) Dataflow Gen2, (C) OneLake, (D) Semantic Model.|
|**Mikro lekce angličtiny**|**Core Terms:** _Unified Data Lake_, _Interoperability_, _Data Virtualization_, _Replication_. **Fráze:** _Single source of truth_ (jediný zdroj pravdy), _Eliminate data silos_ (odstranit datová sila), _Open standard format_ (otevřený standardní formát).|
|**Souhrn a Domácí procvičení (10 min)**|Rozumíte konceptu OneLake a výhodám Delta Parquet formátu. Víte, jak používat **Shortcuts** pro virtualizaci externích dat. **Domácí úkol:** Vyhledejte v dokumentaci, jaké jsou podmínky pro **Shortcut Caching** (caching from S3/GCS) a kdy se data z cache automaticky smažou.|

--------------------------------------------------------------------------------

### Den 3: Lakehouse: Jádro DE

|   |   |
|---|---|
|Sekce|Obsah|
|**Theory Focus (English)**|**Lakehouse Architecture & Usage** The **Lakehouse** is a core data store combining the flexibility of a data lake (storing raw **Files**) and the structure of a data warehouse (managed **Tables** as Delta Parquet). It is primarily operated using the **Spark engine** via **Notebooks** (PySpark, Spark SQL). The Lakehouse provides a **read-only SQL Analytics Endpoint** to query data using T-SQL, offering flexibility for BI tools and analysts. The Lakehouse is the most flexible data store, suitable for unstructured, semi-structured, and structured data, making it ideal for the Bronze and Silver layers of a Medallion Architecture.|
|**České vysvětlení pojmů**|**Lakehouse** je základní úložiště pro datové inženýry, které se dělí na **Files** (pro surová, nestrukturovaná data) a **Tables** (pro Delta tabulky). Nativní jazyk pro Lakehouse je **PySpark/Spark SQL** (přes Notebooky). Lze k němu přistupovat i pomocí T-SQL přes **SQL Analytics Endpoint**. Pro DP-700 je klíčové, že Lakehouse nejlépe podporuje **data science a ML scénáře**.|
|**Mini-praktická úloha**|V Notebooku načtěte surový CSV soubor z **Files** oblasti Vašeho Lakehouse do Spark DataFrame. Přidejte sloupec s aktuálním časem a zapište jej jako novou **Delta tabulku** do sekce **Tables** (např. pomocí `df.write.format("delta").mode("overwrite").saveAsTable(...)`).|
|**Exam-style Question**|_Which capability is uniquely supported by the Lakehouse data store compared to the Warehouse, making it suitable for landing raw log files?_ (A) T-SQL Querying, (B) Row-Level Security, (C) Storing unstructured files in the file section, (D) Multi-table transactions.|
|**Mikro lekce angličtiny**|**Core Terms:** _Raw Data_ (surová data), _Spark Engine_, _Delta Table_, _SQL Analytics Endpoint_. **Fráze:** _Read-only access_ (přístup pouze pro čtení), _Medallion Architecture_ (medailonová architektura), _Unstructured data_ (nestrukturovaná data).|
|**Souhrn a Domácí procvičení (10 min)**|Umíte definovat Lakehouse, znáte jeho dvě části (Files, Tables) a primární jazyk (Spark). **Domácí úkol:** Zjistěte, jaké Delta Lake operace je nutné provádět pravidelně pro optimalizaci Lakehouse tabulek (HINT: Compact files and remove old files).|

--------------------------------------------------------------------------------

### Den 4: Data Warehouse (DW)

|   |   |
|---|---|
|Sekce|Obsah|
|**Theory Focus (English)**|**Warehouse Architecture & T-SQL** The **Data Warehouse** is optimized for structured, tabular data and T-SQL transformations. It is backed by the Polaris (SQL) engine and supports **multi-table transactions**. DW is commonly used for the Gold layer in a Medallion Architecture, providing a robust relational model for BI and advanced security (RLS/CLS). DW supports traditional database objects like tables, views, stored procedures, and schemas. You can ingest data using Data Pipelines, Dataflows, or the **COPY INTO** T-SQL command.|
|**České vysvětlení pojmů**|**Data Warehouse** je postaven na známém jazyce **T-SQL** a je ideální pro BI reporting a dimenzionální modelování. Klíčové výhody: **podpora multi-table transakcí** (Lakehouse ji nepodporuje) a lepší Git/CI-CD integrace přes **SQL Database Projects**. Pro DP-700 je důležité znát příkazy jako **CREATE TABLE AS SELECT (CTAS)** a **COPY INTO** pro efektivní ingest a transformaci.|
|**Mini-praktická úloha**|Vytvořte v DW nový SQL dotaz. Pomocí **CTAS** načtěte data z tabulky `Sales` ve Vašem Lakehouse (pomocí cross-database querying, např. `SELECT * FROM LakehouseName.dbo.SalesTable`) do nové tabulky `DW_Sales_Gold` v Data Warehouse.|
|**Exam-style Question**|_Your team requires full T-SQL support, including multi-table transactions and stored procedures, for the final reporting layer. Which Fabric data store should you choose?_ (A) Eventhouse, (B) Lakehouse, (C) Warehouse, (D) Dataflow Gen2.|
|**Mikro lekce angličtiny**|**Core Terms:** _T-SQL_, _Multi-table Transaction_, _Structured Data_, _Stored Procedure_, _CTAS_. **Fráze:** _Gold Layer_ (zlatá vrstva), _Tabular data_ (tabulková data), _Relational model_ (relační model).|
|**Souhrn a Domácí procvičení (10 min)**|Rozumíte rozdílům mezi Lakehouse (Spark, flexibilní, ML) a Warehouse (T-SQL, transakce, BI). **Domácí úkol:** Zopakujte si, proč **Primary Key constraints** v Data Warehouse ve Fabricu nejsou vynucované (_NOT ENFORCED_) a jaký je jejich skutečný účel.|

--------------------------------------------------------------------------------

## 🚀 Fáze 2: Pohyb a transformace dat (Dny 5–8)

|   |   |   |
|---|---|---|
|Den|Téma|Klíčové Fabric Itemy|
|**5**|Data Pipelines I|Copy Data, Activities, Triggers (Schedule)|
|**6**|Data Pipelines II|Orchestration, Control Flow, Lookup, ForEach|
|**7**|Dataflows Gen2|Power Query (M), Low-Code Transformation, Staging|
|**8**|Rozhodování o Ingestu|Pipeline vs. Dataflow vs. Notebook vs. Mirroring|

### Den 5: Data Pipelines I (Základy a Copy Activity)

|   |   |
|---|---|
|Sekce|Obsah|
|**Theory Focus (English)**|**Data Pipelines & Orchestration** A **Data Pipeline** is the primary tool for orchestration and data movement (ETL/ELT) in Fabric, resembling Azure Data Factory pipelines. Pipelines execute different Fabric items (Notebooks, Dataflows, SQL Scripts) using connected **Activities**. The key activity for ingestion is **Copy Data**, which supports copying data from over 100 sources (including cloud and on-premises via Data Gateway) to Fabric data stores. Pipelines are commonly triggered by a **Schedule** or an **Event**.|
|**České vysvětlení pojmů**|**Data Pipeline** je orchestrátor, který řídí tok dat a spouští jiné Fabric aktivity (např. refresh semantic model). Nejdůležitější je **Copy Data** aktivita pro hromadný přesun dat, která podporuje hybridní scénáře (přes **on-prem data gateway**). Aktivity se propojují pomocí podmínek jako _On Success_, _On Fail_, _On Completion_. Spuštění zajišťují **Triggery** (např. časový plán).|
|**Mini-praktická úloha**|Vytvořte Data Pipeline. Přidejte aktivitu **Copy Data** pro načtení malého souboru z externího ADLS Gen2 do Vašeho Lakehouse. Přidejte aktivitu **Notebook** (Inactive). Propojte Copy Data s Notebookem pomocí podmínky **On Success**.|
|**Exam-style Question**|_A data engineering team needs to move large volumes of batch data from an external Azure SQL Database to a Fabric Lakehouse, followed by a semantic model refresh. Which Fabric item is best suited for this end-to-end orchestration?_ (A) Dataflow Gen2, (B) Fabric Notebook, (C) Data Pipeline, (D) Eventstream.|
|**Mikro lekce angličtiny**|**Core Terms:** _Orchestration_, _Activity_, _Control Flow_, _Schedule Trigger_, _Copy Data_. **Fráze:** _On Success/On Fail_ (při úspěchu/selhání), _Data Movement_ (pohyb dat), _External source_ (externí zdroj).|
|**Souhrn a Domácí procvičení (10 min)**|Umíte definovat, co je pipeline, znáte její klíčové aktivity (Copy Data) a jak propojit kroky. **Domácí úkol:** Zjistěte, jaký je rozdíl mezi **Pipeline Parameters** (přijímané zvenčí) a **Variables** (žijí uvnitř pipeline).|

--------------------------------------------------------------------------------

### Den 6: Data Pipelines II (Pokročilá orchestrace)

|   |   |
|---|---|
|Sekce|Obsah|
|**Theory Focus (English)**|**Advanced Pipeline Control Flow** Complex pipelines often utilize **Control Flow** activities like **Lookup** (to retrieve metadata) and **ForEach** (to iterate over a list or metadata records) to enable **Metadata-Driven Pipelines**. This pattern allows processing many datasets (e.g., 25 tables) using a single Copy Data activity dynamically. For modularity, the **Parent-Child** architecture is used via the **Invoke Pipeline** activity, allowing reusable sub-pipelines (Child) to be called from a main pipeline (Parent).|
|**České vysvětlení pojmů**|**Metadata-Driven Pipelines** umožňují automatizovat ingest stovek tabulek bez nutnosti psát pro každou z nich samostatnou logiku. Klíčové aktivity jsou **Lookup** (načte metadata, např. seznam tabulek) a **ForEach** (iteruje přes seznam). Dynamické výrazy (Dynamic Expressions) jako `@item().SourcePath` se používají uvnitř aktivit pro dynamické určení zdroje a cíle. **Invoke Pipeline** se používá pro volání podřazených (Child) pipeline.|
|**Mini-praktická úloha**|Navrhněte logiku pipeline pro **Metadata-Driven Ingest**: 1. **Lookup** aktivita (simuluje načtení seznamu tabulek). 2. **ForEach** aktivita (iteruje seznam). 3. Uvnitř ForEach aktivita **Copy Data** (používá dynamické výrazy z `@item()`).|
|**Exam-style Question**|_You need to process 50 database tables using a single Data Pipeline. Which set of activities must you combine to achieve a metadata-driven ingestion pattern?_ (A) Copy Data and Notebook, (B) Dataflow Gen2 and ForEach, (C) Lookup and ForEach, (D) Invoke Pipeline and Script.|
|**Mikro lekce angličtiny**|**Core Terms:** _Metadata-Driven_, _Lookup Activity_, _ForEach Loop_, _Invoke Pipeline_, _Dynamic Expression_. **Fráze:** _Iterate over a list_ (iterovat přes seznam), _Reusable component_ (znovupoužitelná komponenta), _Parent-Child pattern_ (vzor Parent-Child).|
|**Souhrn a Domácí procvičení (10 min)**|Zvládáte pokročilou orchestraci pomocí Lookup, ForEach a Invoke Pipeline, a rozumíte, jak navrhnout metadata-driven řešení. **Domácí úkol:** Projděte si, jaké aktivity se používají pro **Notifikace/Error Handling** v pipeline (např. Office 365, Teams) a za jakých podmínek se spouští.|

--------------------------------------------------------------------------------

### Den 7: Dataflows Gen2

|   |   |
|---|---|
|Sekce|Obsah|
|**Theory Focus (English)**|**Dataflows Gen2 (DFG2) & Low-Code ETL** **Dataflows Gen2** is a **low-code/no-code** ETL tool powered by the **Power Query (M language)** engine. It offers over 300 built-in connectors and is excellent for business analysts or teams preferring a visual transformation interface. DFG2 supports both **append and replace** methods for updates, though support may vary by destination. A key feature is **Fast Copy**, which leverages the high-throughput Copy Data infrastructure for ingestion. DFG2 is often used as an activity within a Data Pipeline for better orchestration and monitoring.|
|**České vysvětlení pojmů**|**Dataflows Gen2** je nízko-kódový ETL nástroj, který používá rozhraní Power Query (M jazyk). Je ideální pro rychlé **transformace s minimem kódu**. Lze ho použít pro **on-premise zdroje** pomocí Data Gateway. **Fast Copy** umožňuje rychlý zápis do cílů (Lakehouse/Warehouse) s využitím Copy Data enginu. Pro DP-700 je klíčové, že DFG2 se hodí pro scénáře, které **minimalizují vývojové úsilí** (_minimize development effort_).|
|**Mini-praktická úloha**|Vytvořte Dataflow Gen2. Použijte Power Query k načtení dat z veřejného CSV zdroje. Přidejte transformační krok, např. **Group By** nebo **Convert Text to Upper Case**. Nastavte cílovou destinaci (Destination) do Vašeho Lakehouse.|
|**Exam-style Question**|_Which Fabric tool allows data ingestion from over 300 connectors, supports on-premises sources via Data Gateway, and minimizes coding effort, making it ideal for business analysts?_ (A) Fabric Notebook, (B) Data Pipeline, (C) Dataflow Gen2, (D) KQL Queryset.|
|**Mikro lekce angličtiny**|**Core Terms:** _Low-Code/No-Code_, _Power Query_, _M language_, _On-Premise Sources_, _Data Gateway_. **Fráze:** _Visual transformation interface_ (vizuální transformační rozhraní), _Minimize development effort_ (minimalizovat vývojové úsilí).|
|**Souhrn a Domácí procvičení (10 min)**|Rozumíte, kdy použít DFG2 (low-code, on-prem, rychlé transformace). **Domácí úkol:** Popište, jak byste orchestraci pro DFG2 řešili efektivněji než jen manuálním spouštěním (HINT: Vložení DFG2 jako aktivity do Data Pipeline).|

--------------------------------------------------------------------------------

### Den 8: Rozhodování o Ingestu

|   |   |
|---|---|
|Sekce|Obsah|
|**Theory Focus (English)**|**Ingestion Decision Guide** Choosing the right tool depends on complexity, volume, required skillset, and latency. **Data Pipeline** is for orchestration and movement (batch). **Dataflow Gen2** is for low-code ETL (batch, on-prem). **Notebooks (Spark)** are for complex, custom transformations, large volume, and custom API integration (full code). **Shortcuts** and **Database Mirroring** are for data virtualization, minimizing ETL effort entirely. **Mirroring** provides a near real-time replica of supported databases (Azure SQL, Snowflake) in Delta Parquet format.|
|**České vysvětlení pojmů**|Klíčové kritérium: **Skillset** (SQL, PySpark/Python, M/Low-code) a **Komplexita transformace**. Fráze _„minimalizovat vývojové úsilí“_ obvykle směřuje k low-code nástrojům (Dataflow, Pipeline) nebo virtualizaci (Shortcut, Mirroring). **Mirroring** se hodí pro _near real-time_ replikaci podporovaných OLTP databází do Fabricu, čímž eliminuje potřebu psát ETL procesy.|
|**Mini-praktická úloha**|**Scénář:** Tým má silné Python dovednosti a potřebuje provést komplexní validaci schématu příchozích dat. Jaký nástroj zvolíte? (Odpověď: **Notebook** s Python knihovnami jako Great Expectations).|
|**Exam-style Question**|_A company wants to ingest data from an on-premises SQL Server and needs to apply moderate transformations using a low-code approach. Which tool is the appropriate choice?_ (A) Fabric Notebook, (B) Database Mirroring, (C) Data Pipeline with Copy Data, (D) Dataflow Gen2.|
|**Mikro lekce angličtiny**|**Core Terms:** _Mirroring_, _Latency_, _Skillset_, _Custom Transformation_, _Near Real-time_. **Fráze:** _Data Replication_ (replikace dat), _Full code solution_ (řešení založené na plném kódu), _Decision guide_ (rozhodovací průvodce).|
|**Souhrn a Domácí procvičení (10 min)**|Jste schopni vybrat správný nástroj pro ingest dat do Fabric na základě kritérií (kód, složitost, zdroj, rychlost). **Domácí úkol:** Porovnejte, jak se liší přístup k datům u **Shortcut** (virtuální odkaz) a **Mirroring** (near real-time replika).|

--------------------------------------------------------------------------------

## 🚀 Fáze 3: Spark, PySpark a Modely (Dny 9–12)

|   |   |   |
|---|---|---|
|Den|Téma|Klíčové Fabric Itemy|
|**9**|Notebooks a Spark Basics|Notebooks, Magic Commands, notebookutils|
|**10**|Spark konfigurace a optimalizace|Starter Pool, Custom Pool, High Concurrency|
|**11**|Loading Patterns & PySpark|Full Load, Incremental Load, MERGE|
|**12**|Dimenzionální modelování|Star Schema, SCD Type 2, Surrogate Keys|

### Den 9: Notebooks a Spark Basics

|   |   |
|---|---|
|Sekce|Obsah|
|**Theory Focus (English)**|**Notebooks and PySpark** **Notebooks** are code-based tools, the "Swiss army knife" of Data Engineering, primarily using the Spark engine. They support multiple languages per cell using **Magic Commands** (e.g., `%%sql` for Spark SQL, `%%pyspark`). **Notebooks can be parameterized** to accept external values when executed via Pipeline or `notebookutils`. The **notebookutils** library is essential for common tasks like orchestrating other notebooks (`notebook.run_multiple`), reading secrets, and file system operations.|
|**České vysvětlení pojmů**|**Notebooky** jsou nejuniverzálnější nástroj, kde píšete kód (primárně **PySpark** pro práci s daty ve Sparku). **Magic Commands** (např. `%%sql`) Vám umožní přepínat jazyk v rámci jedné buňky. **Parametrizace** buňky (Parameter Cell) je klíčová pro dynamické spouštění kódu. Knihovna **notebookutils** je důležitá pro komunikaci s Fabric (např. spouštění jiných notebooků nebo správa souborů).|
|**Mini-praktická úloha**|V Notebooku načtěte DataFrame s daty. V jedné buňce použijte **%%sql** **magic command** pro provedení jednoduchého `SELECT COUNT(*)`. V další buňce použijte **PySpark** k vykonání téže operace a porovnejte výsledky.|
|**Exam-style Question**|_Which built-in Python library in Fabric Notebooks is designed to streamline common tasks such as accessing secrets from Azure Key Vault and orchestrating other notebooks?_ (A) Pandas, (B) MLFlow, (C) notebookutils, (D) Semantic Link.|
|**Mikro lekce angličtiny**|**Core Terms:** _Parameter Cell_, _Magic Command_, _PySpark_, _DataFrame_, _Exit Value_. **Fráze:** _Streamline common tasks_ (zefektivnit běžné úkoly), _Execution context_ (kontext spuštění), _Run multiple_ (spustit více).|
|**Souhrn a Domácí procvičení (10 min)**|Rozumíte Notebookům, jak parametrizovat kód a znáte základní funkce `notebookutils`. **Domácí úkol:** Nastudujte si rozdíl mezi spuštěním notebooku pomocí **%run** (stejný kontext) a **notebookutils.notebook.run(...)** (jiný kontext).|

--------------------------------------------------------------------------------

### Den 10: Spark konfigurace a optimalizace

|   |   |
|---|---|
|Sekce|Obsah|
|**Theory Focus (English)**|**Spark Configuration and Pools** Fabric provides a default **Starter Pool** for fast startup (under 10 seconds), which is sufficient for most smaller/interactive workloads. For demanding jobs, you must configure a **Custom Spark Pool** (allowing changes in node size, autoscale, executor range), although this increases startup time. The setting **High Concurrency** allows multiple notebooks or jobs running concurrently for one user/pipeline to share the same underlying Spark session, optimizing resource usage. **Environments** are Fabric assets used to manage Spark configurations and install custom Python libraries.|
|**České vysvětlení pojmů**|**Starter Pool** (výchozí) je rychlý, ale omezený pro velké objemy dat a konkurenci. Pro náročné úlohy se používá **Custom Spark Pool**, kde můžete definovat velikost uzlů (nodes) a alokaci jader. **High Concurrency** je klíčové nastavení, které umožňuje sdílení jedné Spark Session mezi více Notebooky (např. spuštěnými z jedné Pipeline). **Environments** se používají k verzování Spark nastavení a Python knihoven.|
|**Mini-praktická úloha**|Identifikujte, kde ve **Workspace Settings** se spravují **Custom Spark Pool** a **Environments**. Nastudujte, jaké parametry můžete u custom poolu měnit (např. _node size_, _autoscale_).|
|**Exam-style Question**|_A production data solution experiences performance bottlenecks due to long Spark cluster startup times for batch jobs. The jobs are large and complex. What feature should the engineer configure to optimize resources while accommodating the high load?_ (A) Enable High Concurrency on the Starter Pool, (B) Create a Custom Spark Pool with optimized node settings, (C) Disable the Autoscale feature, (D) Use notebookutils for parallel execution.|
|**Mikro lekce angličtiny**|**Core Terms:** _Spark Pool_, _Node Size_, _Autoscale_, _Executor_, _High Concurrency_. **Fráze:** _Customization of Spark settings_ (přizpůsobení nastavení Sparku), _Dynamic allocation_ (dynamická alokace), _Share the same session_ (sdílet stejnou relaci).|
|**Souhrn a Domácí procvičení (10 min)**|Znáte rozdíly mezi Spark Pooly a víte, co je **High Concurrency** a k čemu slouží **Environments**. **Domácí úkol:** Zjistěte, jaký je hlavní dopad **Custom Spark Pool** na čas spouštění (HINT: Je delší než u Starter Poolu).|

--------------------------------------------------------------------------------

### Den 11: Loading Patterns & PySpark

|   |   |
|---|---|
|Sekce|Obsah|
|**Theory Focus (English)**|**Loading Patterns: Full vs Incremental** Synchronization between source and Fabric can be achieved via **Full Load** (overwrite all data, simple but costly for large tables) or **Incremental Load** (only load changed data, faster but complex implementation). **Incremental Loading** in Spark/PySpark is typically implemented using the **Delta Lake MERGE** command, which handles inserts, updates, and deletes (UPSERTs) based on key matching. This requires tracking a **watermark** (e.g., a timestamp or sequence number) from the source.|
|**České vysvětlení pojmů**|**Full Load** (plné načtení) přepíše cílovou tabulku pokaždé (např. `mode("overwrite")` v PySpark). **Incremental Load** (přírůstkové načtení) je efektivnější, vyžaduje ale sledování _watermarku_ (poslední zpracovaný čas/ID). Pro implementaci přírůstkového načítání v Lakehouse je klíčový příkaz **Delta MERGE INTO** (obdoba UPSERT).|
|**Mini-praktická úloha**|Napište kód pro jednoduchý **Full Load** (overwrite) v PySpark: načtěte data do DataFrame a zapište je do Lakehouse s režimem **mode("overwrite")**.|
|**Exam-style Question**|_A Data Engineer needs to efficiently synchronize a large source table with a Delta table in Lakehouse, ensuring that new, updated, and deleted rows are handled in a single operation. Which Delta Lake command provides this functionality?_ (A) COPY INTO, (B) UNION ALL, (C) MERGE INTO, (D) VACUUM.|
|**Mikro lekce angličtiny**|**Core Terms:** _Incremental Load_, _Full Load_, _Watermark_, _Merge Into_, _UPSERT_. **Fráze:** _Data synchronization_ (synchronizace dat), _Handle inserts, updates, and deletes_ (zpracovat vložení, aktualizace a mazání).|
|**Souhrn a Domácí procvičení (10 min)**|Rozumíte rozdílu mezi full a incremental loading a víte, že MERGE INTO je klíčový pro UPSERT operace v Lakehouse. **Domácí úkol:** Zjistěte, jak se v T-SQL ve Warehouse provádí operace, která odpovídá PySpark `MERGE INTO`.|

--------------------------------------------------------------------------------

### Den 12: Dimenzionální modelování

|   |   |
|---|---|
|Sekce|Obsah|
|**Theory Focus (English)**|**Dimensional Modeling and SCD Type 2** DP-700 requires knowledge of dimensional modeling concepts (Star Schema, Fact and Dimension tables). **Surrogate Keys** (system-generated integers) are used in dimension tables instead of **Natural Keys** (source IDs) to support historical tracking and protect against source system changes. **Slowly Changing Dimensions (SCD)** describe how to handle changes in dimension attributes. **SCD Type 2** tracks full history by creating a new row for every change, using `ValidFrom` and `ValidTo` timestamps or an `IsCurrent` flag.|
|**České vysvětlení pojmů**|**Dimenzionální modelování** (Star Schema) je klíčové pro analytiku. **Surrogate Keys** (náhradní klíče) se používají pro zajištění unikátnosti řádků a sledování historie. **SCD Type 2** (pomalu se měnící dimenze typu 2) se používá, když potřebujeme **zachovat celou historii** změn atributu (např. adresa zákazníka). Nový řádek se vytvoří, starý se "uzavře" (ValidTo). **SCD Type 3** sleduje jen **poslední změnu** (např. `PreviousCountry`).|
|**Mini-praktická úloha**|Navrhněte schéma pro dimenzi `DimCustomer` (SCD Type 2). Které sloupce musí obsahovat pro sledování historie? (HINT: `SurrogateKey`, `NaturalKey`, `ValidFrom`, `ValidTo`/`IsCurrent`).|
|**Exam-style Question**|_A dimension table tracks customer location changes. The requirement is to maintain a full history of all past and current addresses for accurate historical reporting. Which type of Slowly Changing Dimension (SCD) should be implemented?_ (A) SCD Type 0, (B) SCD Type 1, (C) SCD Type 2, (D) SCD Type 3.|
|**Mikro lekce angličtiny**|**Core Terms:** _Dimensional Model_, _Star Schema_, _Fact Table_, _Dimension Table_, _Surrogate Key_, _Natural Key_, _SCD Type 2_. **Fráze:** _Maintain full history_ (zachovat celou historii), _Temporal analysis_ (časová analýza), _Data Integrity_ (datová integrita).|
|**Souhrn a Domácí procvičení (10 min)**|Rozumíte dimenzionálním základům a víte, jak implementovat (konceptuálně) SCD Type 2 pro sledování historie. **Domácí úkol:** Zjistěte, jakým způsobem se ve Fabric DW generují Surrogate Keys, když DW nepodporuje _Identity_ sloupce.|

--------------------------------------------------------------------------------

## 🚀 Fáze 4: Real-Time a Security (Dny 13–16)

|   |   |   |
|---|---|---|
|Den|Téma|Klíčové Fabric Itemy|
|**13**|Real-Time Analytics I|Eventstreams, Sources, Destinations|
|**14**|Real-Time Analytics II|KQL Database, KQL Basics, Materialized Views|
|**15**|Security I|Workspace/Item Roles, Dynamic Data Masking (DDM)|
|**16**|Security II|RLS, OLS, CLS (T-SQL vs OneSecurity)|

### Den 13: Real-Time Analytics I (Eventstreams)

|   |   |
|---|---|
|Sekce|Obsah|
|**Theory Focus (English)**|**Eventstreams and Streaming Data** **Real-time systems** process data continuously with low latency, suitable for telemetry, logs, and IoT. **Eventstreams** is the no-code/low-code tool for processing and routing streaming data in Fabric. It supports sources like Azure Event Hubs/IoT Hub and custom HTTP endpoints. Key operations include **Filtering**, **Aggregating** over **Time Windows** (Tumbling, Hopping, Sliding), and directing data to destinations like **Eventhouse (KQL DB)**, **Lakehouse**, or **Data Activator**. **Spark Structured Streaming** is the code-based alternative for complex streaming transformations.|
|**České vysvětlení pojmů**|**Eventstreams** je vizuální nástroj, který pomáhá s ingestem, lehkou transformací a přesměrováním streamovaných dat. Můžete definovat **časová okna** (Time Windows) pro agregace: **Tumbling** (nepřekrývající se), **Hopping** (překrývající se). Data se typicky ukládají do **Eventhouse (KQL DB)** pro real-time analýzu. Pro komplexní, kódové transformace se používá **Spark Structured Streaming**.|
|**Mini-praktická úloha**|**Scénář:** Potřebujete vypočítat průměrnou teplotu senzoru každou celou minutu. Jaký typ **Time Window** použijete pro tuto pevnou, nepřekrývající se agregaci? (Odpověď: **Tumbling Window**).|
|**Exam-style Question**|_A solution requires low-code ingestion and transformation of telemetry data coming from Azure Event Hubs, with the goal of writing aggregated results to a KQL Database. Which Fabric item should be used?_ (A) Data Pipeline with Notebook Activity, (B) Dataflow Gen2, (C) Eventstreams, (D) Spark Structured Streaming.|
|**Mikro lekce angličtiny**|**Core Terms:** _Streaming Data_, _Latency_, _Tumbling Window_, _Hopping Window_, _Event Hubs_, _Time-Series_. **Fráze:** _Real-time analytics_ (analýza v reálném čase), _Source/Destination_ (zdroj/cíl), _Unbounded table_ (neomezená tabulka - koncept Spark Streaming).|
|**Souhrn a Domácí procvičení (10 min)**|Rozumíte real-time scénářům, roli Eventstreams a typům časových oken. **Domácí úkol:** Zjistěte, kdy je vhodné zvolit **Spark Structured Streaming** namísto Eventstreams (HINT: Když je vyžadována velká komplexita transformací a kód).|

--------------------------------------------------------------------------------

### Den 14: Real-Time Analytics II (KQL Database a KQL)

|   |   |
|---|---|
|Sekce|Obsah|
|**Theory Focus (English)**|**KQL Database and KQL Basics** **Eventhouse** is the container for **KQL Databases**, which are optimized for log and time-series data using the Kusto Query Language (KQL). The KQL database manages data through **Retention** (how long data is kept) and **Caching** policies (hot vs. cold data). **KQL** is the read-only query language used for fetching, filtering, and analyzing this data. Key KQL operators include `take`, `project` (select columns), `where` (filter), and `summarize` (aggregation, similar to SQL `GROUP BY`). **Materialized Views** store pre-computed aggregation results for faster reporting.|
|**České vysvětlení pojmů**|**Eventhouse** je kontejner pro **KQL Databáze**. KQL DB je ideální pro data, kde záleží na čase (time-series) a rychle se mění. **KQL (Kusto Query Language)** je čtecí jazyk pro dotazování těchto dat; dotazy se řetězí pomocí operátoru `|
|**Mini-praktická úloha**|Napište jednoduchý KQL dotaz pro fiktivní tabulku `SensorLogs`: Chcete zobrazit prvních 10 řádků a pouze sloupce `SensorID` a `Temperature`. (HINT: `SensorLogs|
|**Exam-style Question**|_A KQL database table contains millions of log entries. You need to create a pre-computed aggregation to speed up a real-time dashboard query that frequently calculates the daily average temperature. Which KQL feature should you use?_ (A) KQL Function, (B) Materialized View, (C) Update Policy, (D) Retention Policy.|
|**Mikro lekce angličtiny**|**Core Terms:** _Kusto Query Language (KQL)_, _Eventhouse_, _Retention Policy_, _Caching Policy_, _Materialized View_. **Fráze:** _Read-only request language_ (jazyk pro dotazy pouze pro čtení), _Time-series data_ (data časových řad), _Pre-computed results_ (předpočítané výsledky).|
|**Souhrn a Domácí procvičení (10 min)**|Chápete strukturu Eventhouse, znáte základní KQL operátory (`project`, `summarize`, `take`) a víte, proč se používají Materialized Views. **Domácí úkol:** Zjistěte, jaké jsou **hlavní limity** T-SQL při dotazování KQL databáze ve srovnání s KQL.|

--------------------------------------------------------------------------------

### Den 15: Security I (Základní přístupy a maskování)

|   |   |
|---|---|
|Sekce|Obsah|
|**Theory Focus (English)**|**Workspace and Item-Level Access** Access control uses the **Principle of Least Privilege**. **Workspace roles** (Admin, Member, Contributor, Viewer) control broad permissions over all items in the workspace. **Viewer** role can read data via SQL endpoints but cannot run pipelines. **Item-level access** grants permissions only to a specific item (e.g., one Data Warehouse) without granting access to the whole workspace. **Dynamic Data Masking (DDM)** hides sensitive information (e.g., salaries, emails) at the query result level for non-privileged users, without changing the underlying data.|
|**České vysvětlení pojmů**|Cílem je vždy použít **nejmenší nutná práva** (Principle of Least Privilege). Práva se definují buď na úrovni **Workspace** (platí pro vše uvnitř), nebo na úrovni **Item** (pouze pro konkrétní objekt). **Viewer** role umožňuje pouze čtení dat. **Dynamic Data Masking (DDM)** maskuje citlivá data (např. email) při zobrazení (např. `MASKED WITH (FUNCTION = 'email()')`), ale nejedná se o plnohodnotné bezpečnostní opatření, protože jej lze obejít.|
|**Mini-praktická úloha**|**Scénář:** Uživatel potřebuje vidět necitlivá data z tabulky `Employee` ve Warehouse, ale nechcete, aby viděl e-mailové adresy. Navrhněte DDM masku pro sloupec `Email`.|
|**Exam-style Question**|_You need to prevent non-administrative users from viewing full email addresses in a financial table, but the original data must remain unencrypted. Which security feature should you implement in the Data Warehouse?_ (A) Row-Level Security, (B) Column-Level Security, (C) Dynamic Data Masking, (D) Object-Level Security.|
|**Mikro lekce angličtiny**|**Core Terms:** _Least Privilege_, _Access Control_, _Viewer Role_, _Dynamic Data Masking_, _Sensitive Information_. **Fráze:** _Hide sensitive data_ (skrýt citlivá data), _Query result level_ (na úrovni výsledku dotazu), _Unencrypted data_ (nešifrovaná data).|
|**Souhrn a Domácí procvičení (10 min)**|Znáte role ve Workspace a umíte definovat DDM. **Domácí úkol:** Zjistěte, jaké jsou čtyři podporované maskovací funkce pro DDM v T-SQL (HINT: default, email, random, partial).|

--------------------------------------------------------------------------------

### Den 16: Security II (RLS, OLS, CLS)

|   |   |
|---|---|
|Sekce|Obsah|
|**Theory Focus (English)**|**Granular Access Control** **Row-Level Security (RLS)** restricts data access based on user identity or role (e.g., a sales rep only sees their own sales records). In T-SQL (Warehouse/SQL Endpoint), RLS is implemented using a **Table-Valued Function (TVF)** and a **Security Policy**. **Object-Level Security (OLS)** controls access to entire tables or objects via `GRANT SELECT`. **Column-Level Security (CLS)** controls access to specific columns via `GRANT SELECT (Column1, Column2)`. Fabric is moving towards a unified **OneSecurity** model to apply RLS/CLS across all engines (Spark, SQL).|
|**České vysvětlení pojmů**|**RLS (Zabezpečení na úrovni řádků)** filtruje řádky podle toho, kdo se dotazuje (např. pomocí `USER_NAME()`). **OLS/CLS (Objektové/Sloupcové zabezpečení)** se aplikuje pomocí příkazu **GRANT SELECT** na konkrétní tabulky nebo sloupce. U Warehouse/SQL Endpointu se RLS implementuje pomocí T-SQL (TVF + Security Policy). DP-700 klade důraz na implementaci RLS/CLS, které jsou nejčastěji nutné v Gold vrstvě.|
|**Mini-praktická úloha**|**Scénář:** Potřebujete, aby se uživatelům skupiny `Finance` zobrazily pouze sloupce `InvoiceID` a `Amount` z tabulky `FactOrders`. Napište zjednodušený příkaz CLS. (Odpověď: `GRANT SELECT (InvoiceID, Amount) ON FactOrders TO Finance;`).|
|**Exam-style Question**|_A team wants to ensure that users in the Sales group can only view the sales orders where the 'SalesRep' column matches their own username. Which feature should be implemented?_ (A) Dynamic Data Masking, (B) Object-Level Security, (C) Column-Level Security, (D) Row-Level Security.|
|**Mikro lekce angličtiny**|**Core Terms:** _Row-Level Security (RLS)_, _Column-Level Security (CLS)_, _Object-Level Security (OLS)_, _Table-Valued Function (TVF)_, _Security Policy_. **Fráze:** _Granular access control_ (detailní řízení přístupu), _Restrict data access_ (omezit přístup k datům), _Apply the policy_ (aplikovat politiku).|
|**Souhrn a Domácí procvičení (10 min)**|Znáte všechny úrovně zabezpečení DW (DDM, RLS, CLS/OLS) a víte, jak se RLS implementuje pomocí TVF a Security Policy. **Domácí úkol:** Zjistěte, co je **OneSecurity** a jaký je jeho budoucí cíl (HINT: Sjednocení zabezpečení RLS/CLS napříč Spark a SQL enginy).|

--------------------------------------------------------------------------------

## 🚀 Fáze 5: Governance, Monitoring a Finální Příprava (Dny 17–20)

|   |   |   |
|---|---|---|
|Den|Téma|Klíčové Fabric Itemy|
|**17**|Governance a Data Quality|Endorsement, Sensitivity Labels, Lineage, Domains|
|**18**|Deployment a CI/CD|Git Integration, Deployment Pipelines, SQL Database Projects|
|**19**|Monitoring a Optimalizace|Monitoring Hub, Capacity Metrics, V-Order, Query Optimization|
|**20**|Semantic Models a Exam Prep|Semantic Models, Direct Lake, DAX Basics, Exam Strategy|

### Den 17: Governance a Data Quality

|   |   |
|---|---|
|Sekce|Obsah|
|**Theory Focus (English)**|**Data Governance Features** **Endorsements** help users find trusted data items. There are three types: **Promoted** (recommended by item creator), **Certified** (meets organizational quality standards, requires specific permissions), and **Master Data** (core enterprise data source, highest trust level). **Sensitivity Labels** (managed via Purview) protect data based on its confidentiality (e.g., Confidential) and can automatically apply to downstream items. **Lineage View** provides a visual map of data flow and dependencies within a workspace. **Domains** are used to logically group Workspaces based on organizational structure.|
|**České vysvětlení pojmů**|**Endorsements** (doporučení) zvyšují důvěru v data: **Promoted** (propagováno) je nejnižší úroveň; **Certified** (certifikováno) znamená splnění firemních standardů; **Master Data** je nejvyšší úroveň důvěryhodnosti. **Sensitivity Labels** (štítek citlivosti) se používají k ochraně informací (např. _Confidential_) a synchronizují se s Microsoft Purview. **Lineage View** je klíčový pro sledování **závislostí dat** a dopadové analýzy (Impact Analysis).|
|**Mini-praktická úloha**|**Scénář:** Váš kolega vytvořil Dataflow, který by měl být široce sdílen, ale ještě neprošel formálním auditem kvality. Jaký typ Endorsement mu doporučíte? (Odpověď: **Promoted**).|
|**Exam-style Question**|_Which endorsement type in Microsoft Fabric is typically reserved for data items that meet organizational quality standards and require approval from a dedicated team?_ (A) Master Data, (B) Promoted, (C) Certified, (D) Verified.|
|**Mikro lekce angličtiny**|**Core Terms:** _Endorsement_, _Sensitivity Label_, _Master Data_, _Certified_, _Lineage View_, _Domain_. **Fráze:** _Organizational standards_ (organizační standardy), _Downstream item_ (následný/závislý objekt), _Impact analysis_ (dopadová analýza).|
|**Souhrn a Domácí procvičení (10 min)**|Znáte role Endorsementů a Lineage View pro governance. **Domácí úkol:** Zjistěte, jaké nástroje se v Pythonu používají pro pokročilou **Validaci schématu dat** na vstupu (HINT: Great Expectations).|

--------------------------------------------------------------------------------

### Den 18: Deployment a CI/CD

|   |   |
|---|---|
|Sekce|Obsah|
|**Theory Focus (English)**|**CI/CD and Deployment** **Version Control** in Fabric is achieved via **Git Integration** (Azure DevOps or GitHub), which stores item metadata (Notebook code, Pipeline structure). **Deployment Pipelines** allow manual or automated promotion of Fabric items across stages (Dev → Test → Prod) by comparing content between workspaces. Git integration is _not mandatory_ for Deployment Pipelines. **SQL Database Projects** offer an alternative method to deploy Data Warehouse schema changes. Changes are made locally (e.g., in VS Code), compiled into a **DACPAC** artifact, and deployed using a connection string.|
|**České vysvětlení pojmů**|**Git Integrace** (Version Control) se používá k verzování kódu a struktury Fabric objektů (kromě dat). **Deployment Pipelines** (Kanály nasazení) automaticky porovnávají a posouvají objekty mezi prostředími (stages - Dev, Test, Prod). **Deployment Pipelines a Git integrace jsou oddělené funkce**. **SQL Database Projects** jsou důležité pro automatizované nasazení schématu Data Warehouse. Lokální změny se kompilují do souboru **DACPAC**, který reprezentuje databázové schéma.|
|**Mini-praktická úloha**|**Scénář:** Právě jste dokončili Data Pipeline (Dev) a chcete ji posunout do Test prostředí. Jaký Fabric nástroj použijete pro tento automatizovaný přesun (promotion)? (Odpověď: **Deployment Pipeline**).|
|**Exam-style Question**|_A data engineer has modified a Data Warehouse schema locally using VS Code. To deploy the schema changes to the Production environment, the engineer must first compile the project into which specific artifact type?_ (A) JSON, (B) SQL Script, (C) DACPAC, (D) .FABRIC file.|
|**Mikro lekce angličtiny**|**Core Terms:** _Deployment Pipeline_, _Git Integration_, _Version Control_, _Stage_, _DACPAC_, _SQL Database Project_. **Fráze:** _Promotion of content_ (posun obsahu), _Compare changes_ (porovnat změny), _Schema deployment_ (nasazení schématu).|
|**Souhrn a Domácí procvičení (10 min)**|Víte, jak se nasazují změny pomocí Deployment Pipelines a SQL Database Projects. **Domácí úkol:** Zjistěte, co se **NEverzionuje** v Gitu (HINT: Data, Credentials, Refresh Schedules).|

--------------------------------------------------------------------------------

### Den 19: Monitoring a Optimalizace

|   |   |
|---|---|
|Sekce|Obsah|
|**Theory Focus (English)**|**Monitoring and Optimization** **Monitoring Hub** is the central dashboard for tracking all runs (Pipelines, Notebooks, Dataflows, Semantic Model Refreshes). **Capacity Metrics App** is a Power BI report used by Capacity Admins to monitor **CU consumption**, identify overages, and detect **throttling**. For Data Warehouse optimization, **Query Activity tab** and **Query Insights** views track long-running or frequently executed T-SQL queries. **V-Order** is a proprietary optimization applied to Delta files in Lakehouse/DW, improving read performance (especially for Direct Lake). Delta table maintenance includes **OPTIMIZE** (compacts small files) and **VACUUM** (removes old files).|
|**České vysvětlení pojmů**|**Monitoring Hub** je primární místo pro kontrolu stavu všech spuštění. **Capacity Metrics App** slouží ke sledování nákladů a spotřeby (CU usage), a k identifikaci **throttlingu** (snížení výkonu při přetížení). Pro DW optimalizaci je klíčové sledování **Long-running queries**. **V-Order** je optimalizace souborů pro rychlejší čtení (zvláště pro Direct Lake). V Lakehouse se pro údržbu používá **OPTIMIZE** (kompakce) a **VACUUM** (mazání starých souborů, uvolnění místa).|
|**Mini-praktická úloha**|**Scénář:** Reporty Power BI nad Vaším Lakehouse jsou pomalé. Který příkaz byste spustili v Notebooku, abyste zlepšili výkon čtení Delta tabulky sloučením malých souborů? (Odpověď: **OPTIMIZE**).|
|**Exam-style Question**|_A data engineer is debugging a recurring performance issue caused by heavy CU usage and resource contention. Which tool provides detailed insight into capacity consumption across all workloads and helps detect throttling?_ (A) Monitoring Hub, (B) Lineage View, (C) Capacity Metrics App, (D) Query Activity Tab.|
|**Mikro lekce angličtiny**|**Core Terms:** _Monitoring Hub_, _Capacity Unit (CU)_, _Throttling_, _V-Order_, _Optimize_, _Vacuum_, _Query Insights_. **Fráze:** _Resource contention_ (konkurence zdrojů), _Long-running query_ (dlouho běžící dotaz), _Compacting files_ (kompakce souborů).|
|**Souhrn a Domácí procvičení (10 min)**|Znáte monitorovací nástroje na úrovni Item (Monitoring Hub) a Capacity (Capacity Metrics App). Umíte navrhnout údržbu DW (V-Order) a Lakehouse (`OPTIMIZE`, `VACUUM`). **Domácí úkol:** Zjistěte, které typy chyb (např. připojení, dynamické výrazy) se nejlépe diagnostikují v panelu **Inputs/Outputs** v detailu Pipeline Run.|

--------------------------------------------------------------------------------

### Den 20: Semantic Models a Finální Příprava

|   |   |
|---|---|
|Sekce|Obsah|
|**Theory Focus (English)**|**Semantic Models and Direct Lake** **Semantic Models** (formerly Datasets) are the backend for Power BI Reports, defining relationships, metrics, and DAX calculations. **Direct Lake** is the preferred connection mode in Fabric, combining the speed of Import mode with the currency of Direct Query. Direct Lake reads data directly from Delta Parquet files in OneLake. If Direct Lake cannot process a query (e.g., due to unsupported DAX or Views), it automatically **falls back to Direct Query**. **DAX** (Data Analysis Expressions) is the language used for defining measures and calculated columns in the model.|
|**České vysvětlení pojmů**|**Semantic Models** (Sémantické modely) obsahují logiku modelu (relace, DAX). **Direct Lake** je klíčová inovace, která umožňuje BI reportům číst data přímo z Delta tabulek (OneLake) s extrémní rychlostí a **bez nutnosti refreshů** (data jsou vždy čerstvá). Pokud Direct Lake narazí na limit, provede se **Fallback** (přepnutí) na Direct Query. **DAX** je jazyk pro definování metrik.|
|**Mini-praktická úloha**|**Scénář:** Váš report používá Direct Lake, ale data z Lakehouse se právě aktualizovala. Musíte reportu zajistit nejaktuálnější data. Musíte ručně refreshovat sémantický model? (Odpověď: Ne, Direct Lake čte automaticky čerstvá data).|
|**Exam-style Question**|_Which Power BI storage mode in Fabric combines the performance of Import mode with the ability to query the latest data directly from Delta Parquet files in OneLake?_ (A) Direct Query, (B) Live Connection, (C) Import, (D) Direct Lake.|
|**Mikro lekce angličtiny**|**Core Terms:** _Semantic Model_, _Direct Lake_, _Direct Query_, _Import Mode_, _Fallback_, _DAX_. **Fráze:** _Currency of data_ (aktuálnost dat), _Read directly from Delta_ (číst přímo z Delta), _Calculated measures_ (vypočítané míry).|
|**Souhrn a Domácí procvičení (10 min)**|Rozumíte roli Semantic Modelů a výhodám Direct Lake (rychlost, aktuálnost). **Finální úkol:** Projděte si **Strategii zkoušky DP-700**: časový management (1 minuta na otázku), kdy používat Learn dokumentaci a jak přistupovat k Case Study. **GRATULACE! Jste připraven/a na závěrečný test.**|

--------------------------------------------------------------------------------

## 🧮 Průběžné mikro-hodnocení (Micro-assessment)

Po dnech 4, 8, 12 a 16 provedeme krátké hodnocení. V praxi to znamená, že mi na konci těchto dnů položíte otázky typu: _„Pochopil/a jsem správně, že pro inkrementální loading je v Lakehouse klíčový MERGE INTO, zatímco DW používá STORED PROCEEDURES a T-SQL?“_

Na základě Vašich odpovědí a případných nejasností **dynamicky přizpůsobím** obsah následující fáze, abychom se zaměřili na Vaše slabší místa.

**Motivace:** Pamatujte, že Data Engineering je základem moderního BI a AI, a poptávka po těchto dovednostech neustále stoupá. Váš strukturovaný přístup k DP-700 Vám dává nejen certifikaci, ale hlavně ucelenou _strukturu pro studium a učení_. Vydržte, jde Vám to skvěle!

# [[PLÁN JE JEDNA VĚC (JAK NA NĚJ?)]]
## 🎯 Srovnání studijních zdrojů pro DP-700

|   |   |   |
|---|---|---|
|Zdroj|Silné stránky (DP-700 Focus)|Slabé stránky (DP-700 Focus)|
|**Microsoft Learn** (Oficiální moduly, dokumentace)|**Pokrytí teorie (Vysoké)**, Oficiální **anglická terminologie**. Nutné pro získání případného slevového voucheru.|**Praxe/Realismus (Nízké)**. Moduly nejsou _dostatečné_ ke složení zkoušky. Chybí hloubka pro rozhodování ("kdy co použít").|
|**Fabric Dojo** (Placené moduly 3/13)|**Reálné scénáře (Vysoké)**, **Hyperkondenzovaný** obsah, cílená příprava na orchestraci, CI/CD, Eventhouse. Obsahuje **hands-on tutoriály** a Q&A.|Pokrytí je omezené na zakoupené moduly.|
|**Hands-on labs / Sandbox**|**Praktické procvičení (Klíčové)**. Zkouška vyžaduje **hands-on zkušenost** s Pipelines, Lakehouse, Spark, KQL a security.|Neposkytuje strukturu ani teoretické vysvětlení.|
|**Certas.com** (Practice Questions)|**Exam-style otázky (Vysoké)**. Poskytuje custom-made otázky s vysvětlením, které jsou podobné otázkám v reálném testu.|Nepokrývá teorii.|
|**YouTube Kanály** (Např. Aleksi Partanen, Ansh Lamba, Will Needham)|**Hloubka teorie i praxe (Vysoká)**. Nabízí kompletní série s _teorií_, _hands-on demy_ a _exam-like otázkami_ v každém díle.|Může trvat dlouho (např. 11hodinový kurz), nutná pečlivá filtrace relevantních témat.|

--------------------------------------------------------------------------------

## 🥇 Kombinace a Prioritní Strategie (20 dní)

Vzhledem k časovému limitu a potřebě posílit praktické dovednosti i angličtinu musím 70 % času věnovat praxi a 30 % cílené teorii a terminologii.

### I. Priorita 1: Praktické procvičení a rozhodování (70 % času)

Základem pro úspěch u DP-700 je schopnost **rozhodnout se, který nástroj kdy použít**.

|   |   |   |
|---|---|---|
|Zdroj|Doporučená aktivita (Denně)|Proč|
|**Váš 20denní Plán**|Plňte **Mini-praktické úlohy** a **Domácí procvičení** v testovacím Fabric Workspace.|Ověření znalostí v praxi. Např. implementace **MERGE INTO** pro inkrementální loading.|
|**YouTube Série / Placené Moduly**|Sledujte **cílené hands-on tutoriály/dema** k aktuálnímu tématu (např. Den 13: Eventstreams dema, Den 16: RLS implementace v DW).|Umožňuje vidět reálné implementační detaily a slyšet klíčovou anglickou terminologii.|
|**Certas.com**|Denně **10–15 practice questions** k modulům, které jste ten den studoval/a (např. DP-700 Modul 1: Ingest, Modul 2: Lakehouse).|Posiluje **rozhodovací mindset** a přípravu na _exam-style_ otázky.|
|**GitHub / Sandboxy**|Stáhněte si **kódové ukázky** (např. Python notebooky pro **Great Expectations** validaci nebo CI/CD scénáře s **SQL Database Project**).|Získejte praktické zkušenosti s řešením "full code" scénářů.|

### II. Priorita 2: Cílená Teorie a Terminologie (30 % času)

Zaměřte se na detaily, které dělají rozdíl mezi Lakehouse a Warehouse a na anglické fráze.

|   |   |   |
|---|---|---|
|Zdroj|Doporučená aktivita (Denně)|Proč|
|**Váš 20denní Plán**|Pečlivé prostudování **Theory Focus (English)** a **Mikro lekce angličtiny**.|Přímá příprava na anglickou terminologii a porozumění kontextu zkoušky.|
|**Microsoft Learn Dokumentace**|Vyhledejte a studujte jen **rozhodovací průvodce** (_Decision Guides_) – např. srovnání Lakehouse vs. Warehouse vs. KQL Database nebo volbu nástrojů Pipeline vs. Dataflow Gen2 vs. Spark.|Poskytuje formální, oficiální a detailní informace nutné pro zkoušku.|
|**Fabric Dojo** (3 moduly)|Zaměřte se na moduly pokrývající **Deployment Pipelines, Version Control (Git)** a **Granulární Security (RLS/CLS)**.|Tyto pokročilé organizační/správní témata jsou často v testu a vyžadují přesnou znalost terminologie.|

--------------------------------------------------------------------------------

## ⏱️ Denní Rozvrh (Poměr Teorie vs. Praxe)

Využijte strukturu z 20denního plánu a alokujte čas následujícím způsobem:

|   |   |   |
|---|---|---|
|Časová Alokace|Aktivita|Zaměření|
|**30 min**|**Teorie + Terminologie**|Prostudujte **Theory Focus (English)** a **České vysvětlení** k danému dni. Zaměřte se na **Core Terms** a **Fráze** (např. _High Concurrency, Multi-table transactions, Low-Code_).|
|**70 min**|**Praktické Demos & Hands-on**|Sledujte tutoriály nebo provádějte **Mini-praktické úlohy** (kódování v Notebooku, nastavení Copy Data, KQL dotaz). Důraz na reálné nastavení a **chybové stavy**.|
|**20 min**|**Testování Znalostí**|10–15 practice questions na Certas.com a řešte **Exam-style questions** z denního plánu.|

--------------------------------------------------------------------------------

## 🚫 Co Přeskočit (Optimalizace času)

Protože máme pouze 20 dní, měli byste se vyhnout aktivitám s nízkou návratností času:

1. **Aplikace znalostí, které nejsou primárně v DP-700:** Přeskočte hloubkové kurzy Power BI Reportingu a DAX (DAX není v DP-700, zaměřte se jen na **Semantic Model** a **Direct Lake** koncepty).

2. **Čtení celých Learn modulů:** Nestravujte celý obsah modulů od Microsoft Learn (protože "nejsou dostatečné na složení zkoušky"). Používejte je jen jako **rychlý referenční zdroj** a pro potvrzení terminologie.

3. **Hluboké ladění Python/PySpark syntaxe:** Nepište složité Python/Pandas transformace od nuly. Místo toho se zaměřte na **integraci Sparku do Fabricu** (Notebooks, `notebookutils`, `%%sql`) a **Delta operace (****MERGE INTO****,** **OPTIMIZE****)**.

4. **Nepotřebné T-SQL detaily:** Zopakujte si klíčové T-SQL příkazy pro DW (např. **CTAS**, **COPY INTO**), ale vyhněte se cvičení, která se silně zaměřují na detaily klasických SQL serverů, které Fabric DW nepodporuje (např. vynucené Primary Keys).

Váš největší nepřítel je čas. Musíte **kombinovat teorii s okamžitou praktickou aplikací**, protože zkouška testuje, zda chápete _dopady_ Vašich architektonických rozhodnutí v reálném Fabric prostředí. Držte se striktně poměru 70:30 (Praxe:Teorie).