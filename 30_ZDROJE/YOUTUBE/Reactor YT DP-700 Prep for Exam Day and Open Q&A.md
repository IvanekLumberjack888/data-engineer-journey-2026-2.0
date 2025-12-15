# Ze série [YT: DP-700 Prep for Exam Day and Open Q&A](https://youtube.com/playlist?list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&si=cKmbUuzcak8kr7S9)
# 🚀 DP-700 Part 1: Implement and Manage Analytics Solutions

Video představuje první část akcelerované přípravy na certifikaci DP-700 zaměřenou na implementaci a správu analytických řešení v Microsoft Fabric. Níže je strukturované shrnutí v češtině vhodné do Obsidianu.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​

## Kontext a cíle sezení

- Sezení je součástí série „Get Certified: DP-700 Fabric Data Engineer (accelerated)“ pořádané Microsoft Reactor.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Cílem je ukázat, jak navrhnout a implementovat škálovatelná analytická řešení v Microsoft Fabric s důrazem na architekturu, lakehouse a integraci dat.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    

## Architektura Microsoft Fabric

- Microsoft Fabric sjednocuje služby pro analytiku (data engineering, data factory, warehousing, real-time, BI) do jedné platformy sdílející společný OneLake.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Architektura umožňuje pracovat s různými workloady (Engineering, Data Science, Real-Time, Power BI) nad stejným úložištěm, což snižuje duplikaci dat a zjednodušuje správu.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    

## OneLake a úložiště dat

- OneLake funguje jako „jedno jezero“ pro celou organizaci, na kterém jsou logicky budované struktury jako lakehouse, data warehouse a další objekty.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Fabric podporuje otevřené formáty (Parquet/Delta) a umožňuje sdílení dat napříč workspace a workloady bez nutnosti jejich kopírování.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    

## Lakehouse koncept v Fabric

- Lakehouse kombinuje prvky data lake a data warehouse – umožňuje ukládání souborů i tabulek ve společném prostoru a podporuje SQL i Spark.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- V rámci lakehouse se typicky buduje medailonová architektura (bronze–silver–gold) s postupným čištěním, transformací a modelováním dat pro reporting a analytiku.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    

## Ingestní a integrační možnosti

- Fabric nabízí více způsobů ingestu dat: Data Factory (pipeline, copy aktivity), Dataflows, přímé připojení na zdroje, event streamy apod.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Při návrhu řešení se volí správná strategie ingestu podle charakteru zdroje (batch vs. real-time, on-prem vs. cloud) a požadavků na latenci a spolehlivost.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    

## Navrhování škálovatelných řešení

