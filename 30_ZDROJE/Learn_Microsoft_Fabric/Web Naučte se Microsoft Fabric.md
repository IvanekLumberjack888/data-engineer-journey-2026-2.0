# 🚀 Why you should watch this course! - Fabric Foundation Microsoft Fabric
https://www.skool.com/microsoft-fabric/classroom/d154aad4?md=8abba5d02fa241aab9af28a738319f8d

---

## Klíčové výstupy kurzu

- **Získáte dobré porozumění tomu, co je Microsoft Fabric, jaké problémy řeší a jak je řeší**
    
- **Uvědomíte si obrovskou příležitost, kterou Fabric přináší jak pro vaši organizaci, tak pro vás osobně ve vaší kariéře**
    

---

## Struktura kurzu

- **První část:** Případová studie, která ukazuje problémy v infrastruktuře a workflow, jež Fabric řeší.
    
- **Druhá část:** Základní pojmy, které musíte znát:
    
    - _OneLake_ (jednotné datové jezero)
        
    - _Sedm klíčových zkušeností_ s Fabric
        
    - _Čtyři výpočetní enginy_
        
- **Podrobnější prozkoumání:** Sedm hlavních oblastí práce s Fabric
    

---

## Pro koho je kurz určen

- **Začátečníci s Fabric:** Pokud jste o Fabric jen slyšeli nebo zatím nemáte hlubší znalosti
    
- **První uživatelé Fabric:** Pokud jste s Fabric začali pracovat a chcete získat lepší základy
    
- **Power BI vývojáři:** Pokud chcete zjistit, co Fabric přináší vám i vaší firmě
    
- **Datoví profesionálové:** Pokud pracujete s nástroji jako Snowflake, Databricks a chcete poznat Fabric
    
- **Manažeři:** Pokud potřebujete porozumět Fabric pro rozhodování nebo účast v diskusi (není nutné být praktický uživatel)
    

---

## Styl výuky

- **Nejsou předpokládány žádné vstupní znalosti**
    
- **Kurz je plný praktických příkladů pro lepší pochopení platformy Fabric**
    

---

## Představuje se autor kurzu

- **Will Needham:** Více než 8 let zkušeností jako datový profesionál (BI, Data Science, Real-time Analytics, Data Engineering, Data Warehousing)
    
- **Konzultant pro data strategii, architekturu a datové inženýrství v Microsoft Azure stacku**
    
- **Zakladatel YouTube kanálu Learn Microsoft Fabric a Skool komunity**
    
- **Plně se věnuje vzdělávání v oblasti Microsoft Fabric**
    

---

Tento kurz **pokrývá všechny klíčové aspekty Microsoft Fabric** — od důvodů vzniku přes hlavní koncepty až po praktické využití pro různé role v datové oblasti. Vhodné pro úplné začátečníky, pokročilé uživatele Power BI, datové inženýry i manažery, kteří potřebují o Fabric rozhodovat nebo ho vysvětlit jiným. Každá část je doplněna praktickými ukázkami a autor je připraven se podělit o své bohaté zkušenosti.

