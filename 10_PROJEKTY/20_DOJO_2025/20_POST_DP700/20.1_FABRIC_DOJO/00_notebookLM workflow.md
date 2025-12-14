

---

# 2. Lifecycle Management (Fabric / DP‑700)

Lifecycle management řeší, jak řízeně vyvíjet, verzovat a nasazovat řešení ve Fabricu přes více prostředí (vývoj, test, produkce).  
V DP‑700 tě zajímá hlavně: verzování artefaktů (version control), databázové projekty a deployment pipelines.

---

## 2.1 Version Control – verzování řešení

## Hlavní myšlenka

- Version control ukládá stav artefaktů (kód, definice objektů) do repozitáře, typicky Git.
    
- Umožňuje spolupráci více vývojářů, průběžné sledování změn a případný návrat ke starším verzím.
    

## Co se typicky verzije ve Fabricu

- T‑SQL skripty, PySpark kód, notebooky (v textové podobě).
    
- Definice pipelines, dataflowů, semantic modelů a dalších objektů jako konfigurační soubory.
    

## Klíčové body pro zkoušku

- Workspace může být napojený na Git repozitář (např. Azure DevOps, GitHub).
    
- Základní workflow: změna → commit → push → pull request → review → merge do hlavní větve.
    
- Version control je základ CI (continuous integration) – každá změna prochází automatizovanými kontrolami.
    

---

## 2.2 Database Projects – databáze jako kód

## Hlavní myšlenka

- Database project reprezentuje schéma databáze jako sadu souborů v projektu (tabulky, pohledy, procedury, funkce).
    
- Schéma se verzije v Gitu a deployment probíhá skriptem generovaným z projektu.
    

## Proč je to důležité

- Změny schématu jsou trasovatelné, recenzované a opakovatelné mezi prostředími.
    
- Lze porovnat rozdíly mezi verzemi databáze a automaticky vygenerovat upgrade skript.
    

## Pro DP‑700 si pamatuj

- Database projects patří do kategorie „schema as code“ a dobře zapadají do CI/CD pipeline.
    
- Typický scénář: vývojář upraví model, commitne změnu, CI pipeline postaví projekt a připraví deployment do testu/produkce.
    

---

## 2.3 Deployment Pipelines – nasazování mezi prostředími

## Hlavní myšlenka

- Deployment pipeline ve Fabricu propojuje několik prostředí (stages), jako je Development, Test a Production.
    
- Každá stage je obyčejný Fabric workspace, který má svou roli v lifecycle řešení.
    

## Co pipeline umí

- Porovnání obsahu mezi stagemi (co chybí, co je novější, co se změní při deploymentu).
    
- Nasazení vybraných artefaktů (reports, datasets, pipelines atd.) z jedné stage na další.
    
- Umožňuje řízený postup: nejdřív dev → test (ověření), pak test → prod.
    

## Důležité pro zkoušku

- Deployment pipelines jsou o nasazování obsahu/workspace objektů, ne o samotném Git version control.
    
- Často se používají společně: Git řeší kód a definice, deployment pipelines řeší propagaci do konkrétních Fabric workspace prostředí.
    

---

# Q&A bloky (s odpověďmi)

Formát si můžeš v Obsidianu přepsat třeba na „## Otázka / ## Odpověď“.

---

**Q1: Jaký je hlavní účel version control ve Fabric projektech?**  
**A1:** Umožnit verzování kódu a definic artefaktů, sledovat historii změn, podporovat spolupráci více vývojářů a mít možnost vrátit se ke starším verzím.

---

**Q2: Jak do CI/CD zapadá Git repozitář napojený na Fabric workspace?**  
**A2:** Workspace čte a zapisuje artefakty do Git repozitáře; každá změna se commituje a pushuje, CI pipeline změnu zkontroluje a po schválení jde obsah dál do testu či produkce.

---

**Q3: Co je to database project v kontextu lifecycle managementu?**  
**A3:** Je to projekt, který popisuje schéma databáze jako sadu souborů, verzovanou v Gitu, ze které se generují skripty pro nasazení změn mezi prostředími.

---

**Q4: Proč je vhodné řídit databázové schéma pomocí database projects?**  
**A4:** Zajišťuje konzistentní a opakovatelné změny schématu, umožňuje code review, audit změn a automatické generování upgrade skriptů pro jednotlivá prostředí.

