# 1. Úvod k DP‑700 & Bootcampu

Tento bod je rámcem pro celou tvou „skládačku“ – shrnuje, co DP‑700 pokrývá a jak na to bootcamp navazuje.  
Obsahuje strukturu témat, která sis už rozepsal jako body 2–10 (lifecycle, security, loading, ingestion, real‑time, monitoring, exam tips).

---

## 1.1 Co se od DP‑700 očekává

- Zkouška ověřuje schopnost navrhovat, budovat a spravovat řešení na Microsoft Fabric: workspace nastavení, lifecycle, zabezpečení, ingest, transformace, real‑time a monitoring.
    
- Důraz je na architektonické volby (správný nástroj/pattern pro scénář), ne jen na klikání v UI.
    

---

## 1.2 Struktura studijních témat (tvoje „kapitoly“ 1–10)

- 1: Fabric Workspace Settings – základní konfigurace prostředí.
    
- 2: Lifecycle Management – verzování, deployment, databázové projekty.
    
- 3: Security & Governance – přístupy, RLS/OLS, sensitivity, endorsement.
    
- 4–6: Loading, Ingestion, T‑SQL/PySpark, Real‑time – jak dostat data dovnitř a zpracovat je správným nástrojem.
    
- 7–8: Monitoring & Optimization – jak hlídat běhy, chyby a výkon datových úložišť.
    
- 9: Exam Technique – jak z těchto znalostí vytěžit co nejvíc bodů u samotné zkoušky.
    

---

## 1.3 Jak s touhle strukturou pracovat

- Každý bod 1–10 brát jako samostatnou kapitolu v Obsidianu s tvými Q&A a kvízy, které už máš.
    
- V průběhu přípravy se vracet k tomuto „obsahu“ a kontrolovat, že nemáš slabé slepé místo v žádné z kapitol.
    
---
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
# 5. T‑SQL a PySpark pro ingest, transformace a loading

Téma 5 je o tom, jak použít T‑SQL a PySpark k načítání, úpravám a ukládání dat ve Fabricu, a kdy který přístup zvolit.  
Cílem je rozumět typickým úlohám (ingest, transformace, loading do modelu) a mít jasno v rozdílech mezi SQL a Spark přístupem.

---

## 5.1 T‑SQL – kdy a proč

- T‑SQL je ideální pro relační, strukturovaná data a analytické dotazy nad warehouse či lakehouse tabulkami.
    
- Typické scénáře: čištění dat, agregace, joiny, příprava fact/dim tabulek, implementace SCD logiky (zejména SCD1/2) v SQL.
    

Výhody:

- Silná optimalizace query enginu, známý jazyk pro datové inženýry/analytiky, dobrá integrace s BI vrstvou.
    
- Hodí se, když data už jsou v tabulkovém tvaru a nepotřebuješ extrémně custom logiku nebo práci s nestrukturovanými daty.
    

---

## 5.2 PySpark – kdy a proč

- PySpark využívá distribuované zpracování nad Sparkem, vhodné pro velké objemy dat a složitější datové transformace.
    
- Umí pracovat jak se strukturovanými, tak polostrukturovanými a nestrukturovanými daty (JSON, logy, soubory).
    

Výhody:

- Horizontální škálování, možnost psát komplexní logiku v Pythonu, integrace s knihovnami (např. pro data quality, ML).
    
- Vhodné pro scénáře, kde T‑SQL naráží na limity (objem, typ dat, komplexita transformací).
    

---

## 5.3 T‑SQL vs. PySpark pro ingest/transform/load

- Pro jednodušší ETL uvnitř relačního světa (warehouse, star schema) dává smysl primárně T‑SQL.
    
- Pro lakehouse scénáře, velké datové sady, vícestupňové transformace a kombinaci formátů dat se typicky hodí PySpark.
    

Důležité pro DP‑700:

- Oba přístupy můžeš míchat v jednom řešení – např. ingest + heavy transformace v PySpark, finální modelování pro reporting v T‑SQL.
    
