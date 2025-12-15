# Studium u videa: Aleksi DP-700 Exam Prep: Scope, Skills & Essential Tools

DP‑700 testuje tři hlavní oblasti (implement & manage analytic solution, ingest & transform data, monitor & optimize analytic solution) a stojí na klíčových Fabric nástrojích: pipelines, dataflow Gen2, notebooks, eventstream, lakehouse, warehouse a eventhouse. Následující podklad je připravený jako kompletní markdown poznámka pro Obsidian.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​

---

# DP‑700 – Scope, Skills & Essential Tools

## Přehled zkoušky

- Tři hlavní sekce zkoušky:
    
    - Implement & manage analytic solution
        
    - Ingest & transform data
        
    - Monitor & optimize analytic solution.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        
- Cíl: vědět, na které skills a nástroje se soustředit, a co je ve Fabricu skutečně relevantní pro DP‑700.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
    

---

## Sekce 1 – Implement & manage analytic solution

- Správa workspace:
    
    - Nastavení workspace (Spark settings, OneLake, data workflow) a pochopení, jak ovlivňují celé řešení.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        
- Lifecycle management:
    
    - Version control (Git), database projects, deployment pipelines – denní chléb data inženýra.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        
- Governance & security:
    
    - Přístup na úrovni workspace, objektů, řádků/sloupců; data masking, sensitivity labels, endorsement.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        
- Orchestrace řešení:
    
    - Výběr nástroje pro orchestraci (pipelines, notebooks, dataflow Gen2), plánování, triggery, parametry, dynamické výrazy.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        

---

## Sekce 2 – Ingest & transform data

- Ingest patterns:
    
    - Full load vs incremental load – kdy použít který přístup a jak ovlivňuje architekturu.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        
- Dimenzionální modelování:
    
    - Základy hvězdicového schématu, faktové a dimenzní tabulky, načítání do dimenzionálního modelu.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        
- Typy dat a datové zdroje:
    
    - Batch data: výběr mezi pipelines, dataflow, shortcuts/mirroring.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        
    - Datové úložiště: lakehouse vs warehouse vs eventhouse; kdy virtualizovat (shortcut/mirroring) vs kopírovat.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        
- Transformace a jazyky:
    
    - SQL (T‑SQL, Spark SQL), Python/PySpark, KQL.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        
    - Operace: joiny, agregace, group by, čištění dat, řešení duplicit a pozdě příchozích záznamů.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        
- Streaming:
    
    - Eventstream + Spark Structured Streaming jako hlavní nástroje.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        
    - Windowing functions pro práci s časovými okny.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        

---

## Sekce 3 – Monitor & optimize analytic solution

- Monitorování řešení:
    
    - Stav ingestu (pipelines, eventstream), transformací (dataflow, notebooks) a refreshů semantic modelů.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        
    - Alerty pro automatické upozornění na problémy.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        
- Troubleshooting:
    
    - Řešení chyb v pipelines, dataflow, notebooks, eventhouse/eventstream a T‑SQL.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        
- Optimalizace výkonu:
    
    - Ladění lakehouse tabulek, pipelines, warehouses, eventhouse/eventstream, Spark jobs a dotazů.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        
    - Výběr vhodného návrhu řešení s ohledem na výkon.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        

---

## Klíčové nástroje – přehled

- Data movement & transformation tools:
    
    - Data pipeline, Dataflow Gen2, Notebook, Eventstream.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        
- Data stores:
    
    - Lakehouse, Warehouse, Eventhouse.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        
- Většina exam scénářů se točí kolem správného použití a kombinace těchto nástrojů.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
    

---

## Data Pipeline

- Charakteristika:
    
    - Low/no‑code orchestration nástroj podobný ADF/Synapse pipelines; používá se pro integraci a řízení běhu kroků.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        