---

**Q5: Jaký je rozdíl mezi version control a deployment pipeline ve Fabricu?**  
**A5:** Version control řeší verzování a správu kódu/definic v Gitu, zatímco deployment pipeline se stará o nasazování artefaktů mezi konkrétními workspace prostředími (Dev/Test/Prod).

---

**Q6: Jak fungují stages v deployment pipeline?**  
**A6:** Každá stage odpovídá jednomu workspace; pipeline porovnává obsah mezi těmito workspaces a umožňuje řízený přesun vybraných položek z nižší stage na vyšší.

---

**Q7: Jak může být database project zapojený do CI/CD pipeline?**  
**A7:** Po commitu změn do repozitáře CI pipeline projekt sestaví, ověří a vygeneruje skripty, které se následně použijí k nasazení změn do testovacího a následně produkčního prostředí.

---

# Kvízové otázky (styl zkoušky)

Můžeš si je v Obsidianu vést jako separátní poznámku nebo přepsat na checkboxy.

1. **Které tvrzení nejlépe popisuje roli version control v řešení založeném na Fabricu?**  
    a) Slouží pouze k plánování běhů pipelines  
    b) Ukládá verze artefaktů, umožňuje sledovat změny a podporuje spolupráci týmu  
    c) Slouží výhradně k monitoringu výkonu spark jobů  
    d) Nahrazuje potřebu deployment pipelines  
    **Správná odpověď:** b)
    
2. **Co je typickým vstupem pro deployment pipelines ve Fabricu?**  
    a) Výsledky monitoringu  
    b) Git repozitář bez vazby na workspace  
    c) Workspaces reprezentující jednotlivá prostředí (např. Dev, Test, Prod)  
    d) Pouze databázové projekty  
    **Správná odpověď:** c)
    
3. **Jaký je hlavní přínos database projects v rámci lifecycle managementu?**  
    a) Automatizují generování reportů v Power BI  
    b) Umožňují verzovat databázové schéma a generovat konzistentní deployment skripty  
    c) Slouží ke správě uživatelských oprávnění  
    d) Používají se jen pro real‑time streaming scénáře  
    **Správná odpověď:** b)
    
4. **Která kombinace nejlépe odpovídá typickému CI/CD scénáři pro Fabric řešení?**  
    a) Git pro verzování, manuální kopírování objektů do produkce  
    b) Žádný Git, pouze deployment pipelines  
    c) Git pro kód a definice + database projects pro schéma + deployment pipelines pro přesun obsahu mezi prostředími  
    d) Pouze databázové projekty bez pipelines  
    **Správná odpověď:** c)
    
5. **Proč je vhodné mít Dev, Test a Prod jako oddělené workspaces zapojené v jedné deployment pipeline?**  
    a) Kvůli zjednodušení účtování licencí  
    b) Aby bylo možné testovat změny izolovaně a až poté je řízeně nasadit do produkce  
    c) Aby bylo možné nasazovat pouze celé tenantry  
    d) Protože Fabric jinak nepovolí vytvářet pipelines  
    **Správná odpověď:** b)
    

---
---

# 3. Security, Governance & Orchestration

Toto téma řeší, kdo k čemu ve Fabricu může, jak se chrání a kategorizují data a jak se orchestrace používá pro řízené zpracování.  
Jde o kombinaci přístupových práv (workspace, item, RLS/CLS/OLS), klasifikace (sensitivity labels, endorsement) a orchestrací (pipelines, notebooks, triggery).

---

## 3.1 Workspace‑level access controls

- Workspace je kontejner pro artefakty; přístup na úrovni workspace určuje, kdo je vůbec „uvnitř“ a co tam smí dělat.
    
- Typické role: admin (správa workspace a práv), member/contributor (tvorba a úpravy obsahu), viewer/reader (pouhé čtení a používání).
    

Klíčové body:

- Workspace role se dědí na položky, pokud není detailnější nastavení na úrovni itemu.
    
- Přístup na workspace úrovni je prvotní bariéra – kdo se nedostane do workspace, neuvidí ani jeho obsah.
    

---

## 3.2 Item‑level access controls

- Item = konkrétní artefakt (dataset, report, notebook, pipeline atd.).
    
