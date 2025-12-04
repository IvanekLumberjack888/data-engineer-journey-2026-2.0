# 📚 DATA ENGINEER JOURNEY 2026 - KOMPLETNÍ PLÁN (FULL EDITION)

**VŠECHNO CO POTŘEBUJETE - OD ZAČÁTKU DO KONCE!**

---

## 🎯 OBSAH TOHOTO DOKUMENTU

- ✅ 20 modulů (001-020) - detailně rozepsáno!
- ✅ Všechny šablony (Daily, Learn, Project, Weekly Review)
- ✅ 23-týdenní harmonogram
- ✅ XP gamifikace + levely
- ✅ Checklists
- ✅ Claude AI strategie + tarify
- ✅ Setup návody

**TOTO JE VAŠE BIBLE PRO PŘÍŠTÍCH 23 TÝDNŮ!**

---

## 📅 MĚSÍC 1: LISTOPAD 2025 (FUNDAMENTY)

### MODUL 001: GIT & GITHUB BASICS

**Doba:** 90 minut  
**Obtížnost:** ⭐ Nula  
**Prerekvizity:** Nic  
**Výsledek:** GitHub repo + první commit

#### 🎯 Proč to potřebuješ?

Git = Nejdůležitější nástroj pro programátora! Firmy: "Pošli GitHub" → vidí VŠECHNO!

**Bez Gitu:**
```
script_v1.py
script_v2_final.py
script_v3_final_FINAL.py  ← Chaos!
```

**S Gitem:**
```
script.py (jedna verze, ale všechna historie v Gitu)
```

#### 📚 Teorie (30 minut)

**Co je Git?**
- Local version control (na tvém PC)
- Ukládá HISTORII všech změn
- Umožňuje rollback (vrátit se)
- Standard v IT

**Co je GitHub?**
- Cloud úložiště pro Git repo
- Portfolio pro programmátory
- Recruiteři tam hledají lidi
- Open source komunita

**Workflow:**
```
Local changes → git add → git commit → git push → GitHub
```

**SSH klíče:**
- Public key = zámek (dáš na GitHub)
- Private key = klíč (máš na PC)
- Bezpečný přístup

#### 💻 Praktika (60 minut)

##### Instalace Git

**Mac:**
```bash
brew install git
```

**Windows:**
1. Stáhni: https://git-scm.com/download/win
2. Next, Next, Next (defaultní settings OK)

**Linux:**
```bash
sudo apt-get install git
```

##### Konfigurace

```bash
# Řekni Gitu kdo jsi
git config --global user.name "Tvoje Jméno"
git config --global user.email "tvuj@email.com"

# Ověř:
git config --global user.name
git config --global user.email
```

##### GitHub Účet

1. Jdi na https://github.com
2. Sign up (zdarma!)
3. Email: tvůj email
4. Username: `tvojeusername` (bude vidět recruiterům!)

##### SSH Klíče Setup

```bash
# Vytvoř klíč (Enter 3x)
ssh-keygen -t ed25519 -C "tvuj@email.com"

# Zobraz public klíč
cat ~/.ssh/id_ed25519.pub | pbcopy  # Mac
# Nebo Windows: Get-Content ~/.ssh/id_ed25519.pub | Set-Clipboard

# Jdi na GitHub:
# Settings (⚙️ nahoře vpravo)
# → SSH and GPG keys
# → New SSH key
# → Paste klíč
# → Add SSH key

# Test:
ssh -T git@github.com
# Output: "Hi username! You've successfully authenticated..."
```

##### Tvůj První Repo

```bash
# Vytvoř složku
mkdir data-engineer-study-2026
cd data-engineer-study-2026

# Inicializuj Git
git init

# Vytvoř README
echo "# Data Engineer Study 2026" > README.md

# Přidej do stagia
git add README.md

# Commitni (💾 uložení s komentářem)
git commit -m "🚀 Initial commit"

# Ověř:
git log
# Vidíš: commit hash, author, message
```