- Volba nástroje závisí i na skillsetu týmu a provozním modelu (SQL‑centrický vs. data‑engineering/Big Data tým).
    

---

# Q&A bloky (s odpověďmi)

**Q1: Kdy zvolit T‑SQL pro datové transformace ve Fabricu?**  
**A1:** Když pracuješ hlavně se strukturovanými relačními daty, potřebuješ dělat joiny, agregace a přípravu fact/dim tabulek v prostředí warehouse/lakehouse, a výkon SQL enginu je dostačující.

---

**Q2: Jaké typy úloh jsou typicky vhodné pro PySpark?**  
**A2:** Zpracování velkých objemů dat, komplexní transformační pipeline, práce s polostrukturovanými daty (např. JSON), kombinace více formátů a scénáře, kde potřebuješ výhody distribuovaného výpočtu.

---

**Q3: Proč dává smysl kombinovat T‑SQL a PySpark v jednom řešení?**  
**A3:** Protože můžeš využít silné stránky obou: PySpark pro heavy‑lifting a ingest v lakehouse, T‑SQL pro finální modelování a jemné ladění relačních struktur pro reporting.

---

**Q4: Jaký dopad má výběr mezi T‑SQL a PySpark na tým a provoz?**  
**A4:** T‑SQL lépe sedí SQL‑orientovaným týmům a klasickému BI, zatímco PySpark vyžaduje data‑engineering skillset a práci se Spark clustery, ale přináší lepší škálování pro big‑data scénáře.

---

# Kvízové otázky (styl zkoušky)

1. **Které tvrzení nejlépe popisuje použití T‑SQL ve Fabricu?**  
    a) Je určené výhradně pro streaming scénáře  
    b) Slouží k relační analýze a transformacím nad strukturovanými daty v warehouse/lakehouse  
    c) Používá se jen pro správu uživatelských rolí  
    d) Nahrazuje potřebu PySpark  
    **Správná odpověď:** b)
    
2. **Kdy je nejvhodnější sáhnout po PySpark místo T‑SQL?**  
    a) U malých tabulek s několika stovkami řádků  
    b) Když potřebuješ uložit metadata o reportech  
    c) Když zpracováváš velké objemy dat nebo různorodé formáty a chceš využít distribuované výpočty  
    d) Jen při návrhu datového modelu v Power BI  
    **Správná odpověď:** c)
    
3. **Jaký přístup odpovídá „hybridnímu“ použití T‑SQL a PySpark?**  
    a) Všechno v T‑SQL, PySpark se vůbec nepoužívá  
    b) Všechno v PySpark, SQL je zakázané  
    c) Ingest a těžké transformace v PySpark, finální modelování a připrava dat pro reporting v T‑SQL  
    d) Oba nástroje se používají jen pro monitoring  
    **Správná odpověď:** c)
    
---
---
# 6. Real‑time (Eventstreams, Eventhouse, KQL)

Téma 6 se zaměřuje na real‑time architekturu ve Fabricu: příjem událostí (eventstreams), jejich ukládání a analýzu (Eventhouse/KQL DB) a dotazování pomocí KQL.  
Cílem je chápat základní komponenty reálného času a kdy dává smysl je použít oproti batch scénářům.

---

## 6.1 Eventstreams – příjem dat v reálném čase

- Eventstream je služba, která přijímá proud dat v reálném čase z různých zdrojů (senzory, aplikace, logy, event hubs, MQTT apod.).
    
- Umožňuje data směrovat paralelně do více cílových systémů (např. Eventhouse/KQL DB, lakehouse, Power BI).
    

Klíčové vlastnosti:

- Schopnost transformovat a filtrovat události už při průchodu streamem (např. enrich, filtry, mapování schématu).
    
- Podpora oken (windows) – časové, počítané atd. pro agregace v reálném čase (počty, průměry, threshold alerty).
    

---