- Item‑level oprávnění mohou přepsat nebo zpřesnit děděná workspace práva – např. jen určité osoby mohou dataset upravovat, i když mají širší práva ve workspace.
    

Důležité:

- U klíčových objektů (např. sdílené semantic modely) se často používá jemnější řízení přístupu na úrovni itemu.
    
- Item‑level přístup umožňuje scénáře typu „širší tým má přístup do workspace, ale citlivý dataset vidí jen omezená skupina“.
    

---

## 3.3 RLS, CLS, OLS a File‑level access

- RLS (Row‑Level Security): omezuje, které řádky v tabulkách může konkrétní uživatel vidět (např. regionální manažer vidí jen svůj region).
    
- OLS (Object‑Level Security): skrývá celé tabulky nebo sloupce – některé objekty modelu pro určité uživatele vůbec „neexistují“.
    

Další prvky:

- CLS (Column/Cell‑Level Security) / file‑level access: řízení přístupu na úrovni sloupců nebo souborů v úložišti.
    
- Tyto mechanismy se často kombinují – např. RLS na řádky + OLS na vybrané tabulky, aby se minimalizovalo riziko odhalení citlivých dat.
    

---

## 3.4 Dynamic Data Masking

- Dynamické maskování dat zakrývá citlivé údaje při čtení, aniž by měnilo data fyzicky v databázi.
    
- Typicky se používá pro osobní údaje (např. zobrazit jen část telefonního čísla či e‑mailu).
    

Hlavní myšlenka:

- Uživatelé s plnými právy vidí plná data, zatímco ostatní vidí „maskovanou“ verzi podle nastavených pravidel.
    
- Maskování doplňuje, ale nenahrazuje RLS/OLS – jde o další vrstvu ochrany.
    

---

## 3.5 Sensitivity labels

- Sensitivity labels označují, jak citlivá jsou data (např. veřejné, interní, důvěrné, vysoce důvěrné).
    
- Tyto štítky mohou ovlivnit chování nástrojů: šifrování, omezení sdílení, varování uživatelům apod.
    

Důležité:

- Štítky se mohou přenášet spolu s daty – např. z datasetu do reportu.
    
- Konzistentní používání sensitivity labels je základ datové governance v organizaci.
    

---

## 3.6 Item endorsement

- Endorsement (např. „promoted“, „certified“) vyjadřuje, že určitý dataset nebo report je doporučený/ověřený pro použití.
    
- Pomáhá uživatelům najít důvěryhodné zdroje mezi mnoha podobnými objekty.
    

Klíčové body:

- „Certified“ obvykle znamená, že objekt prošel formálním schvalovacím procesem (např. BI tým, data governance tým).
    
- Endorsement = část governance na úrovni obsahu, ne čistě bezpečnost, ale úzce na ni navazuje.
    

---

## 4. Orchestration (Data Pipelines, Notebooks, Triggers)

- Orchestrace řídí pořadí, závislosti a plánování datových úloh ve Fabricu.
    
- Hlavní stavební prvky: data pipelines, notebooks a triggery (časové, event‑based atd.).
    

## 4.1 Orchestrace s Data Pipeline

- Data pipeline spojuje jednotlivé aktivity (kopírování dat, spouštění notebooku, volání REST API atd.) do jednoho toku.
    
- Umožňuje definovat závislosti, podmíněné větvení a paralelní běhy.
    

## 4.2 Orchestrace s Notebookem

- Notebook může fungovat jako krok v pipeline nebo samostatná orchestrující jednotka (např. pomocí knihoven, které spouští další úlohy).
    
- Vhodné, když potřebuješ flexibilní logiku, cykly nebo komplexní rozhodování.
    

## 4.3 Triggery

- Triggery definují, kdy a proč se orchestrace spustí – plán (schedule), událost (např. příchod souboru), ruční spuštění.
    
- V kombinaci s pipelines a notebooks tvoří kompletní ETL/ELT workflow.
    

---

# Q&A bloky (s odpověďmi)

**Q1: Jaký je rozdíl mezi workspace‑level a item‑level access controls?**  
**A1:** Workspace‑level přístup určuje, kdo může vstoupit do workspace a obecně pracovat s jeho obsahem, zatímco item‑level přístup zpřesňuje oprávnění pro konkrétní artefakty (datasety, reporty, pipelines) uvnitř workspace.