- Vlastnosti:
    
    - Canvas s aktivitami (Copy Data, notebook activity, dataflow activity, refresh semantic modelu).[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        
    - Podmíněná logika, smyčky, parametry, proměnné, expression language.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        
- Role v řešení:
    
    - Lepí jednotlivé kroky do end‑to‑end workflow.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        
    - Transformace minimálně – hlavní role je orchestrací.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        

---

## Dataflow Gen2

- Charakteristika:
    
    - Low/no‑code nástroj pro transformace založený na Power Query.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        
- Typický postup:
    
    - Připojení ke zdroji, výběr tabulky, transformace přes UI (remove, filter, merge, change type).[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        
- Integrace:
    
    - Bývá volán z pipelines, aby byl součástí orchestrace.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        
- Zásadní rozdíl:
    
    - Dataflow = transformace; pipeline = orchestrace.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        

---

## Notebooks

- Charakteristika:
    
    - Code‑based nástroj pro pokročilé transformace a datovou logiku; podporuje Python a Spark SQL pro Spark notebooks.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        
- Další typy notebooks:
    
    - Python notebooks (bez Spark), T‑SQL notebooks pro databáze.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        
- Výhody/nevýhody:
    
    - - Největší flexibilita a síla, vhodné pro složité scénáře.
            
    - − Vyžadují programátorské dovednosti.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        
- Role v DP‑700:
    
    - Typická volba pro komplexní transformace a práci s lakehouse.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        

---

## Eventstream

- Charakteristika:
    
    - No/low‑code nástroj pro ingest a transformaci streamovaných dat.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        
- Funkce:
    
    - Node‑based canvas, kroky jako filtrování a další transformace přes UI.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        
- Integrace:
    
    - Typicky píše do eventhouse či jiných streaming‑ready stores.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        
- Role v DP‑700:
    
    - Hlavní streaming nástroj v low‑code světě Fabricu.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        

---

## Lakehouse

- Charakteristika:
    
    - Ukládá soubory (libovolný formát) i Delta tabulky se schématem.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        
- Struktura:
    
    - Složka Files (file system) a Tables (Delta tabulky).[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        
- Integrace:
    
    - Nejlépe se obsluhuje přes notebooks (Spark).[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        
- Specifika:
    
    - Jako jediný Fabric data store umí nativně raw CSV a obecné soubory.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        

---

## Warehouse

- Charakteristika:
    
    - Relační SQL databáze ve Fabricu, používá schemas, tables, views, stored procedures, functions.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        
- Jazyk:
    
    - T‑SQL pro dotazy i transformace uvnitř skladu.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        
- Transformace:
    
    - Možnost psát transformace jako stored procedures – warehouse funguje jako data store i transformation tool.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        
- Kontrast s lakehouse:
    
    - Lakehouse = soubory + Delta + Spark; warehouse = čistě relační SQL store.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        

---

## Eventhouse

- Charakteristika:
    
    - Workspace pro KQL databáze, určen primárně pro event/telemetry data.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        
- Integrace:
    
    - Nejčastější kombinace: eventstream → eventhouse.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        
- Jazyk:
    
    - KQL pro analýzu event dat.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        

---

## Jazyky ve scope DP‑700

- Jazyky, které potřebuješ:
    
    - Spark SQL, T‑SQL, Python/PySpark, KQL.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        
- Jazyk mimo scope:
    
    - DAX – protože Power BI a DAX nejsou hlavním zaměřením DP‑700.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        
- Úroveň znalosti:
    
    - Základní až středně pokročilá – schopnost řešit typické DE úlohy.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        

---

## Tabulka – Nástroj vs. účel

|Nástroj|Typ|Hlavní účel|Typické použití|
|---|---|---|---|
|Data pipeline|Orchestrace|Řízení běhů, plánování, integrace kroků|Copy Data, volání notebooků/dataflow, refresh modelu.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​|
|Dataflow Gen2|Transformace|Low‑code transformace dat|Čištění, tvarování tabulek, jednoduché ETL.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​|
|Notebook|Transformace|Code‑based komplexní transformace|Pokročilé ETL/ELT, business logika, práce s lakehouse.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​|
|Eventstream|Streaming|Ingest a transformace streaming dat|Příjem telemetrie, filtr, zápis do eventhouse.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​|
|Lakehouse|Data store|Uložení souborů a Delta tabulek|RAW/Silver/Gold vrstvy, práce se Sparkem.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​|
|Warehouse|Data store|Relační SQL analytická databáze|Dimenzionální model, T‑SQL transformace.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​|
|Eventhouse|Data store|Uložení a analýza event dat (KQL)|Telemetrie, logy, streaming analytika.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​|

---

## Exam‑like otázky z videa

1. Který jazyk není součástí DP‑700?
    
    - Spark SQL, KQL, DAX, T‑SQL, Python/PySpark → správně: DAX.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        
2. Který Fabric data store umí ukládat raw CSV soubory?
    
    - Warehouse, Azure Blob Storage, Eventhouse, Azure SQL Database, Lakehouse → správně: Lakehouse.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
        

---

## Jak s tímto podkladem pracovat

- Přidávej vlastní příklady z praxe (např. jak bys v práci použil pipeline vs notebook).[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
    
- U každé sekce si znač: „rozumím / zopakovat“, a vytipuj si slabší jazyky (KQL, Spark SQL…) pro cílený trénink.[youtube](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)​
    

1. [https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1](https://www.youtube.com/watch?v=tynojQxL9WM&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=1)
2. [https://www.youtube.com/watch?v=DWUuuGAxwlI&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=2](https://www.youtube.com/watch?v=DWUuuGAxwlI&list=PLlqsZd11LpUEaz9mgMR-mQgbvscTI0Q5x&index=2)