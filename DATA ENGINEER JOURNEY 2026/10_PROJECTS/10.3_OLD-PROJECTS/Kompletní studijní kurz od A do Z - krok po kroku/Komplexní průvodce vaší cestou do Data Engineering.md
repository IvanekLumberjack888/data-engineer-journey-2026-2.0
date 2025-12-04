<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" style="height:64px;margin-right:32px"/>

# Komplexní průvodce vaší cestou do Data Engineeringu a Data Architektury

Máte velmi dobrý vhled do aktuální situace na trhu práce a vaše intuice o budoucnosti IT je správná. Pojďme si rozebrat komplexní strategii, jak se z bodu nula dostat do Data Engineeringu s cílem Data Architektury, a zároveň jak investovat svých 20 dolarů měsíčně nejefektivněji.

## Váš strategický vhled je správný

**HR a nábor se skutečně mění**. Podle World Economic Forum bude do roku 2030 potřeba **39% současných dovedností změnit nebo naučit nově**. Firmy už nehledají lidi, kteří "20 let pracovali na jedné pozici" – hledají lidi, kteří se **rychle učí, adaptují a prokazují upskilling a reskilling**.[^1][^2][^3][^4]

**Certifikace před vstupem do IT** je skvělá strategie. Studie LinkedIn ukazuje, že **94% zaměstnanců zůstává déle ve firmách, které investují do jejich rozvoje**. Pokud přijdete s certifikací a projekty v portfoliu, **vynikáte nad kandidáty bez nich**.[^5][^6][^1]

**Pozice Data Engineer nebude za 5 let stejná** – máte pravdu. Ale to je **pozitivní signál**, ne negativní. AI nebude data engineery nahrazovat, ale **změní jejich roli**:[^7][^8][^9]

- **Rutinní ETL úkoly** budou automatizované AI nástroji[^9]
- Data engineeři se posunou k **strategičtějším rolím**: data platform engineering, automation engineering, nebo business-facing roles[^9]
- **Poptávka po data engineerech roste 15-20% ročně** a v roce 2025 je přibližně 500,000 data engineerů celosvětově – **poptávka je masivní**[^10][^11]

**AI vytváří VÍCE práce pro data engineery**, ne méně. Každý AI model potřebuje čistá, strukturovaná data – což je přesně to, co data engineeři zajišťují.[^8][^7]

## Proč Data Engineering → Data Architecture je správná cesta proti nahrazení AI

**Data Architect** je role, která vyžaduje:

- **Strategické myšlení** a dlouhodobé plánování[^12][^13]
- **Komunikace s C-level** managementem[^12]
- **Business understanding** – pochopení, jak data podporují business cíle[^13][^14]
- **Design thinking** – navrhování komplexních systémů s ohledem na governance, bezpečnost a škálovatelnost[^15][^12]

Tyto schopnosti **AI nedokáže nahradit**, protože vyžadují:

1. **Hlubší kontext** business procesů a politiky organizace
2. **Kreativní řešení problémů** v ambivalentních situacích
3. **Lidské vztahy** a důvěru stakeholderů[^14][^13]

**Career path**: Junior Data Engineer (0-2 roky) → Mid-Level Data Engineer (2-5 let) → Senior Data Engineer (5-8 let) → Data Architect (10-14 let).[^16][^12]

Vaše strategie "začít jako Data Engineer a posunout se k Data Architecture" je **přesně správná cesta**, jak se vyhnout nahrazení AI.[^17][^12]

## Jak si rozvrhnout studijní plán (od bodu nula)

### Fáze 1: Základy (Měsíce 1-3)

**Cíl: Python + SQL mastery**

**Python**:[^6][^18][^5]

- Základní syntaxe, funkce, datové struktury
- Pandas pro data manipulaci
- NumPy pro numerické operace
- Doporučené kurzy:
    - DataCamp "Python for Data Engineers"[^19]
    - Codecademy "Data Engineer Career Path"[^19]

**SQL**:[^18][^5][^6]