## 6.2 Eventhouse / KQL Database

- Eventhouse (KQL Database) je úložiště optimalizované pro časové a logovací data, nad kterými se provádějí KQL dotazy.
    
- Je navrženo pro vysoké rychlosti ingestu a rychlé ad‑hoc dotazy nad velkým objemem událostí.
    

Důležité pro zkoušku:

- Typický scénář: Eventstream zapisuje do KQL DB, kde se pak dělá analýza, monitorování, detekce anomálií či dashboardy.
    
- KQL DB je sloupcově orientovaná databáze s podporou time‑series a retention politik (uchování dat po určitou dobu).
    

---

## 6.3 KQL – dotazovací jazyk pro real‑time/log data

- KQL (Kusto Query Language) je jazyk určený primárně pro dotazy nad logy a událostmi – má silnou podporu filtrování, agregací, joinů a time‑series funkcí.
    
- Syntakticky připomíná potrubní (pipe) styl: výsledek jedné operace se posouvá do další.
    

Typické použití:

- Filtrování událostí podle času, typu, zdroje.
    
- Agregace nad sliding/ tumbling okny, detekce anomálií, korelace více datových proudů.
    

---

# Q&A bloky (s odpověďmi)

**Q1: Jakou roli hraje Eventstream v real‑time architektuře Fabricu?**  
**A1:** Slouží jako vstupní a směrovací vrstva pro příjem událostí v reálném čase ze zdrojů a jejich distribuci do cílových systémů (např. KQL DB, lakehouse, dashboardy).

---

**Q2: Proč je vhodné ukládat real‑time události do Eventhouse/KQL DB?**  
**A2:** Protože KQL DB je optimalizovaná pro vysokorychlostní ingest, časové dotazy a analýzu logů/událostí, takže umožňuje rychlé vyhodnocování a monitorování nad velkým objemem dat.

---

**Q3: V čem se KQL liší od klasického T‑SQL?**  
**A3:** KQL je zaměřené na dotazy nad logy a časovými daty s podporou pipe stylu, time‑series funkcí a interaktivní analýzy, zatímco T‑SQL je obecný relační jazyk pro OLTP/OLAP tabulky.

---

**Q4: Jak mohou Eventstreams a KQL spolupracovat v jednom scénáři?**  
**A4:** Eventstreams přijímá události a zapisuje je do KQL DB, kde následně KQL dotazy vyhodnocují metriky, detekují anomálie nebo pohánějí real‑time dashboardy.

---

# Kvízové otázky (styl zkoušky)

1. **Které tvrzení nejlépe popisuje Eventstream ve Fabricu?**  
    a) Je to dávkový nástroj pro nightly load  
    b) Je to služba pro příjem a směrování proudů událostí v reálném čase  
    c) Je to vizuální editor Power BI reportů  
    d) Je to jen lokální cache dat  
    **Správná odpověď:** b)
    
2. **Kdy je vhodné použít Eventhouse/KQL Database pro ukládání dat?**  
    a) Když potřebuješ uložit referenční dimenze s nízkou frekvencí změn  
    b) Když ukládáš binární soubory pro data lake  
    c) Když potřebuješ ukládat a analyzovat vysokofrekvenční logy a eventy s podporou rychlých časových dotazů  
    d) Když chceš hostovat OLTP aplikaci  
    **Správná odpověď:** c)
    
3. **Jaký typ operací je pro KQL typický?**  
    a) Transakční INSERT/UPDATE s důrazem na referenční integritu  
    b) Filtrování, agregace a analýza nad logy a časovými řadami v pipe stylu  
    c) Vytváření Power BI vizuálů  
    d) Nasazování databázových schémat  
    **Správná odpověď:** b)
    
4. **Proč se v real‑time scénářích často kombinuje Eventstream a KQL?**  
    a) Protože Eventstream ukládá data jen lokálně bez možnosti dotazování  
    b) Protože KQL slouží k definování směrování v Eventstreamu  
    c) Protože Eventstream spolehlivě doručí data do KQL DB, kde je možné je rychle analyzovat a vizualizovat  
    d) Protože KQL je jediný způsob, jak vytvořit Eventstream  
    **Správná odpověď:** c)
    