---

**Q2: Kdy použít RLS a kdy OLS?**  
**A2:** RLS používáš, když chceš filtrovat řádky podle uživatele (např. jen jeho region), OLS když potřebuješ některé tabulky nebo sloupce úplně skrýt před určitými uživateli.

---

**Q3: Jaký problém řeší Dynamic Data Masking?**  
**A3:** Umožňuje zobrazit citlivé údaje jen částečně nebo v anonymizované podobě pro uživatele, kteří nemají plná oprávnění, aniž by se měnila skutečná data v databázi.

---

**Q4: Jaký je praktický přínos sensitivity labels v datové platformě?**  
**A4:** Umožňují jednotně označit citlivost dat, vynutit dodatečná bezpečnostní opatření (např. šifrování, omezení sdílení) a přenášet informaci o klasifikaci napříč datovými artefakty.

---

**Q5: Proč je endorsement důležitý pro běžné uživatele reportů a datasetů?**  
**A5:** Pomáhá jim rychle rozpoznat, které zdroje jsou důvěryhodné a schválené, takže se mohou vyhnout použití neověřených nebo zastaralých datasetů.

---

**Q6: Jaký je rozdíl mezi orchestrací přes data pipeline a orchestrací přes notebook?**  
**A6:** Data pipeline je vizuální nástroj pro skládání aktivit a jejich závislostí, zatímco notebook poskytuje flexibilní programovatelnou orchestraci, vhodnou pro složitější logiku a dynamická rozhodnutí.

---

**Q7: Jakou roli hrají triggery v orchestracech?**  
**A7:** Triggery určují, kdy se orchestrace spustí (čas, událost, ručně), díky čemuž lze automatizovat běh datových workflow bez manuálního zásahu.

---

# Kvízové otázky (styl zkoušky)

1. **Které tvrzení nejlépe vystihuje účel workspace‑level access controls?**  
    a) Řídí pouze maskování citlivých polí v tabulkách  
    b) Definují, kdo má přístup do workspace a jaké má v něm role  
    c) Používají se výhradně pro řízení přístupu k souborům v OneLake  
    d) Ovlivňují jen to, kdo může vytvářet triggery  
    **Správná odpověď:** b)
    
2. **Jaký scénář je typický pro použití Row‑Level Security (RLS)?**  
    a) Skrytí celé faktové tabulky před konkrétní skupinou uživatelů  
    b) Zobrazení pouze záznamů odpovídajících uživatelovu regionu nebo týmu  
    c) Maskování čísel kreditních karet  
    d) Omezování exportu dat do Excelu  
    **Správná odpověď:** b)
    
3. **Co je primárním cílem Dynamic Data Masking?**  
    a) Trvale anonymizovat data v databázi  
    b) Zrychlit dotazy nad velkými tabulkami  
    c) Dočasně zakrýt citlivé hodnoty pro určité uživatele při čtení dat  
    d) Vynutit šifrování na disku  
    **Správná odpověď:** c)
    
4. **Která kombinace nejlépe popisuje roli sensitivity labels a item endorsement?**  
    a) Labels pro výkon, endorsement pro zálohování  
    b) Labels popisují citlivost dat, endorsement označuje doporučené/ověřené zdroje  
    c) Obě funkce slouží jen k omezení exportu do PDF  
    d) Labels se používají jen v databázi, endorsement jen v pipelines  
    **Správná odpověď:** b)
    
5. **K čemu se v rámci orchestrace používají triggery?**  
    a) K verzování pipeline  
    b) K definování, jaké role má uživatel ve workspace  
    c) K určování, kdy a za jakých podmínek se pipeline nebo notebook spustí  
    d) K nastavování sensitivity labels na datasety  
    **Správná odpověď:** c)
    
---
---
# 4. Data Loading Patterns & Ingestion

Tohle téma je o tom, jak data do Fabricu dostat a v jakém režimu je načítat: plně, inkrementálně, dimenzionálně a přes různé ingestion možnosti (storage, nástroje, shortcuts, mirroring, pipelines).  
Z pohledu DP‑700 je důležité umět vybrat vhodný vzor načítání a správný ingestion přístup pro konkrétní scénář.

---

## 4.1 Full a Incremental loading

**Full load**