##### Push na GitHub

```bash
# Jdi na GitHub → New repository
# Název: data-engineer-study-2026
# Public (recruiteři vidí!)
# Nezaškrtávej "Initialize with README" (máš už!

# V terminálu:
git branch -M main  # Přejmenuj master → main
git remote add origin git@github.com:username/data-engineer-study-2026.git
git push -u origin main

# Ověř:
# Jdi na GitHub.com/username/data-engineer-study-2026
# Měl bys vidět README.md!
```

#### ✅ Cvičení

```bash
# Cvičení 1: Vytvoř nový soubor a commitni
echo "# Hello World" > hello.md
git add hello.md
git commit -m "📝 Add hello world"
git push

# Cvičení 2: Modifikuj soubor
echo "## Welcome" >> hello.md
git add hello.md
git commit -m "📝 Update hello"
git push

# Cvičení 3: Podívej se na historii
git log --oneline
# Vidíš 3 commity!
```

#### 📋 Checklist

- [x] Git je nainstalovaný (`git --version`)
- [x] GitHub účet vytvořen
- [x] SSH klíče nastavené (test prošel)
- [x] Local repo vytvořen
- [x] GitHub repo vytvořen
- [x] Push na GitHub funguje
- [x] Mám 3+ commity

---

### MODUL 002: OBSIDIAN SETUP

**Doba:** 60 minut  
**Obtížnost:** ⭐ Lehká  
**Prerekvizity:** 001  
**Výsledek:** Obsidian vault + Daily Notes + Templates

#### 🎯 Proč to potřebuješ?

Obsidian = **Tvůj druhý mozek** pro studium!

**Features:**
- ✅ Offline (bez internetu!)
- ✅ Markdown (.md soubory)
- ✅ Propojování poznámek ([[Reference]])
- ✅ GitHub-friendly (Git sync)
- ✅ Plugins (Daily Notes, Templates, Search)
- ✅ **ZDARMA**

#### 📚 Teorie (10 minut)

**Co je Obsidian?**
- Note-taking app (jako OneNote ale lepší)
- Ukládá jako .md soubory (plain text)
- Vše lze verzovat v Gitu
- Graph View vidí propojení

**P.A.R.A. struktura:**
- **P**rojects (aktivní věci)
- **A**reas (dlouhodobé oblasti)
- **R**esources (reference)
- **A**rchive (staré věci)

#### 💻 Praktika (50 minut)

##### Instalace

1. Stáhni: https://obsidian.md
2. Nainstaluj
3. Otevři

##### Vytvoření Vault

```
Obsidian → Create new vault
Jméno: Data Engineer Study 2026
Cesta: H:\Můj disk\DATA ENGINEER JOURNEY\vault
```

##### P.A.R.A. Struktura

```bash
# V terminálu nebo Obsidianu:

vault/
├── 00_FEED/
│   └── Index.md (Přehled všeho)
│
├── 10_PROJEKTY/
│   └── 10.1_OSOBNÍ/
│       └── Data Engineer 2026/
│           ├── 001-Git-GitHub-Basics.md
│           ├── 002-Obsidian-Setup.md
│           └── ...ostatní moduly
│
├── 01_DAILY_PAGES/
│   ├── 2025-11-02.md
│   ├── 2025-11-03.md
│   └── ...161 daily notes!
│
└── 30_ZDROJE/
    ├── 30.1_ODKAZY/
    │   └── Webové-zdroje.md
    │
    ├── 30.2_INTEGRATIONS/
    │   ├── GitHub-setup.md
    │   └── Claude-Perplexity-strategy.md
    │
    └── 30.3_TEMPLATES/
        ├── Daily-Note-Template.md
        ├── Learn-Note-Template.md
        ├── Project-Note-Template.md
        └── Weekly-Review-Template.md
```

##### Plugins

**Instalace:**
1. Settings (⚙️) → Community plugins
2. Toggle "Community plugins"
3. Browse
4. Hledej plugin
5. Install → Enable