---
---
# 7. Monitoring, Errors & Optimization (část 1)

Téma 7 je o tom, jak ve Fabricu sledovat výkon a chyby, a jak optimalizovat platformu i jednotlivé nástroje z pohledu DP‑700.  
Rozpadá se na monitoring/optimalizaci celé platformy a monitoring/optimalizaci konkrétních datových nástrojů (pipelines, dataflows, Spark, eventstream).

---

## 7.1 Monitoring & optimalizace Fabric platformy

## Monitoring Hub

- Centrální místo pro přehled aktivit v rámci Fabricu: běhy pipeline, refresh datasetů, Spark joby, chyby a varování.
    
- Umožňuje filtrovat podle typu nástroje, času, stavu (success/fail) a rychle se prokliknout k detailu konkrétního běhu.
    

## Capacity Metrics App

- Slouží ke sledování využití kapacity (Fabric/Azure capacities): CPU, paměť, query load, concurrency atd.
    
- Pomáhá identifikovat, zda jsou problémy způsobeny limity kapacity (přetížení, throttling), nebo chybně navrženými dotazy/pipeline.
    

## Workspace Monitoring (preview)

- Poskytuje detailnější pohled na aktivity a výkon konkrétního workspace: jaké objekty běží, jak dlouho, s jakou chybovostí.
    
- Vhodné pro týmový pohled na jeden projekt / doménu bez nutnosti sledovat celý tenant.
    

---

## 7.2 Monitoring/optimalizace datových nástrojů

## Data Pipelines

- Sleduje se stav jednotlivých aktivit v pipeline (success/fail/skipped), doby běhu, počty zpracovaných řádků a chybové zprávy.
    
- Optimalizace zahrnuje paralelizaci, správné nastavení partitioningů, omezení zbytečných kopií dat a vhodné retrypy/error‑handling.
    

## Dataflow Gen2

- Monitoring zahrnuje kontrolu refreshů, délku běhů a míru chyb (např. chybné řádky, timeouty, problémy se zdrojem).
    
- Optimalizuje se správnou volbou transformací, filtrováním co nejblíže zdroji a omezením zbytečně komplikovaných kroků Power Query.
    

## Spark Notebook / Spark Job Definition

- Sledují se Spark joby (stages, tasks), využití executors, shuffles, cache a chybové logy.
    
- Optimalizace cílí na správné partitioningy, redukci shuffle operací, využití cache/persist a vhodné nastavení velikosti clusteru.
    

## Eventstream

- Monitoruje se příjem událostí (throughput), latence, chybné zprávy a výpadky cílových sinků.
    
- Optimalizace spočívá v ladění filtrů, mapování schémat a správném nastavení cílových úložišť, aby stíhala ingest.
    

---

# Q&A bloky (s odpověďmi)

**Q1: K čemu slouží Monitoring Hub ve Fabricu?**  
**A1:** Je to centrální přehled běhů a stavů aktivit napříč Fabric nástroji (pipelines, refresh, Spark atd.), který umožňuje rychle dohledat, co selhalo a proč.

---

**Q2: Jaký typ informací získáš z Capacity Metrics App?**  
**A2:** Přehled o využití kapacity – CPU, paměť, zátěž dotazů a případný throttling – což pomáhá odlišit problémy způsobené limity kapacity od problémů v samotném řešení.

---

**Q3: V čem je přínos Workspace Monitoring oproti globálnímu pohledu?**  
**A3:** Zaměřuje se na konkrétní workspace, takže tým vidí jen aktivity a výkon svého projektu, což usnadňuje cílené ladění a troubleshooting.

---