1. [https://www.skool.com/microsoft-fabric/classroom/d154aad4?md=8abba5d02fa241aab9af28a738319f8d](https://www.skool.com/microsoft-fabric/classroom/d154aad4?md=8abba5d02fa241aab9af28a738319f8d)
   
---
---

# 🚀 The story of Houston Electrics – Fabric Foundation

---

## Úvod: Jak vznikají problémy v datové infrastruktuře (příběh Houston Electrics)

- Houston Electrics je **fiktivní firma** (internetový prodejce elektrotechniky), která rychle rostla a chtěla být inovativní díky práci s daty.
    
- V roce 2015 najala prvního **Chief Data Officer** a spustila digitální transformaci: založila centrální datové oddělení (přes 50 lidí), investovala do cloudových technologií (Azure, AWS) a začala používat Power BI.
    

---

## Realita: Organický růst způsobuje problémy

- Firma má několik technických oddělení, **každé používá jiné technologie na správu a analýzu dat**.
    
- Data se mezi odděleními **kopírují, transformují** – vzniká spousta datových sil.
    
- Na příkladu workflow recenzí zákazníků:
    
    - Recenze se ukládají v Azure SQL databázi.
        
    - Data engineering tým buduje pipeline, která každé ráno kopíruje data do data lake.
        
    - Data science tým provádí sentiment analýzu, výsledky ukládá do další složky v data lake.
        
    - BI tým z Power BI sděluje výsledky produktovému týmu.
        
    - _Jeden workflow – čtyři technologie, čtyři formáty, všude kopie dat._
        

---

## Hlavní problémy ve firmě

- **Mnoho datových sil:** Oddělení mají vlastní kopie dat, špatná integrace.
    
- **Stovky pipeline:** Data engineering tým jen kopíruje data mezi odděleními, pipeline často selhávají, údržba zabírá většinu času.
    
- **Proprietární formáty:** Data science týmu trvá dlouho připravit data – různé formáty, není jistota kvality ani aktuálnosti.
    
- **Rozdílná uživatelská zkušenost:** Každý systém má jiné ovládání, nové zaměstnance trvá měsíce zaučit.
    
- **Různá pravidla pro přístup, bezpečnost, governance:** IT oddělení složitě spravuje přístupy a zabezpečení, každá technologie je jiná.
    
- **Složitá a nepředvídatelná fakturace:** Každý produkt má jiné licencování a model účtování, pro IT je těžké predikovat náklady.
    

---

## Shrnutí: Proč je to relevantní pro Microsoft Fabric

- **Fabric vznikl zejména kvůli nutnosti sjednotit a zjednodušit data infrastrukturu**, aby:
    
    - odstranil datová sila a kopie,
        
    - vytvořil jednotné formáty,
        
    - sjednotil uživatelskou zkušenost,
        
    - zjednodušil governance, zabezpečení a billing.
        

Tento příběh vysvětluje, **jaké typické problémy ve firmách Fabric řeší** – sjednocení datové platformy, snížení komplexity a údržby, zvýšení efektivity práce s daty napříč organizací.

1. [https://www.skool.com/microsoft-fabric/classroom/d154aad4?md=cd17025fb2be4fb4b85cb257693e8a31](https://www.skool.com/microsoft-fabric/classroom/d154aad4?md=cd17025fb2be4fb4b85cb257693e8a31)
   
---
---

# 🚀 How Fabric is different – Fabric Foundation

---

## Jak se Microsoft Fabric liší od starých datových platforem

- V rámci Fabric je celá rodina datových produktů rozdělená do čtyř hlavních oblastí:
    
    - Data ingestion (samoobslužné načítání dat)
        
    - Data storage (ukládání dat)
        
    - Data engineering (datové inženýrství)
        
    - Data science & business intelligence
        

---

## Největší mýty o Fabric

- Častý omyl: Fabric je „jen přemalovaný Power BI nebo stávající technologie“. **Ve skutečnosti byl vyvinut úplně od základu** – odpovídá na klíčové problémy, které mají firmy se správou dat.
    

---

## Hlavní inovace Fabric

1. **OneLake ruší datová sila**
    
    - Veškerá firemní data jsou v jednom místě – OneLake.
        
    - _Konec kopírování dat mezi odděleními._
        
2. **Jediná kopie datasetu**
    
    - Každý dataset existuje v systému pouze na jednom místě, ostatní týmy data pouze „odkazují“ pomocí Shortcuts.
        
3. **Jednotný otevřený formát – Delta Parquet**
    
    - Všechny tabulková data jsou ukládána v OneLake v Delta Parquet formátu – usnadňuje integraci mezi týmy i technologiemi.
        
4. **Jednotné rozhraní pro všechny role**
    
    - Přihlašujete se do stejných webových stránek (podobné Microsoft 365), všechny součásti Fabric vypadají a ovládají se velmi podobně.
        
    - Zvyšuje efektivitu – neřešíte rozdíly mezi platformami.
        
5. **Jednotný způsob správy přístupů a bezpečnosti**
    
    - Všechna oprávnění a bezpečnostní politiky jsou spravovány jednotně přes Workspaces.
        
    - Zjednodušená správa napříč celou organizací.
        
6. **Lepší governance a dohledatelnost**
    
    - Všechna data jsou snadno dohledatelná, governance je centrální.
        
    - Fabric nabízí vestavěné funkce pro správu datasetů.
        
7. **Jedno monitorovací centrum**
    
    - Fabric Monitoring Hub monitoruje veškerou infrastrukturu na jednom místě.
        
8. **Zjednodušené billing/licence**
    
    - Stačí koupit kapacitu Fabric a máte přístup ke všem funkcím – žádné další produkty/licence.
        
    - Power BI Premium capcity lze využít i pro Fabric.
        

---

**Shrnutí:**  
Fabric znamená sjednocení, otevřenost, jednoduchost a efektivitu pro celou datovou organizaci. Vše je postaveno tak, aby zmizely datová sila, složitá správa, duplicity a problémy s integrací dat mezi týmy.

1. [https://www.skool.com/microsoft-fabric/classroom/d154aad4?md=214c577eb0334ea993d4dfa4120296cb](https://www.skool.com/microsoft-fabric/classroom/d154aad4?md=214c577eb0334ea993d4dfa4120296cb)
   
---
---
# 🚀 Fundamental concepts in Fabric – Fabric Foundation

---

## Hlavní koncepty v Microsoft Fabric

- Většina uživatelů **nepracuje přímo s OneLake** – hlavní aktivita probíhá v tzv. „experiencích“ Fabricu.
    

---

## Co je „Fabric experience“?

- Experience je **seskupení nástrojů podle rolí**.
    
- Každá role v datové oblasti má svůj vlastní set: například Data Engineering experience obsahuje vše, co potřebuje datový inženýr.
    

---

## Sedm základních „experiencí“ v Microsoft Fabric

- **Data Factory** – stavba pipelines a transformace dat
    
- **Data Warehouse** – transakční datový sklad pro strukturovaná data (SQL)
    
- **Data Engineering** – nástroje pro datové inženýrství, Lakehouse, notebooky
    
- **Data Science** – nástroje pro ML experimenty, modelování, notebooky
    
- **Real-time Analytics** – zpracování a ukládání dat v reálném čase (KQL engine)
    
- **Power BI** – BI reporty pro vizualizaci dat
    
- **Data Activator** – automatizace akcí podle vzorců v datech (např. spouštění workflow při detekci události v datech)
    

---

## 4 výpočetní enginy Fabricu

- **SQL engine** – pro Data Warehouse, umí T-SQL
    
- **Spark engine** – pro Data Engineering/Data Science, umí Python (PySpark), R, Scala, SparkSQL
    
- **KQL engine** – pro Real-time Analytics (dotazy v KQL)
    
- **Analysis Services engine** – pro Power BI
    

---

## Princip: Oddělení úložiště od výpočtu

- **Uživatel pracuje s jednotlivými experiences**
    
- **Výpočetní engine působí jako překladač mezi uživatelem/UI a úložištěm (OneLake)**
    
- Například SQL engine vezme SQL dotaz, převede ho na dotaz do Delta tabulek v OneLake, vrátí výsledek do Data Warehouse UI.
    

---

Tento koncept **umožňuje jednotnou správu dat, snadné zabezpečení** i governance napříč všemi datovými platformami a rolemi v organizaci. Každý engine je optimalizován pro jiné uživatelské scénáře a typy datových úloh.

1. [https://www.skool.com/microsoft-fabric/classroom/d154aad4?md=1ad2fc9aa60f4bd08608e2dedba75893](https://www.skool.com/microsoft-fabric/classroom/d154aad4?md=1ad2fc9aa60f4bd08608e2dedba75893)

---
---

# 🚀 Data Factory experience – Fabric Foundation

---

## Hlavní zaměření Data Factory v Microsoft Fabric

- **Jádro:** Pohyb a transformace dat (ETL – Extract, Transform, Load).
    
- **Klíčový scénář:** Přenést nová data do Fabric, např. z externího API nebo firemních systémů.
    
- **Podobnost s:** Azure Data Factory, Synapse Pipelines, Power BI Data Flow (Gen 1).
    
- **Určeno pro:** Enterprise škálu – zvládne velké objemy dat i vysokou frekvenci obnovení.
    

---

## Hlavní objekty v Data Factory experience

- **Data Pipelines:** Orchestrace zpracování dat – např. spuštění Fabric Notebooku podle plánu, volání uložených procedur, přenos dat do Fabric.
    
- **Dataflows:** No-code/low-code nástroj s Power Query rozhraním – umožňuje napojit přes 300 zdrojů dat, transformovat je a zapsat do Lakehouse či Data Warehouse v rámci Fabric.
    

---

## Pro koho je Data Factory určena

- **Datoví inženýři**
    
- **Vývojáři Power BI**
    

---

## Další zdroje k tématu

- Data Factory – high-level video overview
    
- Dataflows v Fabric – přehled
    
- Novinky v Data Factory (YouTube)
    
- Nejčastější scénáře pro data pipeline (YouTube)
    
- Kompletní end-to-end projekt s Dataflows
    

---

Data Factory je hlavním místem v rámci Fabric pro orchestraci a automatizaci pohybu dat napříč všemi dalšími částmi platformy. Otevírá jednoduchý i robustní způsob jak budovat ETL procesy s minimem kódu i v enterprise prostředí.

1. [https://www.skool.com/microsoft-fabric/classroom/d154aad4?md=2ca9b39c8f24466983f937038c1ac962](https://www.skool.com/microsoft-fabric/classroom/d154aad4?md=2ca9b39c8f24466983f937038c1ac962)

---
---

# 🚀## Data Engineering experience – Fabric Foundation

---

## Hlavní účel Data Engineering v Microsoft Fabric

- Umožňuje **návrh, stavbu a správu infrastruktury a systémů**, které podporují organizaci při sběru, ukládání, zpracování a analýze velkých objemů dat.
    
- Příklady podobných nástrojů: **Azure Data Lake Services (ADLS Gen2), Databricks, Snowflake**.
    

---

## Klíčové objekty Data Engineering experience

- **Lakehouse**: Kombinace datového jezera a skladiště – umožňuje ukládat nestrukturovaná data (soubory) a pomocí notebooků je převádět na strukturované tabulky.
    
- **Fabric Notebook**: Skriptovací prostředí pro data engineering úlohy (čištění, validace dat atd.), podporuje Python, R a Scala, běží na Apache Spark.
    
- **Data Pipeline**: Orchestrace datových workflow (automatizované kroky i napojení na další části Fabric).
    
- **Spark job definition**: Definice úloh pro Spark cluster (vstupní/výstupní data, transformace, nastavení běhu apod.).
    

---

## Pro koho je určena

- **Datoví inženýři** – hlavní cílová skupina tohoto pracovního prostoru.
    

---

## Další zdroje a doporučení

- Videoprůvodce: „Lakehouse Complete Guide (YouTube)“
    
- Dokumentace: Přehled Data Engineering v Microsoft Fabric
    

---

Tato „experience“ je základní stavební kámen pro datové inženýry ve Fabric, kde vytváří a spravují datovou architekturu, připravují data pro analytické i BI scénáře, často ve spolupráci s dalšími rolemi v datovém týmu.

1. [https://www.skool.com/microsoft-fabric/classroom/d154aad4?md=ebfe2960e1c5457da278f9e45a9b4205](https://www.skool.com/microsoft-fabric/classroom/d154aad4?md=ebfe2960e1c5457da278f9e45a9b4205)

---
---

# 🚀## Data Warehouse experience – Fabric Foundation

---

## Hlavní účel Data Warehouse v Microsoft Fabric

- Poskytuje **transakční datový sklad** se vším, co od něj čekáte:
    
    - tabulky, schémata, pohledy, uložené procedury
        
    - dotazování přes známý jazyk **T-SQL**
        
- Nabízí podporu **low-code/no-code**: Analytici mohou využívat vizuální skripty pro snazší práci.
    
- Je **“lake-centric”** – vše běží na vysoce škálovatelné architektuře, je optimalizované pro libovolně velké datové objemy.
    
- Není to klasický SQL Server, ale můžete používat T-SQL.
    

---

## Podobné nástroje

- Synapse SQL Serverless/Dedicated
    
- Snowflake
    

---

## Klíčové objekty Data Warehouse experience

- **Data Warehouse** – vlastní datový sklad, postavený na enginu Polaris (distribuovaný SQL engine).
    

---

## Pro koho je určena

- Správci databází
    
- Datoví inženýři
    
- Datoví analytici
    

---

## Další zdroje a doporučení

- Kompletní video-průvodce „Fabric Data Warehouse Complete Guide (YouTube)“
    

---

Tento pracovní prostor v rámci Fabric je ideální pro ty, kdo chtějí stavět škálovatelné, transakční datové sklady s moderní architekturou napojenou na celé Fabric prostředí a OneLake.

1. [https://www.skool.com/microsoft-fabric/classroom/d154aad4?md=51f72a7d6a5f483baefac215d9cf426e](https://www.skool.com/microsoft-fabric/classroom/d154aad4?md=51f72a7d6a5f483baefac215d9cf426e)