**Plugin 1: Daily Notes**
```
Browse → "Daily Notes" → Install + Enable

Settings:
- Date format: YYYY-MM-DD
- New file location: 01_DAILY_PAGES
- Template file location: 30_ZDROJE/30.3_TEMPLATES/Daily-Note-Template
- Open daily note: ON
- Auto backup: ON
```

**Plugin 2: Templater**
```
Browse → "Templater" → Install + Enable

Settings:
- Template folder: 30_ZDROJE/30.3_TEMPLATES
- Trigger Templater on new file: ON
- Enable folder templates: ON
  - Folder: 01_DAILY_PAGES
  - Template: Daily-Note-Template
```

**Plugin 3: Graph View (Built-in)**
- Levý panel → Graph View icon
- Vidíš všechny propojené poznámky!

##### Denní Workflow

```
17:05 - Otevři Obsidian
17:05 - Cmd+Shift+D (Mac) nebo Ctrl+Shift+D (Windows)
        → Daily note se auto-vytvoří
17:10 - Vyplň plán na dneska
17:15 - Studuj...
18:00 - Vyplň "Dneška jsem zvládnul"
18:05 - Save (Cmd+S)
18:05 - Git commit + push
```

#### ✅ Cvičení

```
Cvičení 1: Vytvoř první Daily note
- Cmd+Shift+D
- Vyplň template

Cvičení 2: Vytvoř Learn note
- Ručně: 30_ZDROJE/ → New file
- Název: "Co-je-Git.md"
- Vyplň template

Cvičení 3: Propoj poznámky
- V Daily note: "Dneska jsem se učil [[Co-je-Git]]"
- Klikni na odkaz
- Vidíš propojení!
```

#### 📋 Checklist

- [x] Obsidian nainstalovaný
- [x] Vault vytvořen
- [x] P.A.R.A. složky vytvořené
- [x] Daily Notes plugin aktivní
- [x] Templater plugin aktivní
- [x] Templates vytvořené
- [x] Obsidian je propojen s Git repo
- [x] První Daily note funguje

---

### MODUL 003: PYTHON SETUP

**Doba:** 45 minut  
**Obtížnost:** ⭐ Nula  
**Prerekvizity:** 002  
**Výsledek:** Python 3.13 + venv + requirements.txt

#### 🎯 Proč to potřebuješ?

Python = Nejpopulárnější jazyk pro Data Engineering!

#### 📚 Teorie (10 minut)

**Co je Python?**
- Programovací jazyk
- Easy to learn, powerful
- Data Science standard

**Virtual Environment (venv)?**
- Izolované Python prostředí
- Projektu A ≠ Projektu B
- Best practice!

#### 💻 Praktika (35 minut)

##### Instalace Python

**Check:**
```bash
python --version
# Měl bys vidět: Python 3.13.x
```

**Pokud nemáš:**

**Mac:**
```bash
brew install python@3.13
```

**Windows:**
1. https://www.python.org/downloads/
2. Download Python 3.13
3. **DŮLEŽITÉ:** Zaškrtni "Add Python to PATH"
4. Install

**Linux:**
```bash
sudo apt-get install python3.13
```

##### Virtual Environment Setup

```bash
# V H:\Můj disk\DATA ENGINEER JOURNEY\

# Vytvoř venv
python -m venv venv

# Aktivuj venv
# Mac/Linux:
source venv/bin/activate

# Windows:
venv\Scripts\activate

# Ověř (měl bys vidět "(venv)" na začátku):
# (venv) H:\Můj disk\DATA ENGINEER JOURNEY>
```

##### Requirements.txt

Vytvoř soubor: `requirements.txt`

```
# Core
pandas==2.0.3
numpy==1.24.3
requests==2.31.0

# Database
sqlalchemy==2.0.20
psycopg2-binary==2.9.7
duckdb==0.8.1

# Data formats
pyarrow==12.0.1
openpyxl==3.1.2

# Utilities
python-dotenv==1.0.0
pydantic==2.0.0

# Testing
pytest==7.4.0

# Development
black==23.7.0
flake8==6.0.0
```