**Q4: Jaké základní metriky sleduješ u Data Pipelines?**  
**A4:** Stav aktivit (success/fail), dobu běhu, počty zpracovaných dat a konkrétní chybové zprávy u selhaných kroků.

---

**Q5: Jak můžeš optimalizovat Dataflow Gen2?**  
**A5:** Filtrovat data co nejblíže zdroji, zjednodušit transformační kroky, vyhnout se nadbytečným merge a složitým krokům, které zbytečně prodlužují refresh.

---

**Q6: Na co se zaměřit při ladění výkonu Spark úloh ve Fabricu?**  
**A6:** Na partitioning dat, minimalizaci shuffle, efektivní využití cache, vhodnou velikost clusteru a analýzu stages/tasks v job detailu.

---

**Q7: Jaké jsou typické signály problémů v Eventstreamu?**  
**A7:** Zvýšená latence, nečekané snížení throughputu, rostoucí počet chybových zpráv nebo problémy s doručováním do cílových sinků.

---

# Kvízové otázky (styl zkoušky)

1. **Které tvrzení nejlépe popisuje roli Monitoring Hubu?**  
    a) Slouží k nastavování sensitivity labels  
    b) Je centrálním místem pro sledování běhů a stavů aktivit napříč Fabric nástroji  
    c) Umožňuje jen konfiguraci kapacit  
    d) Je určený pouze pro Spark workloady  
    **Správná odpověď:** b)
    
2. **Kdy je vhodné použít Capacity Metrics App při troubleshootingu?**  
    a) Když potřebuješ vytvořit nový workspace  
    b) Když chceš zjistit, zda jsou výkonnostní problémy způsobené přetíženou kapacitou  
    c) Když nastavuješ RLS pravidla  
    d) Když hledáš Power BI vizuály  
    **Správná odpověď:** b)
    
3. **Jaký typ informací je nejdůležitější sledovat u selhané Data Pipeline?**  
    a) Počet uživatelských licencí  
    b) Grafickou podobu ikon v pipeline  
    c) Stav aktivit, chybové zprávy a doby běhu jednotlivých kroků  
    d) Počet vytvořených dashboards  
    **Správná odpověď:** c)
    
4. **Na jaké aspekty se zaměřit při optimalizaci Spark jobu?**  
    a) Jen na počet workspace uživatelů  
    b) Na partitioning, shuffle, využití cache a nastavení velikosti clusteru  
    c) Jen na barvu tématu notebooku  
    d) Pouze na počet sloupců v tabulce  
    **Správná odpověď:** b)
    
5. **Co může naznačovat problém v Eventstreamu?**  
    a) Zvýšení počtu workspaces  
    b) Změna názvu kapacity  
    c) Rostoucí latence, snížení throughputu nebo nárůst chyb při doručování do cílových systémů  
    d) Přidání nového uživatele do tenant  
    **Správná odpověď:** c)
    
---
---
# 8. Monitoring, Errors & Optimization (část 2 – Data Stores)

Téma 8 se soustředí na sledování a ladění jednotlivých úložišť: Data Warehouse, Lakehouse, Eventhouse a Semantic model refresh.  
Cílem je umět poznat, kde vzniká bottleneck, a znát hlavní páky, jak výkon zlepšit.

---

## 8.1 Data Warehouse – monitoring a optimalizace

- Sledují se hlavně dotazy (query duration, CPU, IO), blokace a paralelismus, případně fronty požadavků.
    
- Pro výkon jsou zásadní vhodné indexy/clustered columnstore, správné rozložení dat a omezení zbytečných full‑scan dotazů.
    

Optimalizační principy:

- Psaní efektivních dotazů (filtry, joiny na vhodných klíčích, omezení SELECT *).
    
- Správný návrh schématu (star schema, denormalizace pro analytické dotazy) a péče o statistiky.
    

---

## 8.2 Lakehouse – monitoring a optimalizace

- Sleduje se výkon Spark úloh nad lakehouse (jobs, stages, čtení/zápis souborů, shuffles).
    
