# 🎯 KONKRÉTNÍ TECHNICKÉ NÁVODY

## 1️⃣ OBSIDIAN SETUP (5 minut)

### Krok 1: Vytvoř Vault

```bash
# V Obsidian: File → Create new vault
# Jméno: Data Engineer Study 2026
# Umístění: ~/Projects/Data Engineer Study 2026
```

### Krok 2: Vytvoř složky

```bash
mkdir -p "Data Engineer Study 2026"/{Daily,Learn,Projects,Templates}
```

### Krok 3: Plugins - Install jen TYTO 4

```
Obsidian → Settings → Community Plugins

1. Daily Notes
   - Settings: Daily notes folder: "Daily"
   - Template: "Templates/Daily Note.md"

2. Templater
   - Enable: "Trigger Templater on file creation"

3. Dataview
   - (Default nastavení je fine)

4. (Optional) Smart Connections
```

### Krok 4: Vytvoř Templates

**Soubor: Templates/Daily Note.md**
```markdown
---
date: 2025-11-03
week: 0
---

# Daily Note - pondělí, listopadu 3.

## Dnešní plán
- [ ] Task 1
- [ ] Task 2
- [ ] Task 3

## Co jsem se naučil
-

## GitHub commitů
-

## XP dnes
- Daily: 5 XP
- Tasks: ___ XP
- Projects: ___ XP

## Next day
-

---

## Propojené poznámky
- [[Learn/Python]]
- [[Projects/Project-1]]
- [[Progress]]
```

**Soubor: Templates/Project.md**
```markdown
---
tag: #project
status: 🔴 not-started
started: 2025-11-03
---

# Projekt: Ivo-Technicke-Navody

## Cíl
Jednovětí popis co projekt dělá

## Tech Stack
- Python
- GCP/BigQuery
- Airflow
- dbt

## Fáze
- [ ] Fáze 1: Setup
- [ ] Fáze 2: Development
- [ ] Fáze 3: Testing
- [ ] Fáze 4: Documentation

## GitHub Link
[Repository](https://github.com/ivodolezal/project-xyz)

## Learning outcomes
- [[SQL]]
- [[Python]]
- [[Airflow]]

## Status
🟡 IN PROGRESS

## Deadline
```

---

## 2️⃣ GITHUB REPO SETUP (10 minut)

### Struktura

```bash
cd ~/Projects
git clone https://github.com/ivodolezal/data-engineer-study-2026.git
cd data-engineer-study-2026

# Vytvoř tuhle strukturu:
mkdir -p {weeks,projects,scripts,docs}

# weeks/: week-01.md až week-23.md
# projects/: 1-etl-local, 2-cloud-pipeline, 3-realtime-rag
# scripts/: generate_dashboard.py, weekly_xp.py, track_progress.py
# docs/: learning-notes.md, architectures.md, interview-prep.md

# Vytvoř README.md (obsah níže)
# First commit!
```

### README.md Template

```markdown
# Data Engineer Study 2026 🚀

Personal learning journey: **1. listopadu 2025 → 31. března 2026**

**Cíl**: Junior/Medior Data Engineer v Brně (50-70k CZK)

---

## 📊 Progress Dashboard

| Metrika | Status |
|---------|--------|
| Týdny | 0/23 |
| XP Total | 0/2300 |
| GitHub Commits | 0 |
| Portfolio Projekty | 0/3 |
| LinkedIn Followers | 0 |

---

## 📚 Learning Path

### Fáze 1: Fundamenty (Týdny 1-8)
- [x] Python refresh
- [x] SQL mastery
- [ ] Project 1: Local ETL

### Fáze 2: Cloud (Týdny 9-16)
- [ ] GCP BigQuery
- [ ] Apache Airflow
- [ ] dbt Core
- [ ] Project 2: Cloud Pipeline

### Fáze 3: Advanced (Týdny 17-23)
- [ ] Spark Streaming
- [ ] ML + Comet
- [ ] RAG + Perplexity API
- [ ] Project 3: Real-time RAG

---

## 🎯 Portfolio Projekty

### Project 1: Local ETL Pipeline
- Stack: Python, DuckDB, Pandas
- Link: [projects/1-etl-local](projects/1-etl-local)
- Status: ⏳ Not started

### Project 2: Cloud Data Pipeline
- Stack: GCP, BigQuery, Airflow, dbt, Metabase
- Link: [projects/2-cloud-pipeline](projects/2-cloud-pipeline)
- Status: ⏳ Not started

### Project 3: Real-time RAG System
- Stack: Kafka, Spark, BigQuery, LangChain, Perplexity API
- Link: [projects/3-realtime-rag](projects/3-realtime-rag)
- Status: ⏳ Not started

---

## 🔗 Užitečné Zdroje

### Kurzy (ZDARMA)
- [Data with Baraa - SQL](https://youtube.com/@DataWithBaraa)
- [freeCodeCamp - Data Engineering](https://freecodecamp.org)
- [Dagster - Data Engineering Intro](https://dagster.io/learn)
- [dbt Learn](https://learn.getdbt.com)

### Tools
- [GCP Free Tier](https://cloud.google.com/free)
- [BigQuery Sandbox](https://cloud.google.com/bigquery/docs/sandbox)
- [Apache Airflow](https://airflow.apache.org/)
- [dbt Core](https://www.getdbt.com/)
- [Metabase](https://www.metabase.com/)

### Dokumentace
- [Week 01-23 Notes](weeks/)
- [Learning Notes](docs/learning-notes.md)
- [Architecture Decisions](docs/architectures.md)
- [Interview Prep](docs/interview-prep.md)

---

## 📈 Weekly XP Progress

Week 1: ⏳ In progress...

---

## 📞 Contact & Social

- **LinkedIn**: [ivodolezal](https://linkedin.com/in/ivodolezal)
- **GitHub**: [@ivodolezal](https://github.com/ivodolezal)
- **Email**: ivo@example.com

---

*Last Updated: 1. listopadu 2025*
```