- DDL (CREATE, ALTER, DROP)
- DML (SELECT, INSERT, UPDATE, DELETE)
- JOINs, agregace, subqueries
- Window functions
- Doporučené:
    - SQLZoo (zdarma)
    - Mode Analytics SQL Tutorial

**Projekt (konec Fáze 1)**:

- Vytvořte **ETL pipeline** z CSV do PostgreSQL[^20][^21]
- Přidejte základní data cleaning pomocí Pandas
- **Publikujte na GitHub** s README dokumentací[^22][^20]


### Fáze 2: Cloud Fundamentals (Měsíce 4-5)

**Cíl: Cloud certifikace**

**Která cloud platforma?**[^23][^24][^25]

Pro **data engineering** doporučuji **AWS nebo GCP**:

- **AWS** (nejširší adopce, nejvíce job postings)[^24][^23]
    - Certifikace: **AWS Certified Data Engineer - Associate** (\$150)[^26][^23]
    - Pokrývá: S3, Redshift, Glue, EMR, Kinesis, Lake Formation[^23][^26]
- **GCP** (silné v data/ML, AI-centric roles)[^24][^23]
    - Certifikace: **Google Cloud Professional Data Engineer** (\$200)[^27][^23]
    - Pokrývá: BigQuery, Dataflow, Dataproc, Pub/Sub[^27][^23]

**Azure** je dobrá, pokud cílíte na velké enterprise (finance, healthcare).[^25][^24]

**Moje doporučení pro vás**: Začněte **AWS**, protože má nejvíce job opportunities worldwide.[^25][^24]

**Jak se učit (ZDARMA před certifikací)**:

- AWS Free Tier – hands-on practice[^25]
- YouTube tutoriály (Stephane Maarek, freeCodeCamp)
- AWS Skill Builder (official training)[^26]

**Projekt (konec Fáze 2)**:

- **Postavte ETL pipeline na AWS**[^28][^21]
    - Data z public API (např. OpenWeatherMap) → S3 → Lambda transformace → Redshift
    - Publikujte na GitHub[^20][^22]


### Fáze 3: Workflow Orchestration (Měsíce 6-7)

**Cíl: Apache Airflow**

**Co se naučit**:[^29][^30]

- DAGs (Directed Acyclic Graphs)
- Operators, Sensors, Hooks
- Scheduling a monitoring
- Doporučené:
    - Marc Lamberti "Apache Airflow: The Complete Hands-On Course" (Udemy)
    - Astronomer Academy (zdarma)

**Projekt (konec Fáze 3)**:

- **End-to-End Data Pipeline s Airflow**[^28][^20]
    - Airflow orchestruje pipeline z API → S3 → transformation → BigQuery/Redshift
    - Přidejte **error handling** a **monitoring**
    - Dashboard v Looker/Tableau[^28]


### Fáze 4: Big Data \& Streaming (Měsíce 8-9)

**Cíl: Apache Spark + Kafka**

**Apache Spark (PySpark)**:[^29][^18]

- RDDs, DataFrames, Spark SQL
- Batch processing
- Doporučené:
    - DataCamp "Big Data with PySpark"
    - Pluralsight "Python for Data Engineers"[^31]

**Apache Kafka** (streaming):[^29]

- Producers, Consumers, Topics
- Real-time data processing
- Doporučené:
    - Confluent training (zdarma basics)

**Projekt (konec Fáze 4)**:

- **Real-time streaming pipeline**[^21][^28]
    - Kafka → PySpark Streaming → Redshift
    - Monitoring dashboard
    - Publikujte na GitHub[^22][^20]


### Fáze 5: Modern Data Stack (Měsíce 10-11)

**Cíl: dbt, Data Quality, Governance**

**dbt (data build tool)**:[^9][^29]

- SQL-based transformations
- Testing, documentation
- Version control pro analytics

**Data Quality frameworks**:[^29]

- Great Expectations nebo Soda

**Projekt (konec Fáze 5)**:

- **Production-grade data pipeline**[^20][^28]
    - Kombinace všech předchozích skills
    - Airflow + dbt + BigQuery/Snowflake
    - Data quality tests
    - Full documentation


### Fáze 6: Portfolio \& Job Search (Měsíc 12)