- Škálovatelnost je zajištěna oddělením výpočetních zdrojů od úložiště a možností škálovat kapacitu podle zátěže (např. přes Fabric capacity).[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Doporučuje se modularizace řešení: oddělit ingest, zpracování, kuraci dat a prezentační vrstvu, aby bylo možné nezávisle spravovat a optimalizovat jednotlivé části.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    

## Správa workspace a prostředí

- Workspaces v Fabric slouží jako logické kontejnery pro artefakty (lakehouse, pipelines, semantic modely, reporty) a také jako hraniční bod pro řízení přístupu.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Při správě se řeší role, oprávnění, použití development / test / production workspace a nasazování mezi nimi (např. pomocí deployment pipelines).[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    

## Governance a zabezpečení

- Governance zahrnuje správu přístupů, citlivosti dat (sensitivity labels), sledování lineage a auditování přístupu k datům a objektům.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Důraz je kladen na centralizované řízení datových standardů a opakovatelnost – aby data engineers, analytici i BI uživatelé pracovali s konzistentními, schválenými zdroji.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    

## Napojení na Power BI a semantic modely

- Fabric úzce integruje Power BI – semantic modely a reporty mohou být přímo nad lakehouse nebo warehouse, což zkracuje cestu od dat ke vizualizaci.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Doporučuje se budovat robustní semantic modely (tabulární modely) jako jednotný zdroj pravdy pro reporting napříč týmy.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    

## Přínos pro přípravu na DP-700

- Sezení pomáhá pochopit, jak se na zkoušce DP-700 hodnotí návrh a správa end-to-end analytických řešení ve Fabric, včetně architektury, ingestu a governance.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Doporučený další krok je projít další části série (Ingest & Transform Data, Monitor & Optimize Solutions) a oficiální přípravné materiály na aka.ms/dp700/prepare.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    

1. [https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)

---

# 🚀 DP-700 Part 2: Ingest and Transform Data

Toto sezení je druhou částí akcelerované přípravy na DP-700 a zaměřuje se na ingest a transformaci dat v Microsoft Fabric pomocí Dataflows Gen2 a Data Factory pipelines. Níže máš stručné, ale strukturované shrnutí vhodné do Obsidianu.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​

## Kontext sezení

- Sezení je součástí série „Get Certified: DP-700 Fabric Data Engineer (accelerated)“ pořádané Microsoft Reactor.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Cílem je ukázat, jak použít existující zkušenosti s ETL/ELT nástroji (Power BI, Azure Data Factory apod.) v prostředí Microsoft Fabric pro batch i streaming scénáře.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    

## Hlavní nástroje: Dataflows Gen2 a Pipelines

- Dataflows Gen2 slouží k vizuální přípravě dat (mapování, transformace) nad různými zdroji s cílem uložit data do OneLake (např. do lakehouse tabulek nebo souborů).[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Data Factory pipelines v Fabric zajišťují orchestrace – plánování, sekvencování kroků, kopírování dat a integraci s dalšími aktivitami (notifikace, kontrolní kroky).[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    

## Ingest dat – batch scénáře

- Prezentace ukazuje, jak navrhnout batch ingest z typických zdrojů (databáze, soubory, SaaS) pomocí copy aktivit a dataflow kroků, aby se data bezpečně dostala do OneLake.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Důraz je na opakovatelnost a parametrizaci – opakované načítání větších objemů dat, plánování běhů a minimalizaci manuálních zásahů.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    

## Transformace dat v Fabric

- Transformace probíhá v Dataflows Gen2 (power query M), případně navazujících procesech (Spark, SQL, další pipeline kroky) pro čištění, obohacování a business logiku.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Cílem je připravit data tak, aby byla vhodná pro medailonovou architekturu (bronze–silver–gold) a následné využití v lakehouse, warehouse a semantic modelech.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    

## Streaming, real-time dashboardy a alerty

- Sezení zmiňuje, že kromě batch scénářů Fabric podporuje i streaming a near-real-time vzory pro dashboardy a alerty.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Ukazuje se, jak lze pomocí dostupných nástrojů v Fabric sestavit pipeline, která průběžně přivádí data a aktualizuje vizualizace či spouští upozornění.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    

## Praktické workflow pro data engineera

- Prezentace vede diváka krokem po kroku: od výběru zdroje, přes vytvoření dataflow/pipeline, konfiguraci cílů v OneLake, až po publikaci dat pro další týmy.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Důraz je kladen na znovupoužitelnost komponent, správné pojmenování, verzování a využití Fabric jako jednotné platformy pro ingest i transformace.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    

## Přínos pro přípravu na DP-700

- Sezení pomáhá sladit teoretické požadavky DP-700 s praktickými dovednostmi: jak v době zkoušky rozumět rolím Dataflows Gen2 a Pipelines v rámci Fabric řešení.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Doporučuje se navázat na další části série (Implement and Manage Analytics Solutions, Monitor and Optimize Solutions) a prohloubit práci s nástroji v sandbox prostředí.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    

1. [https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)
2. [https://www.youtube.com/watch?v=4QKT8yQz2l8&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=3](https://www.youtube.com/watch?v=4QKT8yQz2l8&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=3)

---

# 🚀 # DP-700 Part 3: Monitor and Optimize Solutions

Třetí díl série je zaměřený na sledování a optimalizaci řešení ve Fabricu, aby byla rychlá, spolehlivá a cenově efektivní – přesně to, co jako data engineer budeš denně řešit. Níže je shrnutí v podobě poznámky vhodné do Obsidianu.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​

## Kontext sezení

- Jde o třetí epizodu série „Get Certified: DP-700 Fabric Data Engineer (accelerated)“ zaměřenou na oblast „Monitor and Optimize Solutions“ ze zkoušky.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Cílem je ukázat, proč a jak monitorovat Fabric řešení, jak optimalizovat výkon (storage, compute, dotazy) a jak zohlednit bezpečnost a compliance.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    

## Proč monitorovat a optimalizovat

- Monitoring slouží k tomu, aby bylo možné včas odhalit chyby, dlouho běžící úlohy a úzká hrdla – ideálně proaktivně, ještě než to pocítí uživatelé.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Optimalizace cílí na rovnováhu mezi výkonem a náklady: nechceš poddimenzovat compute (pomalé reporty), ale ani přepálené kapacity, které zbytečně stojí peníze.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    

## Co ve Fabricu monitorovat

- Pipelines: historie běhů, chyby, délku trvání, závislosti mezi aktivitami a případné retry.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Dataflows Gen2, semantic model refresh, Spark joby/notebooky, lakehouse a event streams – u všeho sledovat stav, výkon, zdroje a případné chyby.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    

## Monitor Hub ve Fabricu

- Monitor Hub poskytuje centrální místo, kde vidíš historii a detaily běhů: pipelines, dataflows, refresh modelů, Spark úlohy a další položky.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- U konkrétního běhu můžeš zobrazit status, start/end čas, trvání, statistiky a často se prokliknout až na detailní logy a Spark execution details.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    

## Vestavěné monitoring reporty

- Fabric nabízí Power BI reporty pro monitoring: např. chargeback reporting (využití kapacity), feature usage/adoption a content sharing.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Tyto reporty jsou postavené na semantic modelech a slouží spíše pro historickou analýzu (ne real-time); je nutné je pravidelně refreshovat.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    

## Best practices pro monitoring

- Nejdřív si ujasnit, co je „normální“ – sledováním metrik v čase vybudovat baseline, proti které pak poznáš anomálie.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Aktivně pracovat s logy a metrikami, navázat na ně alerty (např. Data Activator / real-time intelligence) a tam, kde dává smysl, automatizovat reakce (retry, restart, fallback).[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    

## Optimalizace storage (OneLake, Lakehouse, Warehouse)

- Fabric používá Delta/Parquet, a proto je důležité používat techniky jako OPTIMIZE, COMPACT a Z-ORDER (prakticky „index“ pro Delta Lake) pro rychlejší čtení.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- U velkých datasetů hraje roli správné partitioning a distribuce dat, aby se zefektivnilo skenování a dotazy nad lakehouse i warehouse.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    

## Optimalizace pipelines a ingestu

- Preferovat inkrementální načítání před full loady, omezovat zbytečné pohyby dat a využívat paralelismus tam, kde to zdroj dovolí.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Správně nastavit triggery (časové, event-based), závislosti aktivit a retry strategie tak, aby pipeline byly robustní, ale zároveň efektivní.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    

## Optimalizace Spark a notebooků

- Spark pooly lze nastavit podle workloadu (velikost, auto-scale, typ uzlů) a hlídat, aby nebyly zbytečně velké nebo naopak slabé.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- V pipelines lze opakovaně využít stejnou Spark session pomocí „session tagu“ pro víc notebooků za sebou, čímž se snižuje overhead startu clusteru.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    

## Real-time: Event Streams a KQL

- Event Streams běží typicky kontinuálně a přijímají boundless data (telemetrie, IoT, logy), která mohou být směrovaná do více cílů (KQL DB, lakehouse atd.).[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Je nutné monitorovat průběžně ingest rate, latenci a chybovost, protože špičky ve streamu mohou vyžadovat více compute a jinak ovlivnit downstream řešení.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    

## Bezpečnost ve Fabricu

- Fabric využívá Microsoft Entra ID (Azure AD) pro autentizaci a multi-tenant izolaci, data jsou šifrovaná v klidu i při přenosu.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Přístup k objektům (workspaces, položky, data) je řízen role-based access controlem (RBAC) v rámci stejného tenant ekosystému jako M365 a Azure.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    

## Compliance a data residency

- Data zůstávají v regionu, kde byla vytvořena (např. EU pro GDPR), zatímco část metadat a zpracování může běžet v „home region“ tenant organizace.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Fabric podporuje multi-geo scénáře tak, aby bylo možné kombinovat lokální regulace (GDPR, CCPA) s centrální správou dat v rámci jednoho Microsoft tenant.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    

## Nástroje pro bezpečnost a compliance

- Kromě Monitor Hubu lze využít activity/audit logy, klasifikaci dat, sensitivity labels a další nástroje z Microsoft 365/Azure ekosystému.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Monitoring bezpečnosti zahrnuje sledování přístupů, změn konfigurace, anomální aktivity a využití alertů pro rychlou reakci.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    

## Doporučení pro přípravu na DP-700

- Získat praktický přístup k Fabric (organizace, trial kapacita) a projít si monitoring, optimalizaci Spark, pipelines, lakehouse a event streams „na vlastní ruce“.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Studovat oficiální DP-700 study guide a Learn moduly, zaměřit se na části „Monitor and Optimize Solutions“ a rozumět, jak jednotlivé funkce souvisí v end-to-end řešení.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    

1. [https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)
2. [https://www.youtube.com/watch?v=2lTkPclV_pQ&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=2](https://www.youtube.com/watch?v=2lTkPclV_pQ&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=2)

---

# 🚀 DP-700 Exam Prep: Prepare for Exam Day and Open Q&A

Toto sezení je závěrečná epizoda série pro DP-700, která shrnuje formát zkoušky, přípravu na exam day, strategie práce s otázkami a využití dostupných zdrojů (Learn, practice testy, community). Níže máš poznámku v češtině vhodnou do Obsidianu.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​

## Proč se certifikovat

- Certifikace pomáhá zvýšit hodnotu na trhu práce, podpořit růst mzdy a usnadňuje kariérní posun či získání seniornějších rolí.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- U partnerů Microsoftu jsou certifikace často nutnou podmínkou pro partnerství a konkrétní projekty, HR i team leadeři je v CV aktivně vyhledávají.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Příprava na zkoušku nutí projít širší spektrum témat než v běžné práci, odhalí mezery ve znalostech a dává jasný cíl a strukturu studia.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    

## Formát zkoušky DP-700

- Zkouška má zhruba 60 otázek, čas na odpovědi je 100 minut, skóre je škálované 0–1000, přičemž hranice pro úspěch je 700 (neodpovídá nutně přesně 70%).[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Typy otázek: multiple choice (single/multi), drag & drop, pořadí kroků, hot area, active screen a case studies s delším scénářem.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Některé bloky (např. část case study) není možné vracet zpět, u jiných lze otázky označovat jako „review later“ a k nim se na konci vrátit.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    

## Práce s otázkami a bodováním

- Za špatnou odpověď nejsou minusové body, proto je vždy lepší něco zvolit než otázku nechat prázdnou.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Ne všechny otázky mají stejnou váhu, uživatel nevidí počet bodů za konkrétní otázku, proto nemá smysl se snažit počítat skóre během testu.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Doporučená strategie: na první průchod rychle odpovědět na všechny otázky, nejisté označit pro review a detailněji se k nim vrátit až po projití celého testu.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    

## Case studies – scénářové otázky

- Case study popisuje fiktivní firmu, její prostředí, business cíle, technické požadavky a omezení; na základě toho následuje sada navazujících otázek.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Informace ve scénáři zahrnují i záměrně nadbytečné detaily, klíčem je rychle poznat, které části jsou relevantní k dané otázce.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Možné strategie:
    
    - Rychle prolétnout všechny sekce case study a pak jít na otázky.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
        
    - Nebo nejdřív jen zjistit, jaké sekce existují, a detailně se k nim vracet až při čtení konkrétních otázek.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
        

## Požadované technické znalosti

- Zkouška očekává orientaci v syntaxi SQL, PySpark a KQL na úrovni čtení kódu, doplnění chybějících částí a pochopení, co daný dotaz dělá.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Důležitá je praktická zkušenost s Fabric (lakehouse, pipelines, Data Factory, Dataflows Gen2, KQL DB, real-time/streaming scénáře), ne jen teorie z dokumentace.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    

## Přípravné materiály a plán studia

- Základ je prostudovat „Exam study guide“ pro DP-700, který přehledně uvádí oblasti dovedností, váhy témat i informace o verzích/aktualizacích zkoušky.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Na Microsoft Learn jsou hotové learning paths a moduly cílené na DP-700, které je vhodné projít po přečtení study guide.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Navíc existují komunitní zdroje (YouTube playlisty, blogy, kurzy, Discord/komunity) – některé jdou hlouběji než oficiální Learn moduly.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    

## Practice assessment a exam sandbox

- K DP-700 existuje oficiální „practice assessment“, který simuluje otázky stejného typu, zobrazí správnou odpověď a krátké vysvětlení plus odkazy na dokumentaci.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Pool otázek v practice testu je omezený, takže opakované vyplňování vede spíš k memorování otázek než k ověření znalostí; nejvíc dává smysl použít ho těsně před termínem zkoušky.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Exam sandbox je samostatné demo prostředí, kde si lze „nanečisto“ projít UI zkoušky, typy otázek, review obrazovku a chování sekcí, ke kterým se nelze vracet.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    

## Microsoft Learn během zkoušky

- U role-based zkoušek (jako DP-700) je v reálné zkoušce dostupné tlačítko pro otevření Microsoft Learn, což umožňuje dohledat detaily v oficiální dokumentaci.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Kvůli omezenému času je potřeba Learn používat selektivně – jen u pár sporných otázek označených pro review, ne u každé otázky.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Užitečný trik je ve vyhledávání aplikovat filtr na Microsoft Fabric, aby se nezobrazovaly výsledky k jiným službám a zrychlilo se hledání relevantních článků.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    

## Exam day – průběh a time management

- Před samotným testem je několik kroků: přihlášení, seznámení s NDA, instrukce, krátký „skills survey“ a teprve poté se spustí odpočet 100 minut.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Během zkoušky je vpravo nahoře viditelný zbývající čas a k dispozici je přehledová obrazovka, která ukazuje, které otázky jsou zodpovězené, nezodpovězené a označené pro review.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Po odevzdání se obvykle ihned zobrazí výsledek; volitelně lze ještě vyplnit zpětnou vazbu k otázkám, která už neubírá čas z limitu zkoušky.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    

## Praktické tipy a mindset

- Doporučuje se zkoušku co nejdřív zarezervovat, mít v kalendáři reálný termín a podle něj plánovat studium; termín lze případně později přerezervovat.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Neúspěch na první pokus není problém – výsledek ukáže slabá místa, která lze cíleně dopracovat, a znovu zkoušku zkusit.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
    
- Rozumná strategie:
    
    - Nepřestudovávat donekonečna, ale v rozumném čase jít psát zkoušku.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
        
    - Při přípravě spojit teorii (Learn, videa) s praktickým hraním si ve Fabric workspace.[youtube](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)​
        

1. [https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4](https://www.youtube.com/watch?v=Cd8BCXxZM8E&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=4)
2. [https://www.youtube.com/watch?v=38cLTNoPLu0&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=1](https://www.youtube.com/watch?v=38cLTNoPLu0&list=PLmsFUfdnGr3zGZfY0QFatlvoargXNU2EZ&index=1)