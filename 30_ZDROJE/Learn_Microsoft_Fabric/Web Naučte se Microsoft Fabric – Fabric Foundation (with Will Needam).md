# **#️⃣ INTRODUCTION**
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

# 🚀 Data Warehouse experience – Fabric Foundation

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

---
---

# 🚀Data Science experience – Fabric Foundation

---

## Hlavní účel Data Science v Microsoft Fabric

- **Kompletní workflow pro data science v rámci firmy:**
    
    - Průzkum dat
        
    - Příprava a čištění dat
        
    - Experimentování a modelování
        
    - Scoring a nasazení modelů
        
    - Publikace prediktivních výstupů do Power BI reportů
        

---

## Co je možné tvořit v Data Science experience

- **Notebooky** – hlavní nástroj pro exploraci dat a tvorbu kódu (Python, R). Používají se na zkoušení dat, experimenty a trénování ML modelů.
    
- **Experimenty** – přesná evidence a logování trénovacích procesů v ML (parametry, verze kódu, metriky z běhu modelu). Používají MLFlow pro tracking experimentů.
    
- **ML Modely** – správa a sledování verzí modelů během experimentování, možnost registrace a review díky MLFlow.
    

---

## Komu je určena

- **Data scientists** – hlavní cílová skupina této části.
    

---

## Podobné nástroje

- Azure Machine Learning
    
- Synapse Notebooks
    
- Databricks Notebooks
    

---

## Doporučené zdroje

- Dokumentace Data Science experience v Microsoft Fabric (learn.microsoft.com)
    
- Průvodce MLFlow (mlflow.org)
    
- Přehled ML modelů ve Fabric (learn.microsoft.com)
    

---

Data Science experience ve Fabric integruje všechny nástroje potřebné pro celý životní cyklus machine learningu, od explorace až po nasazení výsledků do BI reportů — s trackováním a správou modelů i experimentů.