**Cíl: GitHub portfolio + CV + LinkedIn + networking**

**GitHub Portfolio**:[^22][^20]

- 3-5 komplexních projektů
- Každý s:
    - README s architekturou, tech stackem, business value
    - Code comments
    - Diagram architektury
- GitHub Pages pro portfolio website[^32]

**CV \& LinkedIn**:

- "Data Analyst with Python" (Engeto) jako základ
- Seznam projektů s business impact
- Skills: Python, SQL, AWS/GCP, Airflow, Spark, Kafka, dbt
- Certifikace (pokud máte)

**Networking**:

- Připojte se do Discord/Slack komunit (DataTalks.Club, dbt Community)
- LinkedIn posty o vašich projektech
- Komentujte pod posty data engineering influencers


## Investice 20 dolarů měsíčně: Co koupit?

Máte 3 hlavní možnosti pro investici:

### Možnost 1: Claude Pro (\$20/měsíc) [DOPORUČUJI PRO VÁS]

**Proč Claude pro learning Data Engineering?**[^33][^34]

**Výhody**:

- **Coding assistance**: Claude je vynikající v code review, debugging a vysvětlování kódu[^35][^36]
- **Learning Mode**: Pomocí sokratických otázek vás vede k řešení, ne jen dává odpověď[^37][^38]
- **Projects feature**: Můžete uploadovat dokumentaci AWS/GCP a Claude bude mít kontext při každém dotazu[^39][^40]
- **GitHub integrace**: Claude má nativní GitHub integration – můžete připojit vaše repo a Claude analyzuje váš kód[^41]
- **VS Code extension**: Můžete pracovat přímo v IDE[^42][^43]
- **Context window**: 200,000 tokenů (cca 150,000 slov) – můžete uploadovat celé tutorial/knihy[^44]

**Jak využít Claude Pro pro learning**:

1. **Study Projects**: Vytvořte Project "AWS Data Engineering" a nahrajte dokumentaci AWS služeb[^38]
2. **Code Review**: Připojte GitHub repo a nechte Claude reviewovat váš kód[^41]
3. **Learning Partner**: Ptejte se "Vysvětli mi Airflow DAGs jako bych měl 5 let" a Claude použije analogy[^33][^35]
4. **SQL + Python practice**: Claude generuje cvičení a vysvětluje řešení[^45][^46]

**Nevýhody**:

- Žádný real-time web search (na rozdíl od Perplexity)
- Knowledge cutoff (ale můžete to obejít přes upload dokumentace)


### Možnost 2: Perplexity Pro (\$20/měsíc)

**Proč Perplexity?**[^35][^33]

**Výhody**:

- **Research Mode**: Skvělé pro learning nových konceptů s citacemi a zdroji[^47][^33]
- **Real-time web search**: Vždy aktuální informace o nových technologiích[^33][^35]
- **Multiple models**: Můžete přepínat mezi GPT-5, Claude Sonnet 4, atd.[^33]

**Nevýhody**:

- Horší pro coding a complex projects než Claude[^36][^35]
- Žádná GitHub integrace[^33]
- Žádný VS Code extension[^33]

**Verdikt**: Pro **data engineering learning**, Claude > Perplexity.[^36][^35][^33]

### Možnost 3: Kombinace (střídání)

- **Měsíce 1-6**: Claude Pro (pro Python, SQL, coding practice)
- **Měsíce 7-12**: Certifikace (AWS/GCP exam)
- Po certifikaci: Zpět k Claude Pro nebo free tier


## Specifická doporučení pro vás (z Engeto Data Analytik)

**Co už máte**:

- Python basics ✅
- SQL fundamentals ✅
- Data analysis mindset ✅

**Co potřebujete dodat**:

- **Software engineering principles** (Git, testing, code quality)[^48][^18]
- **Data pipeline orchestration** (Airflow)[^18][^29]
- **Cloud platforms** (AWS/GCP)[^5][^18]
- **Big data tools** (Spark)[^18][^29]

**Transition roadmap "Data Analyst → Data Engineer"**:[^49]