- Při full loadu se cílová tabulka pro daná data vždy kompletně přepíše.
    
- Vhodné, když je objem dat malý, load je rychlý a nepotřebuješ držet historii v cíli.
    

**Incremental load**

- Načítají se jen nová nebo změněná data oproti předchozímu běhu (např. podle data změny, watermarku, identity).
    
- Šetří čas i kapacitu a je nezbytný u větších tabulek a near‑real‑time scénářů.
    

Klíčové pro zkoušku:

- Znát výhody/nevýhody: full load je jednodušší, ale méně efektivní; incremental je složitější, ale škáluje lépe a zachovává historii.
    

---

## 4.2 Loading do dimenzionálního modelu

- Dimenzionální model = faktové tabulky (měření) + dimenze (popisné atributy).
    
- Načítání vyžaduje dobré zvládnutí klíčů (business keys, surrogate keys) a typů změn (SCD).
    

Hlavní principy:

- Fakty se typicky načítají inkrementálně podle času vzniku/záznamu.
    
- Dimenze se často načítají jako SCD (Slowly Changing Dimensions):
    
    - SCD1 – přepis hodnot (bez historie)
        
    - SCD2 – zakládání nových řádků pro změny (s historií)
        

---

## 4.3 Volba data store (6.1 Choosing a data store)

- Ve Fabricu můžeš ukládat data do různých typů úložišť (lakehouse, warehouse, external storage atd.).
    
- Volba závisí na typu workloadu: analytický SQL, lakehouse, reporting, ad‑hoc analýza, near‑real‑time atd.
    

Příklady úvah:

- Pro strukturované analytické dotazy je vhodné warehouse nebo lakehouse tabulky v delta formátu.
    
- Pro syrová data z více zdrojů bývá start v lakehouse (bronze layer).
    

---

## 4.4 Volba transformačního nástroje (6.2 Choosing a data transformation tool)

- Fabric nabízí více nástrojů pro transformace: T‑SQL, PySpark, Dataflows, Data Factory‑style aktivity v pipelines atd.
    
- Výběr nástroje záleží na typu uživatele, dat a požadovaném výkonu.
    

Typické volby:

- T‑SQL: když máš převážně relační data a silný SQL skillset.
    
- PySpark: pro distribuované zpracování velkých objemů dat a komplexní transformace.
    
- Dataflows: pro self‑service a GUI‑orientované transformace, podobné Power Query.
    

---

## 4.5 Shortcuts (6.3)

- Shortcut je logický odkaz na data uložená někde jinde (jiný lake, jiný storage účet, jiná složka).
    
- Umožňuje „připojit“ externí data do OneLake/Fabric bez jejich fyzického kopírování.
    

Důležité:

- Šetří storage a zjednodušuje sdílení dat mezi týmy a doménami.
    
- Vhodné, když nechceš duplikovat data, ale potřebuješ s nimi pracovat, jako by byla součástí tvého lakehouse/warehouse.
    

---

## 4.6 Mirroring (6.4)

- Mirroring vytváří „zrcadlo“ externí databáze ve Fabricu, která se průběžně synchronizuje.
    
- Vhodné pro scénáře, kdy potřebuješ reporting/analytics nad operační databází bez velkého vývojového úsilí kolem ETL.
    

Klíčové body:

- Cílem je minimalizovat latenci mezi zdrojovým systémem a analytickou kopií ve Fabricu.
    
- Mirroring může výrazně zjednodušit ingestion architekturu, ale je potřeba řešit výkon a dopady na zdroj.
    

---

## 4.7 Data ingestion s Data Pipelines (6.5)

- Data pipelines jsou hlavní orchestrátor ingestion procesů: získání dat, transformace, uložení do cílového modelu.
    
- Podporují různé konektory, kopírovací aktivity, volání notebooks, rozdělení na fáze (bronze–silver–gold).
    

Důležité:

- Pipelines umožňují opakovatelné, plánované načítání a dobře se integrují s monitorováním a alerty.
    
- Snadno v nich uplatníš full i incremental load pattern.
    

---

# Q&A bloky (s odpověďmi)

**Q1: Kdy je vhodnější použít full load místo incremental load?**  
**A1:** Když je tabulka relativně malá, načítání je rychlé a nevyžaduješ zachování historie v cílovém systému, takže kompletní přepis nevadí.

