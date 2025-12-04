# 🔵 MODUL 003: Python Setup - Tvoje programovací prostředí

**⏱️ Doba: 30-45 minut | Schwízkost: ⭐ Snadné | Předchází: 001 | Pokračuje: 006, 007**

---

## 🤔 PROČ TO POTŘEBUJEŠ?

Python = **programovací jazyk**, kterému se učíš. Ale jak ho spustíš?

**Analogie:**
- Python = kniha s recepty (kód)
- Python interpreter = kuchyň kde recepty vařiš (executable)
- Virtual env = separovaná kuchyň pro každou книгу (izolace)

Python samo o sobě na Macu/Linuxu již je, ale:
- Budeš potřebovat **konkrétní verzi** (3.9+)
- Budeš potřebovat **package manager** (pip) na instalaci knihoven
- Budeš potřebovat **virtual environment** (venv) aby se věci nekonflikovaly

---

## 🎯 CO SE DNESKA NAUČÍŠ

```
✓ Python 3.9+ je nainstalovaný
✓ pip (package manager) funguje
✓ Vytvoříš virtual environment
✓ Zaaktivuješ virtualenv
✓ Instaluješ první balíčky (pandas, numpy)
```

---

## 🛠️ INSTALACE (25 minut)

### Krok 1: Zkontroluj aktuální Python

```bash
python --version
```

nebo

```bash
python3 --version
```

**Očekávaný výstup:**
```
Python 3.9.0 (nebo vyšší)
```

**Pokud máš nižší verzi nebo nic:**

#### Mac:
```bash
brew install python@3.11
```

Pak:
```bash
alias python3=/usr/local/bin/python3.11
alias python=/usr/local/bin/python3.11
```

(Přidej to do `~/.zshrc` aby se pamatovalo!)

#### Windows:
Stáhni z https://www.python.org/downloads/ (verze 3.11)

Při instalaci ZAŠKRTNI: "Add Python to PATH"!

#### Linux:
```bash
sudo apt-get update
sudo apt-get install python3.11
```

### Krok 2: Zkontroluj pip

```bash
pip --version
```

**Očekávaný výstup:**
```
pip 23.0 from /usr/local/lib/python3.11/site-packages/python (python 3.11)
```

### Krok 3: Vytvoř virtual environment

V terminálu:

```bash
cd ~/Projects/data-engineer-study-2026
python -m venv venv
```

**Co se stalo?** Vytvoří se složka `venv/` s isolovaným Python prostředím.

```
data-engineer-study-2026/
├── venv/               ← Tady je tvůj izolovaný Python
├── Obsidian-Vault/
└── README.md
```

### Krok 4: Zaaktivuj virtualenv

**Mac/Linux:**
```bash
source venv/bin/activate
```

**Windows:**
```bash
venv\Scripts\activate
```

**Jak poznáš, že je zaaktivovaný?**

V terminálu před promptem se objeví `(venv)`:

```
(venv) ivo@MacBook data-engineer-study-2026 %
```

### Krok 5: Upgraduj pip (doporučeno)

```bash
pip install --upgrade pip
```

### Krok 6: Instaluj základní balíčky

```bash
pip install pandas numpy matplotlib jupyter
```

**Výstup bude dlouhý:**
```
Collecting pandas
  Downloading pandas-2.0.0-cp311-cp311-macosx_11_0_arm64.whl (11.3 MB)
...
Successfully installed pandas-2.0.0 numpy-1.24.0 ...
```

---

## 📝 requirements.txt - Vždy to udržuj!

Aby ostatní věděli jaké balíčky máš, vytvoř soubor:

`requirements.txt`

```
pandas==2.0.0
numpy==1.24.0
matplotlib==3.7.0
jupyter==1.0.0
```

Později budeš moct udělat:

```bash
pip install -r requirements.txt
```

a všechno se nainstauje najednou!

**Git task:**

```bash
git add requirements.txt
git commit -m "🐍 Python 3.11 setup with pandas, numpy, matplotlib, jupyter"
git push
```

---

## ✅ CHECKLIST

- [ ] Python 3.9+ je nainstalován (`python --version` vrací 3.9+)
- [ ] pip je nainstalován (`pip --version` funguje)
- [ ] Virtual environment je vytvořen (existuje `venv/` složka)
- [ ] Virtual environment je zaaktivovaný (`(venv)` v terminálu)
- [ ] Balíčky jsou nainstalovány (`pip list` ukazuje pandas, numpy, atd.)
- [ ] requirements.txt je vytvořen v root repo
- [ ] requirements.txt je v Gitu

---

## 🔗 PROPOJENÍ - Kam jde dál?

```
TEĎKA (Ty): 003-Python-Setup
├─ ✅ Python je připravený
├─ ✅ Virtual env je aktivní

PŘÍŠTĚ:
├─ 004-Terminal-Basics (Jak si navigovat terminálem?)
├─ 005-VS-Code-Setup (Kde budeš psát kód?)
└─ 006-Python-Refresher-Part1 (Začneš programovat!)
```

---

## 📝 GITHUB TASK

```bash
# Přidej venv/ do .gitignore
echo "venv/" >> .gitignore
git add requirements.txt .gitignore
git commit -m "🐍 Python setup + virtual environment"
git push
```

---

## 🎓 SHRNUTÍ

Python je teď ready! Důležité:

1. **Vždy aktivuj virtualenv** předtím než začneš pracovat:
   ```bash
   source venv/bin/activate  # Mac/Linux
   ```

2. **Když instaluješ nový balíček**, aktualizuj requirements.txt:
   ```bash
   pip install novy-balik
   pip freeze > requirements.txt
   ```

3. **Virtual environment je pro IZOLACI** - každý projekt má svůj Python!

**Příští lekce:** Terminal basics nebo VS Code?

---

**Máš otázky?** Perplexity: "Proč se používá virtual environment v Pythonu?"