1. **Upskill programming** – více Python, méně Excel
2. **Shift mindset** – od "analyzing data" k "building systems that enable analysis"[^49]
3. **Build pipelines** – ne jen analýzy, ale celé ETL workflows[^49]
4. **Learn infrastructure** – cloud, containers, orchestration[^49]

**Vaše výhoda**: Rozumíte **business value of data** (z Engeto kurzu) – to je **huge advantage** pro přechod k Data Architecture později.[^13][^12]

## Broad Perspective: Junioři v IT 2025+

Máte pravdu – **junioři budou muset mít širší přehled a hlubší základy**.[^48][^5]

**Co firmy hledají u juniorů v 2025**:[^5][^48]

1. **Strong fundamentals** – Python, SQL, cloud (ne jen "udělal jsem kurz")[^48][^5]
2. **Tenacity \& attitude** – schopnost "crack their head against a wall and learn"[^48]
3. **Real projects** – ne jen "Hello World", ale **production-like pipelines**[^5][^48]
4. **Willingness to learn** – adaptabilita na nové technologie[^5][^48]
5. **Soft skills** – komunikace, problem-solving[^18][^5]

**Jak se lišit od ostatních juniorů**:[^20][^5]

- **GitHub portfolio** s 3-5 komplexními projekty[^22][^20]
- **Certifikace** (AWS/GCP)[^23][^27]
- **Blog posty** o vašich projektech (LinkedIn, Medium)[^20]
- **Contributions** do open-source (např. dbt, Airflow)[^22]


## Konkrétní akční plán pro vás

### Měsíc 1 (Listopad 2025)

- [ ] Investujte **Claude Pro** (\$20)
- [ ] Vytvořte **GitHub účet** a profile
- [ ] Refresh **Python** (4 hodiny/týden):
    - Pandas, NumPy
    - Claude Project "Python for Data Engineering"
- [ ] **SQL practice** (3 hodiny/týden):
    - SQLZoo, HackerRank SQL
    - Claude jako code review partner


### Měsíc 2 (Prosinec 2025)

- [ ] **První projekt**: ETL CSV → PostgreSQL[^21]
    - Publikujte na GitHub s README[^20]
    - LinkedIn post o projektu
- [ ] Začněte **AWS Free Tier**[^25]
    - S3, Lambda, RDS basics


### Měsíc 3 (Leden 2026)

- [ ] **Druhý projekt**: AWS ETL pipeline[^28]
    - API → S3 → Lambda → Redshift
    - Claude jako coding partner
- [ ] Připojte se do **DataTalks.Club** (Slack community)


### Měsíc 4-5 (Únor-Březen 2026)

- [ ] **AWS Certified Data Engineer - Associate** study[^26]
    - Pause Claude Pro, investujte do practice exams (\$150 exam fee)
    - AWS Skill Builder (zdarma)[^26]
- [ ] **Třetí projekt**: Airflow orchestration[^21]


### Měsíc 6 (Duben 2026)

- [ ] **AWS exam**[^26]
- [ ] Zpět na Claude Pro
- [ ] **Čtvrtý projekt**: Spark + Kafka[^21]


### Měsíc 7-12 (Květen-Říjen 2026)

- [ ] **Modern data stack** (dbt, Great Expectations)[^29]
- [ ] **Pátý projekt**: End-to-End production pipeline[^28][^20]
- [ ] **Portfolio website** (GitHub Pages)[^32]
- [ ] **Job applications** – cílte junior Data Engineer pozice


## Závěrečné myšlenky

Vaše investice \$20/měsíc **do sebe** je nejlepší investice, kterou můžete udělat. V IT pozici to skutečně dostanete zpět na penězích rychleji než v Hedin Automotive.[^10][^5]

**Entry-level data engineer salary**: \$80,000-\$100,000 (USA), v ČR cca 60,000-80,000 Kč/měsíc pro juniory.[^16]

**Mid-level (po 2-5 letech)**: \$110,000-\$140,000 (USA), v ČR 80,000-120,000 Kč/měsíc.[^16]