##### Instalace balíčků

```bash
# Se zapnutým venv:
pip install -r requirements.txt

# Ověř:
pip list
# Měl bys vidět pandas, numpy, atd.

# Test:
python -c "import pandas; print(pandas.__version__)"
# Output: 2.0.3
```

#### ✅ Cvičení

```bash
# Cvičení 1: První Python script
# Vytvoř: hello.py

print("Hello, Data Engineer!")
x = [1, 2, 3, 4, 5]
print(f"Sum: {sum(x)}")

# Spusť:
python hello.py
# Output: Hello, Data Engineer!
#         Sum: 15

# Cvičení 2: Pandas
import pandas as pd
df = pd.DataFrame({'A': [1, 2, 3], 'B': [4, 5, 6]})
print(df)

# Cvičení 3: Requirements
pip freeze > requirements.txt
git add requirements.txt
git commit -m "📋 Add Python requirements"
```

#### 📋 Checklist

- [ ] Python 3.13+ je nainstalovaný
- [ ] venv je vytvořený a aktivní
- [ ] requirements.txt je vytvořený
- [ ] Balíčky jsou nainstalované
- [ ] Hello script funguje
- [ ] Pandas funguje
- [ ] requirements.txt je v Gitu

---

### MODUL 004: TERMINAL BASICS

**Doba:** 60 minut  
**Obtížnost:** ⭐ Lehká  
**Prerekvizity:** 001, 003  
**Výsledek:** Terminal power user!

#### 🎯 Proč to potřebuješ?

Terminal = Superhrnka programátora! 🦸

#### 📚 Teorie (15 minut)

**Co je Terminal?**
- Příkazová řádka
- Moc > GUI
- Programátoři to používají pořád

**Mac Terminal vs Windows PowerShell:**
- Mac: `Terminal` (v /Applications/Utilities/)
- Windows: `PowerShell` (vyhledej "PowerShell")

#### 💻 Praktika (45 minut)

##### Základní příkazy

```bash
# Current directory
pwd  # Print working directory

# List files
ls          # Mac/Linux
dir         # Windows (ale PowerShell zná taky "ls")
ls -la      # Všechny soubory včetně skrytých

# Change directory
cd folder/
cd ..       # Jdi nahoru
cd ~        # Home directory
cd -        # Předchozí directory

# Vytvoř složku
mkdir mojeFolder
mkdir mojeFolder/subfolder

# Vytvoř soubor
touch hello.txt  # Mac/Linux
echo. > hello.txt  # Windows

# Přesuň/přejmenuj
mv oldName.txt newName.txt
move oldName.txt newName.txt  # Windows

# Smaž
rm hello.txt  # Mac/Linux
del hello.txt  # Windows

# Všechny soubory v adresáři
ls *.md     # Jen .md soubory
ls -la | grep python  # Hledej "python"

# Tree struktura
tree        # Mac/Linux
tree /F     # Windows
```

##### Git comandy (Terminal)

```bash
# Status
git status          # Co se změnilo?

# Přidej do stagia
git add .           # Všechny soubory
git add filename    # Jen jeden soubor

# Commitni
git commit -m "📝 Message"

# Pushni
git push            # GitHub

# Pulluj (stáhni z GitHub)
git pull

# Log
git log --oneline   # Істория v jednom řádku

# Branches
git branch          # Vidíš branches
git checkout main   # Přepni na main
```

##### Python v Terminálu

```bash
# Python verze
python --version

# Spusť script
python hello.py

# Interactive Python
python
>>> x = 5
>>> print(x * 2)
10
>>> exit()

# Virtual environment
python -m venv venv
source venv/bin/activate  # Mac/Linux
venv\Scripts\activate     # Windows

# Instalace balíčků
pip install pandas
pip list
pip freeze > requirements.txt
```