- Důležitý je formát a organizace souborů (Delta, velikost souborů, partitioning, počet malých souborů).
    

Optimalizační principy:

- Používat Delta formát, rozumný partitioning a pravidelný compaction (omezit „small files problem“).
    
- Minimalizovat zbytečné přepisy a preferovat append/merges s vhodnými filtry.
    

---

## 8.3 Eventhouse – monitoring a optimalizace

- Sledují se rychlost ingestu, latence dotazů v KQL, využití uložiště a retention nastavení.
    
- Příliš dlouhá retence nebo neefektivní dotazy (bez filtrů na čas/klíče) mohou výrazně zpomalit analýzu.
    

Optimalizační principy:

- Vždy filtrovat podle času a relevantních polí, používat vhodné agregace a shrnutí (aggregation tables).
    
- Nastavit rozumnou retenci dat a případně archivaci starších logů mimo hlavní KQL DB.
    

---

## 8.4 Semantic model refresh – monitoring a optimalizace

- Sleduje se doba refreshů, frekvence, chybovost a vliv na kapacitu (CPU, paměť během refreshů).
    
- Dlouhé nebo často padající refreshe jsou signál, že model, dotazy nebo zdrojová data potřebují úpravy.
    

Optimalizační principy:

- Používat incremental refresh, filtraci na zdroji a efektivní dotazy (omezit náročné transformace během refresh).
    
- Udržovat model přiměřeně velký (odmazat nepotřebné sloupce/tabulky, správně nastavit typy a agregace).
    

---

# Q&A bloky (s odpověďmi)

**Q1: Jaké metriky jsou klíčové pro monitoring Data Warehouse?**  
**A1:** Trvání dotazů, využití CPU/IO, případné blokace a fronty požadavků, které ukazují, zda jsou dotazy nebo schema neefektivní.

---

**Q2: Jak může nevhodná organizace souborů ovlivnit výkon Lakehouse?**  
**A2:** Příliš mnoho malých souborů nebo špatný partitioning vede k velké režii při čtení a zpomaluje Spark dotazy i ingest.

---

**Q3: Proč je důležité ve KQL dotazech nad Eventhouse filtrovat podle času?**  
**A3:** Protože tím zúžíš množinu dat, nad kterou se dotaz provádí, což zásadně zrychlí odezvu při práci s velkými objemy událostí.

---

**Q4: Jak incremental refresh pomáhá u semantic modelů?**  
**A4:** Načítá jen novou/změněnou část dat, takže zkracuje dobu refreshů, snižuje zátěž na zdroj i kapacitu a zlepšuje stabilitu.

---

**Q5: Jaké kroky můžeš udělat, pokud semantic model refresh často selhává nebo trvá příliš dlouho?**  
**A5:** Zkontrolovat zdrojové dotazy, aplikovat filtraci na zdroji, zavést incremental refresh, zjednodušit model a odstranit zbytečné sloupce/tabulky.

---

# Kvízové otázky (styl zkoušky)

1. **Co je typickým signálem toho, že Data Warehouse potřebuje optimalizaci?**  
    a) Změna názvu workspace  
    b) Dlouhotrvající dotazy a vysoké využití CPU/IO při běžné zátěži  
    c) Zvýšený počet uživatelů v tenant  
    d) Více sensitivity labels  
    **Správná odpověď:** b)
    
2. **Který problém často zpomaluje dotazy nad Lakehouse?**  
    a) Příliš málo workspaces  
    b) Nadbytek malých souborů a nevhodný partitioning  
    c) Příliš mnoho sensitivity labels  
    d) Nedostatek dashboards  
    **Správná odpověď:** b)
    
3. **Jaký je hlavní důvod pro nastavení rozumné retence v Eventhouse?**  
    a) Zjednodušení licenční správy  
    b) Snížení počtu workspaces  
    c) Omezení objemu dat, nad kterými se dotazuje, a tím zlepšení výkonu i nákladů na storage  
    d) Zákaz použití KQL  
    **Správná odpověď:** c)
    