**Senior/Architect (5-10+ let)**: \$140,000-\$200,000+ (USA), v ČR 120,000-200,000+ Kč/měsíc.[^10][^16]

**Vaše cesta je realistická a achievable**. S vaším Engeto kurzem máte už základ. Teď potřebujete:

1. **Claude Pro** jako learning partner (nebo Perplexity, ale Claude > pro coding)[^35][^33]
2. **Systematický study plan** (12 měsíců outlined výše)
3. **GitHub portfolio** s real projects[^22][^20]
4. **Cloud certifikace** (AWS/GCP)[^27][^23]
5. **Networking** v komunitách[^49]

**Do roka můžete být připraveni na junior Data Engineer pozice**. Za 5-10 let můžete být Data Architect s platem, který transformuje váš život.[^6][^17][^12][^18][^5]

Držím vám palce! Vaše myšlení je **přesně správné** a vaše strategie je **solid**. Jen do toho! 💪
<span style="display:none">[^50][^51][^52][^53][^54][^55][^56][^57][^58][^59][^60][^61][^62][^63][^64][^65][^66][^67][^68][^69][^70][^71]</span>

<div align="center">⁂</div>

[^1]: https://hortoninternational.com/upskilling-in-2025/

[^2]: https://www.davron.net/upskilling-reskilling-in-2025-navigating-the-future-of-work-in-a-shifting-job-market/

[^3]: https://wawiwa-tech.com/blog/reskilling-and-upskilling-for-the-fastest-growing-tech-jobs/

[^4]: https://productschool.com/blog/leadership/upskilling-and-reskilling

[^5]: https://www.refontelearning.com/blog/entry-level-data-engineering-jobs-in-2025-skills-certifications-you-need

[^6]: https://www.datacamp.com/blog/how-to-become-a-data-engineer

[^7]: https://www.montecarlodata.com/blog-will-genai-replace-data-engineers

[^8]: https://www.gambilldataengineering.com/data-engineering/how-ai-and-data-engineering-are-shaping-the-future-of-work-in-2025

[^9]: https://www.getdbt.com/blog/how-ai-will-disrupt-data-engineering

[^10]: https://www.interviewquery.com/p/data-engineer-career-path

[^11]: https://www.linkedin.com/posts/eczachly_ai-is-1000-not-killing-data-engineering-activity-7342249325520920577-H_Z-

[^12]: https://himalayas.app/career-guides/enterprise-data-architect

[^13]: https://www.coursera.org/articles/data-architect

[^14]: https://www.ironhack.com/us/blog/how-to-become-a-data-architect-a-career-guide

[^15]: https://potomac.edu/data-architect-vs-data-engineer/

[^16]: https://bootcamp.ccslearningacademy.com/data-engineer-career-path/

[^17]: https://www.comptia.org/en-us/blog/your-next-move-data-architect/

[^18]: https://www.datacamp.com/blog/how-to-learn-data-engineering

[^19]: https://www.codecademy.com/learn/paths/data-engineer

[^20]: https://dataengineeracademy.com/module/how-to-use-github-to-showcase-your-data-engineering-skills/

[^21]: https://www.datacamp.com/blog/data-engineering-projects

[^22]: https://www.kdnuggets.com/10-github-repositories-to-master-data-engineering

[^23]: https://pingax.com/certifications-comparison-aws-google-azure/

[^24]: https://dev.to/cyberry_technologies/azure-aws-or-gcp-are-you-wasting-time-on-the-wrong-cloud-certification-in-2025-1i0b

[^25]: https://flashgenius.net/blog-article/aws-vs-azure-vs-google-cloud-certifications-which-cloud-path-should-you-choose-in-2025

[^26]: https://aws.amazon.com/certification/certified-data-engineer-associate/

[^27]: https://dataengineeracademy.com/module/the-most-valuable-data-engineering-certifications-in-2025/

[^28]: https://www.projectpro.io/article/real-world-data-engineering-projects-/472

[^29]: https://www.reddit.com/r/dataengineering/comments/1ms7auu/what_would_be_the_ideal_beginner_learning_path/

[^30]: https://www.linkedin.com/learning/paths/master-data-engineering