---

**Q2: Jaký je hlavní přínos incremental loadu oproti full loadu?**  
**A2:** Načítá jen nová nebo změněná data, čímž snižuje přenosy, zátěž i dobu běhu a lépe škáluje u velkých tabulek nebo častých refreshů.

---

**Q3: Proč je důležité rozlišovat mezi fakty a dimenzemi při načítání do dimenzionálního modelu?**  
**A3:** Fakty reprezentují měření a typicky se načítají inkrementálně podle času, zatímco dimenze nesou popisné informace a často vyžadují SCD logiku pro sledování historie atributů.

---

**Q4: Jaké faktory zvažuješ při výběru datového úložiště ve Fabricu?**  
**A4:** Typ workloadu (SQL analýza vs. lakehouse), objem a strukturu dat, požadavky na výkon, typ uživatelů a to, zda budeš potřebovat syrovou vrstvu nebo spíš hotový warehouse.

---

**Q5: Kdy dává smysl použít PySpark místo T‑SQL pro datové transformace?**  
**A5:** Když potřebuješ distribuované zpracování velkých objemů dat, komplexní transformace nebo integraci s Python ekosystémem, kde samotný SQL už nestačí.

---

**Q6: Jaký problém řeší Shortcuts v kontextu ingestion?**  
**A6:** Umožňují pracovat s daty uloženými mimo tvůj workspace nebo dokonce mimo OneLake, aniž bys je musel fyzicky kopírovat, čímž šetří storage a odstraňují zbytečnou duplicitu.

---

**Q7: V čem se liší mirroring od klasického kopírování dat?**  
**A7:** Mirroring udržuje průběžně synchronizované „zrcadlo“ zdrojové databáze ve Fabricu, zatímco klasický kopírovací proces obvykle provádí dávkové (batch) loady s většími odstupy.

---

**Q8: Jakou roli hrají Data Pipelines v ingestion scénářích?**  
**A8:** Slouží jako orchestrátor, který propojuje zdroje, transformace a cíle do jednoho řízeného workflow s možností plánování, monitoringu a opakovatelného běhu.

---

# Kvízové otázky (styl zkoušky)

1. **Které tvrzení nejlépe popisuje incremental loading?**  
    a) Při každém běhu přepíše celou cílovou tabulku  
    b) Načítá pouze nová nebo změněná data od posledního běhu  
    c) Slouží jen pro real‑time streaming  
    d) Vždy ignoruje historická data  
    **Správná odpověď:** b)
    
2. **Jaký je typický způsob práce s dimenzemi typu SCD2?**  
    a) Vždy se přepíše existující řádek bez historie  
    b) Nové hodnoty se ukládají do samostatné cache tabulky  
    c) Při změně atributu se uzavře starý řádek a vloží se nový s aktualizovanými daty  
    d) SCD2 se používá jen pro faktové tabulky  
    **Správná odpověď:** c)
    
3. **Která kombinace nejlépe vystihuje volbu transformačního nástroje ve Fabricu?**  
    a) T‑SQL pro velká nestrukturovaná data, PySpark jen pro malé tabulky  
    b) T‑SQL pro relační analytické scénáře, PySpark pro distribuované big‑data transformace  
    c) Dataflows jsou jediný podporovaný nástroj  
    d) Transformace jsou vždy jen v notebooks  
    **Správná odpověď:** b)
    
4. **Které tvrzení nejlépe vystihuje Shortcuts?**  
    a) Jsou to zálohy tabulek ve Fabricu  
    b) Fyzicky duplikují všechna zdrojová data do OneLake  
    c) Představují logické odkazy na externí data, se kterými lze pracovat, jako by byla součástí tvého lakehouse  
    d) Slouží pouze pro streaming data  
    **Správná odpověď:** c)
    
5. **Proč bys zvolil mirroring pro integrační scénář nad OLTP databází?**  
    a) Protože znemožní přístup do zdrojové databáze  
    b) Protože umožní mít průběžně aktualizovanou analytickou kopii databáze ve Fabricu s minimálním vývojovým úsilím kolem tradičního ETL  
    c) Protože nahrazuje potřebu data warehouse  
    d) Protože je vhodný pouze pro historická data  
    **Správná odpověď:** b)
    
---
---