4. **Kdy je nejvhodnější nasadit incremental refresh v semantic modelu?**  
    a) Když se data vůbec nemění  
    b) Když potřebuješ často obnovovat velké tabulky, které se mění postupně v čase  
    c) Když chceš zrušit všechny RLS role  
    d) Když nechceš používat Power BI  
    **Správná odpověď:** b)
    
5. **Jaký krok ti typicky NEPOMŮŽE zrychlit semantic model refresh?**  
    a) Odstranění nepotřebných sloupců  
    b) Zavedení incremental refresh  
    c) Zjednodušení dotazů na zdroji  
    d) Přidání náhodných výpočtových sloupců bez využití  
    **Správná odpověď:** d)
    
---
---
# 9. Exam Technique and Tips

Téma 9 není o technických detailech Fabricu, ale o tom, jak z DP‑700 vytěžit maximum: jak přistupovat k testu, jak číst otázky a jak si během zkoušky řídit čas a energii.  
Smyslem je udělat z technických znalostí „body v testu“ – tedy umět je správně aplikovat v typických exam scénářích.

---

## 9.1 Strategie před zkouškou

- Projít celou oficiální osnovu a mít u každého bodu alespoň základní jistotu (Workspace settings, Lifecycle, Security, Loading, Real‑time, Monitoring).
    
- Cvičit různé typy otázek: single choice, multiple answer, case study scénáře, kde je potřeba zvolit nejvhodnější variantu, ne „jedinou správnou“.
    

Praktické návyky:

- Jet např. 1–2 bloky denně a dělat si vlastní Q&A (co už děláš v Obsidianu).
    
- Simulovat zkoušku: časový tlak, žádné dohledávání, jen to, co máš v hlavě.
    

---

## 9.2 Strategie během zkoušky

- Nejprve rychle projít otázky a sebrat „low‑hanging fruit“ – co víš hned, odpověz a jdi dál.
    
- U náročnějších scénářů nepřepalovat čas – radši odpovědět co nejlépe a označit pro revizi.
    

Důležité tipy:

- Pečlivě číst zadání: často jsou tam klíčová slova typu „most cost‑effective“, „minimize admin effort“, „near real‑time“, která určují správné řešení.
    
- Dát si pozor na negace („which option should you NOT choose“).
    

---

## 9.3 Jak číst scénáře (case studies)

- Scénáře často kombinují více oblastí (security + ingestion + monitoring); správná odpověď bývá kompromis dle požadavků businessu.
    
- Všímat si omezení: existující nástroje v organizaci, rozpočet, skillset týmu, SLA na latenci atd.
    

Postup:

- Nejprve zjednodušit si scénář: „co vlastně chtějí? real‑time vs batch, levné vs výkonné, minimum správy vs maximum kontroly“.
    
- Až potom vybírat nástroje (Fabric služby) a konkrétní patterny.
    

---

## 9.4 Práce s více správnými odpověďmi

- Některé otázky mají „select TWO“ nebo „select ALL that apply“ – je potřeba hledat kombinaci, ne jen jednu hezkou odpověď.
    
- Často budou možnosti, které jsou sice technicky možné, ale neodpovídají cílovému požadavku (např. zbytečně drahé nebo příliš složité).
    

Tip:

- Eliminuj extrémy: pokud odpověď nereflektuje požadavek na náklady, jednoduchost nebo latency, vyřaď ji.
    
- Hledej páry odpovědí, které se logicky doplňují (např. Git + deployment pipelines, RLS + sensitivity labels).
    

---

## 9.5 Mentální hygiena a time‑management

- Rozdělit si čas: např. cílit na průměr X minut na otázku, s rezervou pro case studies na konci.
    
- Když se zasekneš, dát si max. krátký limit a pak jít dál – neztratit body na jednoduchých otázkách kvůli jedné těžké.
    

Doporučení:

- Před zkouškou spánek a pauza od učení; poslední hodiny použít jen na lehké opakování.
    
- Během testu dýchat, dělat si mikropauzy mezi bloky, aby se nesnížila koncentrace.
    

---

# Q&A bloky (s odpověďmi)

**Q1: Jak bys měl postupovat, když narazíš na dlouhý scénář s více otázkami?**  
**A1:** Nejprve si zjednodušit zadání a identifikovat hlavní požadavky (latence, náklady, správa), pak číst otázky jednu po druhé a u každé hledat řešení přesně pro tento scénář, ne obecně „nejlepší technologii“.

---

**Q2: Jaký je přístup k otázkám, kde existuje více správných možností?**  
**A2:** Hledat dvojici/kombinaci, která nejlépe splňuje všechny požadavky scénáře, a zároveň vyřadit odpovědi, které jsou zbytečně drahé, složité nebo neřeší klíčový cíl.

---

**Q3: Proč je důležité nepřehánět čas strávený na jedné otázce?**  
**A3:** Protože můžeš přijít o snadné body v jiných otázkách; lepší je dát rozumnou odpověď, označit ji pro revizi a pokračovat dál.

---

**Q4: Jak využít svoje vlastní poznámky (např. v Obsidianu) v přípravě?**  
**A4:** Pomocí vlastních Q&A a kvízů simulovat typy otázek, rychle si opakovat klíčové koncepty a identifikovat slabší místa, na která se pak více zaměříš.

---

**Q5: Jak můžeš během zkoušky minimalizovat chyby způsobené nepozorností?**  
**A5:** Číst otázky i možnosti pomalu, všímat si negací a slov jako „nejlevnější“, „nejjednodušší“, „nejrychlejší“, a před odesláním si v hlavě zkontrolovat, jestli odpověď skutečně splňuje přesně to, co je požadováno.

---

# Kvízové otázky (styl zkoušky)

1. **Jaký přístup je nejvhodnější k rozdělení času během DP‑700?**  
    a) Strávit většinu času na prvních pěti otázkách  
    b) Rozdělit čas rovnoměrně, rychle vyřešit jednoduché otázky a ponechat více času na komplexní scénáře  
    c) Odpovídat jen na otázky, které znáš úplně jistě  
    d) Vždy se vracet k první otázce po každé další  
    **Správná odpověď:** b)
    
2. **Co je typická chyba při čtení exam scénářů?**  
    a) Příliš pomalé čtení  
    b) Ignorování klíčových slov typu „cost‑effective“, „low maintenance“, „near real‑time“  
    c) Podtrhávání v duchu hlavních bodů  
    d) Rozdělení scénáře do jednodušších vět v hlavě  
    **Správná odpověď:** b)
    
3. **Jak bys měl přistupovat k otázkám „select TWO answers“?**  
    a) Vybrat dvě libovolné technologie, které znáš  
    b) Vybrat kombinaci, která technicky funguje, bez ohledu na požadavky  
    c) Vybrat dvojici, která společně nejlépe splňuje omezení a cíle uvedené ve scénáři  
    d) Vybrat vždy nejdražší řešení  
    **Správná odpověď:** c)
    
4. **Proč je důležité simulovat zkoušku při přípravě (např. časově omezený „mock“ test)?**  
    a) Jen kvůli zábavě  
    b) Aby sis zvykl na prostředí Pearson VUE  
    c) Aby ses naučil pracovat pod časovým tlakem a zjistil, kde se zasekáváš  
    d) Aby ses nemusel učit teorii  
    **Správná odpověď:** c)
    
5. **Jaký krok je vhodný těsně před reálnou zkouškou?**  
    a) Učit se do poslední minuty bez pauzy  
    b) Spustit si náročný projekt v práci  
    c) Dát si lehké opakování, odpočinout si a vyspat se, aby byla hlava v den zkoušky čerstvá  
    d) Zcela ignorovat učivo  
    **Správná odpověď:** c)
    