#### ✅ Cvičení

```bash
# Cvičení 1: Navigace
pwd
cd ~
mkdir terminal-test
cd terminal-test
ls

# Cvičení 2: Soubory
touch test1.txt test2.txt test3.txt
ls *.txt
rm test3.txt
ls

# Cvičení 3: Git
git init
git add .
git commit -m "🎉 Terminal practice"
git log --oneline

# Cvičení 4: Python
python
>>> print("Terminal is awesome!")
>>> exit()
```

#### 📋 Checklist

- [ ] Terminal je otevřený
- [ ] pwd, ls, cd, mkdir fungují
- [ ] Git commandy fungují
- [ ] Python script funguje z terminálu
- [ ] Vmenv aktivace funguje

---

### MODUL 005: VS CODE SETUP

**Doba:** 45 minut  
**Obtížnost:** ⭐ Nula  
**Prerekvizity:** 001, 003, 004  
**Výsledek:** VS Code fully configured!

#### 🎯 Proč to potřebuješ?

VS Code = Best editor pro programování! (2025)

#### 📚 Teorie (10 minut)

**Co je VS Code?**
- Free editor od Microsoftu
- Extensions (pluginy)
- Built-in terminal
- Git integration
- Python, SQL, Markdown support

#### 💻 Praktika (35 minut)

##### Instalace

1. https://code.visualstudio.com/
2. Download
3. Install
4. Otevři

##### První otevření

```
File → Open Folder → H:\Můj disk\DATA ENGINEER JOURNEY
```

##### Essential Extensions

Instalace: Extensions icon (4 čtverečky vlevo) → Search

**Extension 1: Python**
- Author: Microsoft
- Install
- Settings: Auto-format on save

**Extension 2: Pylance**
- Author: Microsoft
- Install
- IntelliSense pro Python

**Extension 3: Markdown Preview Enhanced**
- Čti .md soubory s preview

**Extension 4: Git Graph**
- Vizualizace Git history

**Extension 5: Thunder Client** (optional)
- API testing (později pro GCP)

##### Settings

`File → Preferences → Settings` (nebo Cmd+,)

```
# Search:
"Python: Formatting Provider" → black
"Format On Save" → ON
"Tab Size" → 2 (nebo 4)
"Word Wrap" → ON
"Theme" → One Dark Pro (nebo Dark+)
```

##### Workspace Setup

Vytvoř: `.vscode/settings.json`

```json
{
  "python.defaultInterpreterPath": "${workspaceFolder}/venv/bin/python",
  "python.formatting.provider": "black",
  "editor.formatOnSave": true,
  "[python]": {
    "editor.defaultFormatter": "ms-python.python"
  },
  "files.exclude": {
    "**/__pycache__": true,
    "**/*.pyc": true
  }
}
```

##### Terminal v VS Code

```
Terminal → New Terminal
# Měl bys vidět: venv\Scripts\activate (Windows)
#                nebo source venv/bin/activate (Mac)
```

##### Python script v VS Code

Vytvoř: `hello_vscode.py`

```python
# Test script
print("Hello from VS Code!")

# With imports
import pandas as pd
data = pd.DataFrame({'A': [1, 2, 3]})
print(data)

# Run: F5 nebo Terminal: python hello_vscode.py
```

#### ✅ Cvičení

```
Cvičení 1: Otevři GitHub repo
- File → Open Folder
- Vyber DATA ENGINEER JOURNEY

Cvičení 2: Vytvoř Python script
- New file: test.py
- Napíš kód
- F5 to run

Cvičení 3: Git integrační
- Modifikuj hello.md
- Vlevo uvidíš "M" (modified)
- Source Control → Commit
- Push

Cvičení 4: Terminal
- Terminal → New Terminal
- git log
- python --version
```

#### 📋 Checklist