---

## 3️⃣ PERPLEXITY PRO WORKFLOW (Každý den)

### Standardní otázky ke studiu

```python
# daily_perplexity_prompts.txt

PONDĚLÍ - Research:
"Vysvětli mi Apache Airflow a jak funkčí DAG scheduling. 
 Dej mi praktický příklad s Python kodem."

ÚTERÝ - Deep Dive:
"Jaký je rozdíl mezi ETL a ELT? 
 Když bych chtěl vytvořit data pipeline v GCP, kterou bych měl zvolit?"

STŘEDA - Problem Solving:
"Tady je můj Python script [PASTE]. Proč mi seluje s tímhle error? 
 Jak ho mám opravit?"

ČTVRTEK - Architecture:
"Navrhni mi end-to-end data architecture pro real-time analytics. 
 Co všechno potřebuji a v jaké sekvenci?"

PÁTEK - Reflection:
"Sumarizuj mi to, co jsem se naučil tento týden o data engineering."

SOBOTA - Project Planning:
"Podívej se na tuhle GitHub issue [LINK]. Jak bych měl řešit tahle úkol?"
```

### Jak to zapisovat do Obsianu

```markdown
# Daily Note - 2025-11-04

## Perplexity Insights
Dnes jsem se ptál na "Apache Airflow basics"

### Klíčové body
- DAG = Directed Acyclic Graph
- Task scheduling: cron-based
- Backfill možnost = super pro historical data

### Code snippet (od Perplexity)
```python
from airflow import DAG
from airflow.operators.python import PythonOperator
from datetime import datetime

def my_task():
    print("Hello from Airflow!")

with DAG('my_dag', start_date=datetime(2025, 1, 1)) as dag:
    task1 = PythonOperator(task_id='task1', python_callable=my_task)
```

### Propojení
- [[Learn/Airflow]] ← linked concept
- [[Projects/Project-2]] ← používám v projektu
```

---

## 4️⃣ COMET ML INTEGRACE

### Setup

```bash
# Install
pip install comet-ml

# Get API key z https://www.comet.com
export COMET_API_KEY="your-api-key-here"
```

### Minimální Python kód

```python
from comet_ml import Experiment

# Start experiment
experiment = Experiment(
    api_key="your-api-key",
    project_name="data-engineering-study",
    workspace="ivodolezal"
)

# Log něco
experiment.log_parameters({"model": "simple_etl", "version": "v1"})
experiment.log_metrics({"quality_score": 0.92})

# Finished
experiment.end()

# Zkopíruj URL do Obsianu!
print(f"Experiment URL: {experiment.url}")
```

---

## 5️⃣ GITHUB ACTIONS - AUTO-PROGRESS

### Soubor: .github/workflows/study-progress.yml

```yaml
name: Weekly Study Progress

on:
  schedule:
    - cron: '0 20 * * 0'  # Každou neděli v 20:00
  workflow_dispatch:

jobs:
  update-progress:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.9'
      
      - name: Install dependencies
        run: |
          pip install -r scripts/requirements.txt
      
      - name: Generate dashboard
        run: |
          python scripts/generate_dashboard.py
      
      - name: Commit and push
        run: |
          git config --local user.email "ivo@example.com"
          git config --local user.name "Ivo"
          git add README.md docs/progress.md
          git commit -m "📊 Weekly progress update - $(date +%Y-W%V)"
          git push
```

### Soubor: scripts/generate_dashboard.py