[^31]: https://www.pluralsight.com/paths/python-for-data-engineers

[^32]: https://www.youtube.com/watch?v=KIqteLTVLy8

[^33]: https://www.leanware.co/insights/claude-vs-perplexity

[^34]: https://screenapp.io/blog/claude-ai-pricing

[^35]: https://techpoint.africa/guide/perplexity-vs-claude-test/

[^36]: https://learn.g2.com/perplexity-vs-claude

[^37]: https://www.anthropic.com/news/introducing-claude-for-education

[^38]: https://learning.northeastern.edu/ai-student-guides-using-claude-learning-mode-to-study/

[^39]: https://www.anthropic.com/news/projects

[^40]: https://support.claude.com/en/articles/9517075-what-are-projects

[^41]: https://support.claude.com/en/articles/10167454-using-the-github-integration

[^42]: https://docs.claude.com/en/docs/claude-code/ide-integrations

[^43]: https://www.claudelog.com/faqs/how-to-use-claude-code-with-vs-code/

[^44]: https://www.datastudios.org/post/claude-context-window-token-limits-memory-policy-and-2025-rules

[^45]: https://pub.towardsai.net/claude-code-as-a-data-analyst-from-zero-to-first-report-0aa55539a19f

[^46]: https://aws.amazon.com/blogs/machine-learning/build-your-gen-ai-based-text-to-sql-application-using-rag-powered-by-amazon-bedrock-claude-3-sonnet-and-amazon-titan-for-embedding/

[^47]: https://support.claude.com/en/articles/11088861-using-research-on-claude

[^48]: https://www.linkedin.com/pulse/how-successful-junior-data-engineer-connor-baker-

[^49]: https://dataengineeracademy.com/module/from-data-analyst-to-data-engineer-a-roadmap-for-career-transition/

[^50]: https://www.refontelearning.com/blog/is-data-engineering-future-proof

[^51]: https://www.ascend.io/blog/ais-impact-on-data-engineering-careers

[^52]: https://www.reddit.com/r/dataengineering/comments/1jnisk7/what_is_expected_of_me_as_a_junior_data_engineer/

[^53]: https://www.reddit.com/r/dataengineering/comments/1g834dy/the_ai_and_its_impact_on_data_engineers_career/

[^54]: https://learn.snowflake.com/en/data-engineer-python

[^55]: https://365datascience.com/career-advice/career-guides/how-to-become-a-data-engineer/

[^56]: https://www.superhuman.ai/c/perplexity-vs-claude-7-features-compared-2025

[^57]: https://www.whizlabs.com/blog/top-5-cloud-certifications-to-earn-in-2025/

[^58]: https://www.weforum.org/publications/the-future-of-jobs-report-2025/digest/

[^59]: https://www.reddit.com/r/perplexity_ai/comments/1e664fr/claude_on_perplexity_or_claude_directly/

[^60]: https://reports.weforum.org/docs/WEF_Future_of_Jobs_Report_2025.pdf

[^61]: https://www.clickforest.com/en/blog/ai-tools-comparison

[^62]: https://www.jeeviacademy.com/which-cloud-certification-should-i-start-with-aws-azure-or-google-cloud/

[^63]: https://www.mckinsey.com/capabilities/people-and-organizational-performance/our-insights/we-are-all-techies-now-digital-skill-building-for-the-future

[^64]: https://www.reddit.com/r/dataengineering/comments/14bvy46/career_change_to_de_from_a_nondatacoding_career/

[^65]: https://career.softserveinc.com/en-us/stories/big-data-career-path

[^66]: https://www.institutedata.com/blog/4-tips-to-switch-from-a-non-it-background-to-data-science/

[^67]: https://github.com/cybergeekgyan/Data-Engineering-Portfolio

[^68]: https://www.nataindata.com/blog/how-to-become-a-data-engineer-2024-2/

[^69]: https://www.upgrad.com/blog/data-architect-skills/

[^70]: https://github.com/vedanthv/data-engineering-portfolio

[^71]: https://www.youtube.com/watch?v=COXzAb-KPAI