1. [https://www.skool.com/microsoft-fabric/classroom/d154aad4?md=7a6f319fbdae478ba52d771376128a9b](https://www.skool.com/microsoft-fabric/classroom/d154aad4?md=7a6f319fbdae478ba52d771376128a9b)

---
---

# 🚀 Real-time Intelligence experience – Fabric Foundation

---

## Hlavní účel Real-time Intelligence v Microsoft Fabric

- **Nástroje pro ingest, správu a analýzu real-time event dat**  
    (např. data ze senzorů, logovacích systémů, streamů).
    

---

## Klíčové inovace a objekty

- **Eventstream:**  
    No-code nástroj pro registraci, zpracování a směrování streamovaných dat ke správným cílům ve Fabric.
    
- **KQL Database:**  
    Datové úložiště pro streamovaná data, postavené na enginu KQL (Kusto Query Language), stejně jako Azure Data Explorer.
    
- **KQL Queryset:**  
    Sada dotazů nad KQL databází, využívající jazyk KQL (vhodné pro analýzu logů, telemetrie apod.).
    

---

## Komu je určena

- Datoví inženýři
    
- IoT inženýři
    
- Real-time data specialisté
    

---

## Podobné technologie

- Azure Data Explorer
    
- Azure Event Hubs
    
- Azure Stream Analytics
    

---

## Doporučené zdroje

- [Real-Time Intelligence experience v Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/real-time-analytics/overview)
    

---

Real-time Intelligence experience umožňuje bezkódově napojit streamované zdroje dat, ukládat je v KQL databázích, analyzovat v reálném čase a rychle reagovat na události v datech. Ideální prostředí pro IoT, telemetry a všechny scénáře, kde jsou data generována a zpracovávána „za běhu“.

1. [https://www.skool.com/microsoft-fabric/classroom/d154aad4?md=de978916ad734d7db83e9518a4375915](https://www.skool.com/microsoft-fabric/classroom/d154aad4?md=de978916ad734d7db83e9518a4375915)

---
---

# 🚀 Power BI experience – Fabric Foundation

---

## Hlavní účel Power BI ve Fabric

- **Power BI** je BI řešení od Microsoftu pro tvorbu reportů a vizualizaci datových poznatků pro business uživatele.
    
- Umožňuje vytvářet přehledné, interaktivní reporty a sdílet je v rámci firmy.
    

---

## Podobné nástroje

- Tableau
    
- Looker
    

---

## Klíčové objekty Power BI experience

- **Reports** – uživatelsky přívětivé BI reporty poskytující vizuální pohled na klíčová data a trendy.
    
- **Semantic models** (dříve: Datasets) – vše, co tvoří „back-end“ reportu v Power BI (tabulky, relace, metriky, DAX výpočty atd.).
    

---

## Pro koho je určena

- Business uživatelé (konzumace reportů)
    
- Power BI vývojáři (tvorba a správa reportů/datových modelů)
    
- Datoví analytici (analýzy, vizualizace)
    

---

## Doporučené zdroje

- [Oficiální dokumentace Power BI](https://learn.microsoft.com/en-us/power-bi/fundamentals/power-bi-overview)
    

---

Power BI experience je hlavní BI/analytická vrstva Microsoft Fabric, umožňuje firmám snadno sdílet data, vizualizace a analýzy napříč organizací přes moderní interaktivní uživatelské rozhraní.

1. [https://www.skool.com/microsoft-fabric/classroom/d154aad4?md=41390a874171415f9908a13023b95ebd](https://www.skool.com/microsoft-fabric/classroom/d154aad4?md=41390a874171415f9908a13023b95ebd)

---
---

# 🚀 Data Activator experience – Fabric Foundation

---

## Hlavní účel Data Activator v Microsoft Fabric

- **No-code prostředí pro automatické spouštění akcí** při detekci vzorců nebo podmínek ve měnících se datech.
    
    - Typické akce: spuštění automatizace (např. Power Automate) při splnění podmínky.
        
    - Sleduje data v Power BI reportech nebo v event streamech (Real-time Intelligence).
        

---

## Podobné nástroje

- IFTTT
    
- Zapier
    

---

## Klíčový objekt: Reflex

- **Reflex**: je centrum Data Activatoru, zde definujete:
    
    - _Objekty_ – co chcete monitorovat (reálná nebo virtuální entita, např. návštěvy webu).
        
    - _Vlastnosti_ – konkrétní sledovaná metrika (např. počet návštěv za hodinu).
        
    - _Spouštěče_ – hodnoty/vzorce, které vyvolají akci (např. návštěvnost nad 1000/hod).
        
    - _Akce_ – co se má stát (např. odeslání emailu, spuštění workflow).
        

---

## Komu je určeno

- Business uživatelé
    
- Power BI vývojáři
    

---

## Doporučený zdroj

- Praktický tutorial: [Data Activator na ukázkových datech](https://learn.microsoft.com/en-us/fabric/data-activator/data-activator-tutorial)
    

---

Data Activator je určen k **automatizaci reakcí na data** bez nutnosti programování – umožňuje okamžité spouštění akcí při zjištění definovaného vzorce či podmínky v datech. Ideální pro monitoring, alerty a propojení s automatizačními platformami napříč Fabric.

1. [https://www.skool.com/microsoft-fabric/classroom/d154aad4?md=aec580787fdd44708b5057ac53246a0f](https://www.skool.com/microsoft-fabric/classroom/d154aad4?md=aec580787fdd44708b5057ac53246a0f)

---
---

# 🚀Zdroje k Microsoft Fabric – sekce „More resources“

---

## Odkazy od Microsoftu:

- Produktové oznámení: aka.ms/fabric
    
- Digitální event Build (videa): aka.ms/build-with-analytics
    
- Produktový web: aka.ms/microsoft-fabric
    
- Dokumentace: aka.ms/fabric-docs
    
- E-book k Fabric: aka.ms/fabric-get-started-ebook
    
- Microsoft Learn moduly: aka.ms/learn-fabric
    
- End-to-end scénáře a tutoriály: aka.ms/fabric-tutorials
    
- Fabric Notes: aka.ms/fabric-notes
    

---

## Osobní doporučení na kvalitní zdroje:

- **Azure Synapse YouTube channel**: Série Fabric Espresso, videa s členy produktového týmu Microsoft Fabric – praktické ukázky funkcí.
    
- **Advancing Analytics YouTube channel**: Skvělý pro témata Lakehouse a Spark engine ve Fabric.
    
- **KratosBI YouTube channel**: Obsah o Fabric, zejména série Fabric Fridays (praktické příklady a tipy).
    
- **Tales from the Field YouTube channel**: Diskuze a roundupy z komunity Fabric (Microsoft zaměstnanci).
    
- **Fabric.guru**: Hloubkové technické rozbory od Sandeep Pawar.
    
- **Data Mozart**: Zaměřuje se hlavně na Power BI + DP-600 Fabric certifikace (skvělý obsah pro analytiky).
    
- **Blog Sam Debruyn**: Široká škála datových témat, poslední dobou hlavně o Fabric.
    

---

## Co zde najdete?

Tahle sekce obsahuje strhující výběr **oficiálních dokumentací, kurzů, e-booků, tutoriálů i komunitních blogů a YouTube kanálů**, které jsou ideální k dalšímu rozvoji ve světě Microsoft Fabric. Vhodné pro všechny role: od datových inženýrů přes BI analytiky až po tech leadery – podle preferovaného stylu učení (video, praktický projekt, dokumentace).

Pokud se chceš v Microsoft Fabric rychle orientovat a být „v obraze“, tyhle zdroje ti pomůžou na maximum.

1. [https://www.skool.com/microsoft-fabric/classroom/d154aad4?md=8f94805aed254571837ed1304df5e6c1](https://www.skool.com/microsoft-fabric/classroom/d154aad4?md=8f94805aed254571837ed1304df5e6c1)
   
---
---

# **#️⃣ MORE DETAILED TRANSITION GUIDE**

# 🚀 Shrnutí videa „From Power BI to Microsoft Fabric: your ULTIMATE transition guide (FULL SERIES)“

(Pokračování ve stejném duchu – série Learn Microsoft Fabric s Willem Needhamem)

---

## Hlavní myšlenky série

- **Cíl série:** Naučit tě přechod od Power BI-centric architektury k Fabric-centric architektuře – všechny klíčové rozhodovací body, které řešíš při migraci analytického řešení do Fabric.
    
- Série pokrývá celý proces od začátku do konce:
    
    - Strategie práce se workspace a řízení přístupu
        
    - Způsoby získávání dat: ingestion vs mirroring vs shortcuts
        
    - Výběr správy dat: data pipeline vs dataflow vs notebook
        
    - Architektura a výběr datového úložiště: lakehouse, data warehouse, KQL database
        
    - Zajištění kvality dat
        
    - Připojení Power BI na Fabric (inc. DirectLake)
        
    - End-to-end migrační projekt na reálných datech
        

---

## Hlavní body videa

- **Rozdíl mezi Power BI-centric a Fabric-centric architekturou:**
    
    - v Power BI-centric každé zpracování dat, transformace a ingest probíhá „izolovaně“ v Power BI dataflow nebo Power Query.
        
    - ve Fabric-centric architektuře se data ukládají do Fabric (Lakehouse, Data Warehouse, KQL DB) a následně se načítají do Power BI reportů – rozšiřuje možnosti analytiky, governance i integrace s AI/ML.
        
- **Klíčové rozhodovací body přechodu:**
    
    - Jak správně organizovat workspaces (dostupnost, přístupová práva na úrovni workspace, objektu, tabulky, řádku).
        
    - Strategie pro data access: ingestion, mirroring (replikace třeba Azure SQL do Fabric), shortcuts (odkaz na externí storage).
        
    - Nástroje Fabric pro ingestion (pipeline, dataflow, notebook) a kdy který použít.
        
    - Jaké úložiště ve Fabric použít – Lakehouse, Data Warehouse, KQL Database (rozdíly a vhodnost v konkrétních scénářích).
        
    - Jak garantovat datovou kvalitu a zajištění robustní analytické architektury – validační checkpointy napříč workflow, minimalizace erorrů.
        
    - Nové možnosti připojení Power BI – např. DirectLake, import/query.
        
    - Ukázka kompletní migrace – od workspace přes ingestion až po reporting.
        
- **Proč přejít na Fabric-centric model:**
    
    - Jednodušší governance (přístupová práva, dokumentace, audit dat)
        
    - Lepší datová kvalita a robustnost
        
    - Možnost jednodušší integrace AI/ML a datové vědy
        
    - Větší škálovatelnost a moderní architektura odpovídající současným požadavkům na rychlost a efektivitu
        
    - Silnější podpora pro self-service analytics v organizaci
        

---

## Série obsahuje

- Úvodní video (Series Introduction)
    
- Workspace strategie & Access control
    
- Data access patterns (ingestion vs mirroring vs shortcuts)
    
- Data ingestion tools (pipeline vs dataflow vs notebook)
    
- Data architecture patterns & stores (lakehouse, warehouse, KQL DB)
    
- Zajištění datové kvality
    
- Připojení Power BI (DirectLake)
    
- Kompletní end-to-end migrační příklad
    
- Extra bonus na závěr
    

---

## **Tato video série je ideální pro každého, kdo reálně přechází z Power BI do Fabric a chce s minimem chyb zvládnout migraci, nastavit moderní workflow a využít všechny výhody Fabric platformy.**

Chceš-li detailní bodový přehled pro další videa série, napiš!

1. [https://www.youtube.com/watch?v=U4O4PAS--EE](https://www.youtube.com/watch?v=U4O4PAS--EE)
2. [https://www.skool.com/microsoft-fabric/classroom/d154aad4?md=f3761a3e1c4243dbb9ffa4cac5b06600](https://www.skool.com/microsoft-fabric/classroom/d154aad4?md=f3761a3e1c4243dbb9ffa4cac5b06600)
   
---
---

# 🚀 Checklisty a podrobný rozpis nejčastějších chyb u nastavení Microsoft Fabric (podle videa „Capacities, Workspaces and Access Control“)

---

## 1. Nastavení kapacit

**Chyby**

- Příliš mnoho nebo příliš málo kapacit – chaos v billing, správa, výkon
    
- Nesprávné regionální nastavení (porušení GDPR, data residency)
    
- Špatné rozdělení workloadů mezi kapacity (např. BI vs. datové zpracování)  
    **Checklist**
    
- Zvolit minimum kapacit, ideálně jednu (zjednodušení správy)
    
- Vytvořit dodatečné kapacity pouze:
    
    - pro regionální regulace (např. EU, USA)
        
    - pro účtování podle oddělení (nákladová střediska)
        
    - pro rozdělení workloadu (BI/reporting vs. ETL/ML)
        
- Ujistit se, že nákup kapacit odpovídá skutečné spotřebě a potřeba firmy
    

---

## 2. Správa workspace

**Chyby**

- Přespříliš workspace – roztříštěná data, složitá orientace, náročná údržba
    
- Špatná struktura workspace (nejasné rozlišení rolí, vývoj/prod/test)  
    **Checklist**
    
- Plánovat workspace podle:
    
    - týmových/persónních rolí (Data Engineering, Data Science, BI…)
        
    - architektury projektu (Medallion, Data Mesh…)
        
    - vrstvy nasazení (Development, Test, Production – ideálně naming konvencí v jednom workspace)
        
- Minimalizovat počet workspace:
    
    - Sloučit, pokud málo uživatelů/objektů, nebo podobné workflow
        
    - Rozlišovat workspace primárně podle spolupráce týmů, ne technologických objektů
        

---

## 3. Správa přístupu a rolí

**Chyby**

- Individuální přidělování práv (komplikace při onboarding/offboarding, audit)
    
- Nejasný rozdíl mezi rolemi (admin, member, contributor, viewer)  
    **Checklist**
    
- Vždy nastavovat přístup přes:
    
    - Entra ID security groups
        
    - Microsoft 365 Groups
        
- Přidělovat role skupinám, nikdy jednotlivcům
    
- Dokumentovat, kdo má jakou roli (a proč)
    
- Nastavit workflow pro správné mapování nových uživatelů do skupin
    

---

## 4. Práva podle objektů (Fabric items)

**Chyby**

- Přístup na nesprávné úrovni (workspaces místo item/object level)
    
- Nesprávné interpretace práv u různých typů objektů  
    **Checklist**
    
- Ověřit práva pro každý typ itemu:
    
    - admin, member, contributor: stejné pravomoci u většiny itemů
        
    - viewer: pouze čtení obsahu, omezené spouštění (pipeline – může spustit i zrušit)
        
    - u Lakehouse: viewer může pouze přes SQL endpoint, ne Spark
        
- Sdílet pouze objekty, které to podporují! (např. Data Pipeline, Dataflow – pouze přes workspace, nikoliv individuálně)
    

---

## 5. Objekt-level sharing (tabulka, sloupec, řádek)

**Chyby**

- Nesprávné nastavení sdílení objektů (nefunguje vždy u Spark)
    
- Sdílené objekty pouze v Data Warehouse/SQL endpoint Lakehouse  
    **Checklist**
    
- Pro složité scénáře používat:
    
    - Objektové sdílení (tabulka, pohled, sloupec, řádek)
        
    - Row-level security, Column-level security, Dynamic data masking
        
- Sdílet item/objekt pouze tam, kde to má význam (neukládat do Spark, nefunguje fine-grain security)
    

---

## 6. Orchestrace napříč workspace

**Chyby**

- Pokusy o kopírování dat skrz různé workspace pomocí pipeline – nejde!
    
- Špatné plánování workflow (pipeline vs. notebook vs. dataflow vs. eventstream)  
    **Checklist**
    
- Pipeline: zdroj i cíl musí být ve stejném workspace
    
- Notebook nebo Dataflow: lze napříč workspace, v případě potřeby orchestrace mezi projekty, používat tyto objekty
    
- Plánovat workflow podle možností Fabric nástrojů, ne podle starých zvyklostí z Power BI/SQL
    

---

## 7. Naming konvence, dokumentace, audit

**Checklist**

- Vždy používat jasné naming konvence:
    
    - „Hedin_Automotive_Engineering_Dev“, „Hedin_Automotive_Engineering_Test“, „Hedin_Automotive_Engineering_Prod“
        
- Evidovat workspace, kapacity, role, itemy a jejich sdílení (technická dokumentace + průběžná maintenance)
    
- Udržovat seznam skupin a jejich mapování, onboarding checklist pro nové uživatele
    
- Kontrolovat přístup a sdílení každý kvartál (běžný security/audit proces)
    

---

**Doporučení:**  
Pro tým/středně velkou firmu doporučuji jeden workspace per tým/role, silnou naming konvenci a veškeré sdílení přes skupiny. Orchestraci na cross-workspace řešit notebookem/dataflow, kapacitu držet na minimum. Přístup auditovat a pravidelně aktualizovat.

Potřebuješ konkrétní vzor checklist, technický audit nebo naming konvenci? Dej vědět, doplním detailní template!

1. [https://www.skool.com/microsoft-fabric/classroom/d154aad4?md=5247e9c3ed2e4b64858a2a5e53c36481](https://www.skool.com/microsoft-fabric/classroom/d154aad4?md=5247e9c3ed2e4b64858a2a5e53c36481)

![[Workspaces.excalidraw]]

---
---

# 🚀 Shrnutí videa „Data pipeline vs Dataflow vs Shortcut vs Notebook in Microsoft Fabric“

---

## Účel videa

- Pomáhá **rozhodnout**, jaké nástroje použít pro **dostávání dat do Fabric**
    
- Popisuje, kdy je vhodné použít:
    
    - Dataflow (Gen2)
        
    - Data pipeline
        
    - Fabric notebook (Spark)
        
    - OneLake shortcut
        
    - Database mirroring
        

---

## Klíčová témata a checklist

## 1. Dataflow Gen2

- **Kdy použít:**
    
    - Nutnost použít některý ze 300+ konektorů
        
    - No-code/low-code scénáře (Power Query), přístup pro netechnické uživatele
        
    - Přístup k on-premise datům (jediná cesta v současnosti)
        
    - ETL (Extract, Transform, Load) v jednom workflow
        
- **Kdy ne:**
    
    - Velké datové objemy (může být pomalé/neefektivní v kapacitním vytížení)
        
    - Potřeba složité validace dat
        
    - Rozsáhlé control flow/looping (raději pipeline/notebook)
        
- **Poznámky:**
    
    - Lze napojit dataflow do pipeline (lepší orchestrace/logování)
        
    - Není podpora parametrů, looping
        
    - Umožňuje čtení/zápis napříč workspace
        

---

## 2. Data pipeline

- **Kdy použít:**
    
    - Potřeba orchestrace více aktivit (triggování, rozvětvené workflow, error handling)
        
    - Velké datové objemy (efektivnější než dataflow na kopírování dat)
        
    - Přístup k cloudovým zdrojům (Azure SQL, Data Lake, apod.)
        
    - Control flow logika (podmínky, větvení, sekvenční operace)
        
- **Kdy ne:**
    
    - Chybí transformační možnosti (musíš vkládat dataflow/notebook pro transformace)
        
    - Nelze napojit na on-premise data (chybí gateway support)
        
    - Nelze nahrávat lokální soubory
        
    - Omezení napříč workspace (zdroj/cíl musí být ve stejném workspace)
        
- **Poznámky:**
    
    - Podpora nested pipelines
        
    - Vhodné pro metadata-driven ETL orchestrace
        

---

## 3. Fabric notebook (Spark/Python)

- **Kdy použít:**
    
    - Extrakce z API (REST, client Python knihovny)
        
    - Složitá autentifikace, vlastní logika připojení
        
    - Validace dat, pokročilé testování kvality dat
        
    - Velké datové objemy (scale-out pomocí Spark)
        
    - Kód můžeš znovupoužívat a sdílet
        
- **Kdy ne:**
    
    - Nedostatek Python znalostí v týmu
        
    - Organizace preferuje low/no code řešení
        

---

## 4. OneLake shortcut

- **Kdy použít:**
    
    - Externí data (ADLS, Amazon S3, Dataverse)
        
    - Potřeba live synchronizace souborů/folderů bez ETL
        
    - Interní propojení tabulek napříč Fabric (omezené podle typu zdroje/cíle)
        
- **Kdy ne:**
    
    - Omezené typy dat/zdrojů, některé směry nejsou možné (např. Lakehouse → Data Warehouse neprojde shortcutem)
        
- **Poznámky:**
    
    - Pozor na cross-region egress fees (přenos mezi regiony)
        
    - Shortcut musí mít uživatel přístup v obou workspace (source/target)
        
    - Lze automatizovat přes Fabric REST API
        

---

## 5. Database mirroring

- **Kdy použít:**
    
    - Třeba realtime synchronizace dat z podporovaných databází (Snowflake, Cosmos DB, Azure SQL)
        
    - Chcete využít Delta/Parquet formát a time travel pro tracking změn
        
- **Kdy ne:**
    
    - Zatím v preview, omezené typy databází
        

---

## Rozhodovací kritéria (kdy co zvolit):

- Potřeba real-time dat → Shortcut, Database mirroring
    
- Velikost/škálovatelnost dat → Notebook, Pipeline
    
- Skillset týmu → Notebook (Pythonista), Dataflow/Pipeline (Low-code)
    
- Přístup k on-prem → Dataflow
    
- Orchestrace/workflow → Pipeline
    
- Náklady/efektivita → Otestuj ingestion na malém vzorku a sleduj kapacitu
    

---

Tato struktura ti pomůže **rozhodnout, jaký nástroj použít v konkrétním scénáři pro ingest dat do Fabric. Pokud chceš workflow diagram nebo konkrétní příklady, stačí říct!**

1. [https://www.youtube.com/watch?v=t5mUKaLWpHE](https://www.youtube.com/watch?v=t5mUKaLWpHE)
2. [https://www.skool.com/microsoft-fabric/classroom/d154aad4?md=76945d8a83dd4ce7a396a71642f4b28e](https://www.skool.com/microsoft-fabric/classroom/d154aad4?md=76945d8a83dd4ce7a396a71642f4b28e)

---
---

# 🚀 Shrnutí obsahu „Choosing a data store - Fabric Foundation · Learn Microsoft Fabric“

---

## Cíl sekce/videa

- **Pomoc s výběrem správného datového úložiště v Microsoft Fabric** pro různé analytické scénáře.
    

---

## Hlavní typy datových úložišť:

- **Lakehouse**
    
- **Data Warehouse**
    
- **KQL Database**
    

---

## Porovnání hlavních úložišť

|Typ úložiště|Kdy použít|Engine|Formát dat|Vhodné scénáře|
|---|---|---|---|---|
|Lakehouse|Velká, nestrukturovaná/strukturovaná data, moderní ELT workflow|Spark, SQL|Delta/Parquet|Data engineering, ML, BI, reporting|
|Data Warehouse|Strukturovaná data, transakční analytika, SQL pohledy|Polaris (SQL)|Delta/Parquet (interně)|BI reporting, SQL analytika|
|KQL Database|Logy, telemetry, streamovaná/event data|Kusto (KQL)|KQL native|Real-time analytics, time series|

---

## Checklist podle scénáře

- Pokud potřebuješ **dělat datové inženýrství, pokročilé datové transformace, ML — Lakehouse** (přístup přes Spark/SQL, ideální pro notebooky, work with files i tabulky).
    
- Pokud potřebuješ **SQL reporting, tabulkovou analytiku, BI, governance — Data Warehouse** (T-SQL, možnost pohledů, výkonná BI analytika, security na úrovni objektu).
    
- Pokud řešíš **real-time analýzu na event datech, telemetry, clickstream — KQL Database** (Kusto engine, KQL dotazy, rychlá analýza velkých streamovaných dat).
    
- _Vždy ověř, co bude typicky tvůj hlavní typ workflow_:
    
    - Chci robustní data engineering? → Lakehouse
        
    - Potřebuji bezpečnost a SQL reporting? → Data Warehouse
        
    - Potřebuji real-time pohledy na eventy/logy? → KQL Database
        

---

## Poznámky:

- Všechny typy úložišť v Fabric sdílí jednotné OneLake jádro (data v Delta/Parquet nebo nativních formátech).
    
- Lakehouse je vhodný pro flexibilní ingest dat i pokročilé transformace, Data Warehouse exceluje ve škálovatelném BI/reportingu s detailním security, KQL je best pro telemetry/log scénáře.
    
- Připojení na Power BI lze dělat prakticky z každého úložiště (Direct Lake, Import, nebo DirectQuery).
    
- U komplexních projektů lze vrstvy kombinovat, např. Data pipeline → Lakehouse → BI přes Data Warehouse.
    

---

**Stručné pravidlo**:  
_„Vyber podle dominantního analytického workflow, zvaž možnosti enginu, datových typů, potřeb security i očekávané integrace na reporting/BI.“_

Pokud chceš tabulku s podrobným porovnáním, konkrétní workflow, nebo architekturu na míru, napiš!

1. [https://www.skool.com/microsoft-fabric/classroom/d154aad4?md=f52947275c0d4db68b1d1ad9e93c5a6a](https://www.skool.com/microsoft-fabric/classroom/d154aad4?md=f52947275c0d4db68b1d1ad9e93c5a6a)
2. ![[Data stores.pdf]]
---
---

#🚀