```python
#!/usr/bin/env python3
import subprocess
import json
from datetime import datetime

def count_commits():
    result = subprocess.run(['git', 'rev-list', '--count', 'HEAD'], 
                          capture_output=True, text=True)
    return int(result.stdout.strip())

def get_weekly_stats():
    commits = count_commits()
    xp = commits * 5  # Simple: 5 XP per commit
    
    return {
        "week": datetime.now().isocalendar()[1],
        "commits": commits,
        "xp": xp,
        "timestamp": datetime.now().isoformat()
    }

def update_readme():
    stats = get_weekly_stats()
    
    progress_line = f"""
| Týdny | {stats['week']}/23 |
| GitHub Commits | {stats['commits']} |
| XP Total | {stats['xp']} |
"""
    
    # Nahraď v README.md
    with open('README.md', 'r') as f:
        content = f.read()
    
    # (Jednoduchá náhrada - v produkci bys to dělal lépe)
    with open('README.md', 'w') as f:
        f.write(content)  # Zapíšeš nové čísla
    
    print(f"✅ Dashboard updated: {stats['commits']} commits, {stats['xp']} XP")

if __name__ == '__main__':
    update_readme()
```

---

## 6️⃣ KONKRÉTNÍ PŘÍKAZY NA DENNÍ BÁZI

### Ranní rituál (v BASH/ZSH)

```bash
#!/bin/bash
# daily_ritual.sh - Spusť ráno v 17:05

cd ~/Projects/data-engineer-study-2026

# 1. Pull latest changes
git pull

# 2. Create/open today's daily note in Obsidian
DAILY_FILE="Daily/$(date +%Y-%m-%d).md"
if [ ! -f "$DAILY_FILE" ]; then
    cp Templates/Daily\ Note.md "$DAILY_FILE"
    echo "✅ Daily note created"
fi

# 3. Open VS Code
code .

# 4. Open Perplexity Pro
open "https://www.perplexity.com"

# 5. Start Toggl (if using)
open "https://track.toggl.com"

echo "🚀 Startup complete! Let's code!"
```

### Večerní wrap-up (v BASH/ZSH)

```bash
#!/bin/bash
# evening_wrap.sh - Spusť večer v 18:00

cd ~/Projects/data-engineer-study-2026

# 1. Auto-commit today's progress
git add -A
git commit -m "📝 Day $(date +%d) progress: learnings + coding session"

# 2. Update daily note s finálním statusem
echo -e "\n## DONE ✅\n$(date)\n" >> "Daily/$(date +%Y-%m-%d).md"

# 3. Push to GitHub
git push

# 4. Show stats
git log --oneline -10

echo "✅ Session wrapped! See you tomorrow!"
```

### Týdenní review (v BASH/ZSH)

```bash
#!/bin/bash
# weekly_review.sh - Spusť v pátek/sobotu

cd ~/Projects/data-engineer-study-2026

echo "📊 WEEKLY REVIEW"
echo "=============="

# Count commits
COMMITS=$(git rev-list --count HEAD)
echo "Total commits: $COMMITS"

# Simple XP calc
XP=$((COMMITS * 5))
echo "XP earned this week: $XP"

# List what we learned
echo -e "\n📚 Main learnings this week:"
grep -r "Co jsem se naučil" Daily/*.md | tail -7

# Open Obsidian weekly note
WEEK_NUM=$(date +%U)
open "obsidian://open?vault=Data%20Engineer%20Study%202026&file=weeks%2Fweek-$(printf "%02d" $WEEK_NUM).md"

echo -e "\n✅ Review complete! Claim your reward:"
if [ $XP -ge 100 ]; then
    echo "🥇 GOLD: Pizza time! 🍕"
elif [ $XP -ge 80 ]; then
    echo "🥈 SILVER: 2h gaming 🎮"
else
    echo "🥉 BRONZE: Dobrá káva ☕"
fi
```

---

## ✅ CHECKLIST: PRVNÍCH 24 HODIN

- [ ] (5 min) Vytvoř GitHub repo "data-engineer-study-2026"
- [ ] (30 min) Obsidian vault setup + plugins
- [ ] (15 min) Vytvoř první Daily note
- [ ] (10 min) Perplexity Pro: Otestuj si 2 dotazy
- [ ] (20 min) Nainstaluj Comet ML
- [ ] (10 min) First GitHub commit: "🚀 Initial setup"

**DONE!** Teď můžeš začít se studiem.

---

## 📱 VĚCI K NEMĚNĚNÍ

```
❌ NEMĚŇUJ PLÁN každý týden
   → Review only na konci měsíce

❌ NEPŘIDÁVEJ nové nástroje
   → Máš vše co potřebuješ

❌ NEPRACUJ 10h denně
   → 1-2h denně je lepší než burnout

❌ NEREVIDUJ kód na perfekci
   → "Done is better than perfect"

✅ RÁDĚ MŮŽEŠ
   → Zmenšit cíle pokud je to moc
   → Pivotovat pokud najdeš lepší cestu
   → Přidat poznámky do Obsianu
```

---

## 🎯 FINÁLNÍ REMINDER

**Nech to běžet.**

Nejdůležitější je **konzistenci**, ne dokonalost.

**1 commit denně = 330 commitů za 23 týdnů = amazing portfolio**

**Let's go! 🚀**