- [ ] VS Code nainstalovaný
- [ ] Python extension instalovaná
- [ ] Pylance instalovaný
- [ ] venv je vybraný jako interpreter
- [ ] Python script funguje (F5)
- [ ] Terminal funguje
- [ ] Git integration funguje
- [ ] Settings.json vytvořený

---

## 📝 VŠECHNY ŠABLONY

### Daily Note Template

```markdown
---
date: 2025-12-04
week: 49
type: daily
---

# Daily Note - čtvrtek, 4. prosince 2025

## 🎯 Dnešní plánuji
- [ ] Modul: 
- [ ] Praktika: 
- [ ] Commit: 

## 📚 Co jsem se naučil
Zde napiš klíčové body z modulu:
- Koncept 1:
- Koncept 2:
- Koncept 3:

## 💻 Kód co jsem napsal
\`\`\`python
# Code zde
print("Hello")
\`\`\`

## 🐛 Problémy co jsem měl
- Problém 1: Řešení
- Problém 2: Řešení

## 🤔 Otázky #question
Tady jsou moje otázky (budou odpovězeny Perplexity):
- Otázka 1?
- Otázka 2?

### 🤖 AI Odpověď
(Perplexity odpověď se vloží sem)

## ✅ Hotovo
Vypočítej XP a ulož:
- [ ] Daily login: 5 XP ✅
- [ ] Modul: 20 XP (Ano/Ne)
- [ ] Praktika: 10 XP (Ano/Ne)
- [ ] Git commit: 5 XP ✅
- [ ] Obsidian note: 5 XP ✅
- [ ] Perplexity otázka: 10 XP (Ano/Ne)

**TOTAL XP: __**

## 📊 Git
\`\`\`bash
git add .
git commit -m "📝 Day X: [Modul/Téma]"
git push
\`\`\`

---
*Created: 2025-12-04 15:10*
*Last update: 2025-12-04 15:10*
```

### Learn Note Template

```markdown
---
type: learning
date: 2025-12-04
tags: [learning, python, sql, gcp]
---

# Plán-Data-Engineer

## 🎯 Proč to potřebuji?
Řekni proč se to učíš:

## 📚 Klíčové koncepty
- **Koncept 1:** Vysvětlení
- **Koncept 2:** Vysvětlení
- **Koncept 3:** Vysvětlení

## 💡 Jak to funguje?
Detailní vysvětlení mechanismu:

## 💻 Příklady kódu
\`\`\`python
# Příklad 1
def hello():
    print("Hello")

# Příklad 2
class MyClass:
    pass
\`\`\`

## 🔗 Související
- [[Related-Note-1]]
- [[Moduli-Co-To-Vyžaduje]]

## ✅ Checklist porozumění
- [ ] Rozumím základům
- [ ] Praktika hotová
- [ ] Mohu to vysvětlit někomu dalšímu
- [ ] Mám příklady kódu

## 📝 Poznámky
Další poznámky:

---
*Created: 2025-12-04*
```

### Project Note Template

```markdown
---
type: project
status: 🔴 not-started
priority: 🔴 high
---

# Project: Plán-Data-Engineer

## 🎯 Cíl projektu
Co projekt dělá a proč?

## 📊 Tech Stack
- Language: Python / SQL / etc
- Database: PostgreSQL / BigQuery / DuckDB
- Cloud: GCP / AWS / etc
- Tools: Git, Obsidian, VS Code

## 📋 Fáze
- [ ] **Phase 1: Planning** (5 dní)
  - [ ] Requirements
  - [ ] Architecture
  - [ ] Data model

- [ ] **Phase 2: Setup** (3 dny)
  - [ ] Dev environment
  - [ ] GitHub repo
  - [ ] Folder struktura

- [ ] **Phase 3: Development** (10-14 dní)
  - [ ] Feature 1
  - [ ] Feature 2
  - [ ] Testing

- [ ] **Phase 4: Testing** (3-5 dní)
  - [ ] Unit tests
  - [ ] Integration tests
  - [ ] Documentation

- [ ] **Phase 5: Deployment** (2-3 dny)
  - [ ] Final polish
  - [ ] README
  - [ ] GitHub push

## 🔗 GitHub
- **Repo:** [Link]
- **Commits:** 
- **Status:** 

## 📈 Progress
- % done: 0% → 25% → 50% → 75% → 100%
- Last update: 2025-12-04

## 📝 Learnings
Co jsem se naučil v tomto projektu:
- Learning 1:
- Learning 2:

## 🐛 Problémy
- Problem 1: Solution
- Problem 2: Solution

---
*Created: 2025-12-04*
*Status: {{status}}*
```

### Weekly Review Template

```markdown
---
date: 2025-12-04
week: 49
type: weekly
---

# Weekly Review - Week 49 (Nov 2025)

## 📊 Week Stats
- Days completed: __/7
- Total XP: __
- Commits: __
- Daily notes: 7
- Modules: __

## 📈 XP Breakdown
- Daily login: 35 XP (5×7)
- Modules: __ XP
- Praktika: __ XP
- Git commits: 35 XP (5×7)
- Obsidian notes: 35 XP (5×7)
- Perplexity: __ XP

**TOTAL: __ XP**

## ✅ Completed
- [ ] Modul 001
- [ ] Modul 002
- [ ] Praktika hotová
- [ ] GitHub aktualný
- [ ] LinkedIn post

## ❌ Not completed
- [ ] Důvod 1:
- [ ] Důvod 2:

## 🎯 Next Week Goals
- [ ] Modul 003
- [ ] Modul 004
- [ ] Project start
- [ ] 50+ commits

## 📝 Learnings This Week
1. Lesson 1:
2. Lesson 2:

## 🐛 Blockers / Issues
- Issue 1:
- Issue 2:

## 💡 Improvement Actions
- Akce 1:
- Akce 2:

## 📅 Next Week Schedule
- Pondělí: Modul 003 (60 min)
- Úterý: Modul 004 (60 min)
- Středa: Praktika (90 min)
- Čtvrtek: Praktika (90 min)
- Pátek: Review (60 min)
- Sobota: Marathon (6h)

---
*Week started: 2025-12-04*
```

---

## 💰 CLAUDE AI STRATEGIE (Listopad 2025 - Březen 2026)

### Claude Tarify 2025

| Tarif | Cena | Features |
|-------|------|----------|
| **Free** | 0 Kč | Základní chat, limit 3 msg/min |
| **Claude Pro** | 500 Kč/měsíc | Unlimited messages, Claude 3.5 Sonnet |
| **Claude API** | Pay-as-you-go | $0.003 (input) / $0.015 (output) per 1K tokens |

### Naše Strategie - ZDARMA! 

```
Listopad 2025 - Březen 2026:
Používáme PERPLEXITY (máte Free tier)

Únor 2026:
Claude vyzkoušíme na FREE trial
```

### Perplexity vs Claude vs ChatGPT

| Feature | Perplexity | Claude | ChatGPT |
|---------|-----------|--------|---------|
| Web search | ✅ ANO | ❌ Ne | ❌ Ne |
| Real-time data | ✅ ANO | ❌ Ne | ❌ Ne |
| Free tier | ✅ 3-5 otázek/3h | ✅ Ano | ⚠️ Limited |
| Offline | ❌ Ne | ❌ Ne | ❌ Ne |
| Context length | 8K | 200K | 128K |
| Coding | 🟢 Dobré | 🟢🟢 Vyborné | 🟢 Dobré |
| Price | 500 Kč/měsíc | 500 Kč/měsíc | 500 Kč/měsíc |

### Naš AI Workflow

```
BĚHEM STUDIA:
1. Otevři Perplexity
2. Napíšeš otázku z modulu
3. Dostaneš odpověď
4. Zkopíruješ do Daily note
5. Git commit

PŘÍKLAD:
"Vysvětli mi jak funguje Git merge conflict"
→ Perplexity odpovídá
→ Zapíšeš si to do Obsidianu
→ Commit na GitHub
```

### Kdy Koupit Claude?

```
TEĎKA (Listopad 2025):
- NE - Perplexity stačí!
- Free tier postačuje

BŘEZEN 2026 (Po skončení plánu):
- ANO - Pro pokročilé projekty
- RAG implementace
- Custom AI features
```

---

## 🎮 GAMIFIKACE - DETAILNÍ

### XP Systém

**Denní XP:**
```
Daily login:              5 XP
Modul hotový:            20 XP
Cvičení hotová:          10 XP
Git commit:              5 XP
Obsidian note:           5 XP
Perplexity otázka:      10 XP
LinkedIn post:          10 XP
Code review:            10 XP
Bug fix:                10 XP
Documentation:          10 XP

MAX/DEN:                75 XP
```

**Týdenní:**
- 525 XP/týden (cíl)
- Streaks: +100 XP (7d), +200 XP (14d), +500 XP (30d)

**Celkový:**
- 23 týdnů
- 12,075 XP TOTAL
- Level 10 = Data Engineer! 👑

### Levely

```
L1  Initiate           (0-500 XP)          🔴
L2  Apprentice         (500-1,200 XP)      🔴
L3  Explorer           (1,200-2,000 XP)    🟡
L4  Cloud Wanderer     (2,000-3,000 XP)    🟡
L5  Data Architect     (3,000-4,500 XP)    🟢
L6  Pipeline Master    (4,500-6,000 XP)    🟢
L7  Data Vault Sage    (6,000-7,500 XP)    🔵
L8  Streaming Ninja    (7,500-9,000 XP)    🔵
L9  BI Master          (9,000-10,500 XP)   🟣
L10 Data Engineer      (10,500-12,075 XP)  👑
```

### Badges (30+)

```
BRONZE (Fundamenty):
🔰 Git Pioneer
🖥️ Terminal Novice
🐍 Python Starter
📝 Obsidian Scholar

SILVER (Programování):
🔍 SQL Seeker
💻 Python Developer
🗄️ DBeaver Explorer
📊 Code Committer

GOLD (Data Engineering):
🏗️ Modeler
☁️ Cloud Traveler
🔄 ETL Builder
📐 Architect

PLATINUM (Expert):
🌊 Streaming Master
📈 BI Expert
🎨 Portfolio Builder
🎤 Interview Ready

LEGENDARY:
🏆 GitHub Legend
💼 LinkedIn Influencer
🎉 HIRED!
```

---

## ✅ FINÁLNÍ CHECKLIST

```
SETUP:
☐ Git + GitHub
☐ Obsidian vault
☐ Python + venv
☐ VS Code
☐ Terminal

MĚSÍC 1:
☐ Moduly 001-005
☐ 50+ commits
☐ Daily notes: 28
☐ XP: 250-350

MĚSÍC 2:
☐ Moduly 006-010
☐ Project 1 hotový
☐ 100+ commits
☐ XP: 500-600

MĚSÍC 3:
☐ Moduly 011-016
☐ Project 2 hotový
☐ 150+ commits
☐ XP: 900-1,100

MĚSÍC 4:
☐ Moduly 017-020
☐ Project 3 hotový
☐ 300+ commits
☐ Interview ready
☐ XP: 12,075 ✅
```

---

## 🚀 ZAČÍNAŠ DNESKA!

```
TEĎKA:
1. Stáhni tento markdown
2. Vlož si ho do Obsidianu
3. Vytvoř GitHub repo
4. První commit!
5. Daily note: 2025-11-02

ZÍTRA:
6. Začni Modul 001
7. SSH setup
8. První GitHub push

TÝDEN 1:
9. Moduly 001 + 002
10. 10+ commits
11. Setup hotový!
```

---

**MÁTE VŠECHNO! JDETE NA TO?!** 🚀💪👑

*Vygenerováno: 2. listopadu 2025*  
*Verze: 2.0 FULL EDITION*  
*Status: 100% COMPLETE & READY!*
