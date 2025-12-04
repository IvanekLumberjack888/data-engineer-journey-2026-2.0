# 🎓 ČEAT SHEET: Všechny příkazy na jednom místě

Používej to když si pamatuješ příkaz, ale ne přesnou syntax!

---

## 🟦 GIT CHEAT SHEET

### Setup
```bash
git config --global user.name "Ivo Dolezal"
git config --global user.email "ivo@example.com"
ssh-keygen -t ed25519 -C "ivo@example.com"
```

### Repo Management
```bash
git init                                    # Vytvoř nový repo
git clone git@github.com:user/repo.git     # Klonuj repo
git remote add origin git@github.com:...   # Přidej GitHub repo
git remote -v                              # Zkontroluj remotes
```

### Staging & Committing

```bash
cd "H:\Můj disk\DATA ENGINEER JOURNEY"
git status                                  # Pokaž status
git add .                                   # Přidej všechno
git commit -m "📝 Message"                  # Commitni
git push                                    # Pushni do GitHub
```

### Branches
```bash
git branch                                  # Pokaž branches
git branch feature-x                        # Vytvoř branch
git checkout feature-x                      # Přepni branch
git merge feature-x                         # Merguj branch
```

### History & Undo
```bash
git log                                     # Pokaž historii
git log --oneline                           # Krátká historie
git show abc123                             # Pokaž commit
git diff                                    # Pokaž změny
git restore file.py                         # Undo changes
```

---

## 🐍 PYTHON CHEAT SHEET

### Basics
```python
# Komentář
x = 5  # integer
s = "text"  # string
b = True  # boolean

# Operace
x + 2  # 7
x * 2  # 10
s.upper()  # "TEXT"
```

### Datové struktury
```python
# List (mutable)
l = [1, 2, 3]
l.append(4)
l[0]  # 1

# Tuple (immutable)
t = (1, 2, 3)
t[0]  # 1

# Dictionary
d = {"name": "Ivo", "age": 30}
d["name"]  # "Ivo"
d.keys()  # dict_keys(['name', 'age'])

# Set
s = {1, 2, 3}
s.add(4)
```

### Funkce
```python
def hello(name):
    """Docstring - popis funkce."""
    return f"Ahoj {name}!"

result = hello("Ivo")
```

### Loops
```python
# For loop
for i in [1, 2, 3]:
    print(i)

# While loop
while i < 10:
    i += 1

# List comprehension
squares = [x**2 for x in [1, 2, 3]]  # [1, 4, 9]
```

### File I/O
```python
# Čtení
with open("file.txt") as f:
    content = f.read()

# Psaní
with open("file.txt", "w") as f:
    f.write("Obsah")
```

### Imports
```python
import pandas
import numpy as np
from datetime import datetime
```

---

## 🐬 SQL CHEAT SHEET

### SELECT
```sql
SELECT name, age FROM users;
SELECT * FROM users;
SELECT DISTINCT country FROM users;
SELECT COUNT(*) as total FROM users;
```

### WHERE & Operators
```sql
SELECT * FROM users WHERE age > 18;
SELECT * FROM users WHERE country = 'CZ' AND age > 18;
SELECT * FROM users WHERE name LIKE 'Iv%';
SELECT * FROM users WHERE age IN (18, 19, 20);
```

### JOIN
```sql
SELECT u.name, o.order_id
FROM users u
INNER JOIN orders o ON u.id = o.user_id;

-- LEFT JOIN vrací všechny z LEFT tabulky
-- RIGHT JOIN vrací všechny z RIGHT tabulky
-- FULL JOIN vrací všechny
```

### GROUP BY & HAVING
```sql
SELECT country, COUNT(*) as total
FROM users
GROUP BY country;

SELECT country, COUNT(*) as total
FROM users
GROUP BY country
HAVING COUNT(*) > 10;
```

### ORDER & LIMIT
```sql
SELECT * FROM users ORDER BY age DESC LIMIT 10;
```

### Window Functions
```sql
SELECT 
    name, 
    salary,
    ROW_NUMBER() OVER (ORDER BY salary DESC) as rank
FROM employees;

-- Running sum
SELECT 
    order_date, 
    amount,
    SUM(amount) OVER (ORDER BY order_date) as running_total
FROM orders;
```

### Aggregates
```sql
COUNT(*)        -- Počet řádků
SUM(column)     -- Součet
AVG(column)     -- Průměr
MIN(column)     -- Minimum
MAX(column)     -- Maximum
```

---

## 🟧 TERMINAL CHEAT SHEET

### Navigation
```bash
pwd                             # Kde jsem?
ls                              # Co je tady?
cd /path/to/folder              # Jdi tam
cd ~                            # Home directory
cd ..                           # O úroveň výš
cd -                            # Zpátky kam jsem byl
```

### Files & Folders
```bash
mkdir folder                    # Vytvoř složku
touch file.txt                  # Vytvoř soubor
cp source.txt dest.txt          # Kopíruj
mv old.txt new.txt              # Přesun/Přejmenuj
rm file.txt                     # Smaž soubor
rm -rf folder/                  # Smaž složku
cat file.txt                    # Vypíš obsah
```

### Viewing Files
```bash
less file.txt                   # Čtení s paging
head file.txt                   # Prvních 10 řádků
tail file.txt                   # Posledních 10 řádků
wc -l file.txt                  # Počet řádků
```

### Searching
```bash
grep "pattern" file.txt         # Hledej v souboru
find . -name "*.py"             # Hledej soubory
```

### Processes
```bash
ps aux                          # Pokaž procesy
kill 1234                       # Zabij proces
top                             # Monitor ressources
```

### Permissions
```bash
chmod +x script.sh              # Udělej spustitelný
chmod 755 file                  # Nastav práva
```

---

## 🔷 DOCKER CHEAT SHEET (Když budeš potřebovat)

### Images
```bash
docker pull postgres            # Stáhni image
docker images                   # Pokaž images
docker build -t myapp .         # Build image
```

### Containers
```bash
docker run -d -p 5432:5432 postgres  # Spusť PostgreSQL
docker ps                       # Pokaž running containers
docker stop container_id        # Zastaví container
docker rm container_id          # Smaž container
```

### Logs
```bash
docker logs container_id        # Pokaž logy
docker exec -it container_id bash   # Vstup do containeru
```

---

## 📊 VSCODE SHORTCUTS

### File Management
```
Cmd+P (Mac) / Ctrl+P (Windows)     # Quick open file
Cmd+N / Ctrl+N                     # Nový soubor
Cmd+W / Ctrl+W                     # Zavři soubor
Cmd+Shift+P / Ctrl+Shift+P         # Command palette
```

### Editing
```
Cmd+/ / Ctrl+/                     # Comment line
Cmd+D / Ctrl+D                     # Select next match
Cmd+Shift+L / Ctrl+Shift+L         # Select all matches
Cmd+L / Ctrl+L                     # Select line
Cmd+X / Ctrl+X                     # Cut line
```

### Navigation
```
Cmd+G / Ctrl+G                     # Go to line
Cmd+] / Ctrl+]                     # Indent
Cmd+[ / Ctrl+[                     # Unindent
Cmd+Shift+] / Ctrl+Shift+]         # Go to closing bracket
```

### Terminal
```
Cmd+` (backtick)                   # Toggle terminal
Ctrl+Shift+` (backtick)            # Nový terminal
```

---

## 🌐 GCP CHEAT SHEET (Základy)

### gcloud CLI
```bash
gcloud init                     # Setup gcloud
gcloud auth login              # Login
gcloud config set project PROJECT_ID
gcloud projects list           # Pokaž projekty
```

### BigQuery
```bash
bq ls                          # Pokaž datasets
bq query "SELECT 1"            # Spusť query
bq load dataset.table file.csv # Uploaduj data
bq export dataset.table gs://bucket/file.csv  # Export
```

### Cloud Storage
```bash
gsutil ls                      # Pokaž buckets
gsutil cp file.txt gs://bucket/  # Upload
gsutil cp gs://bucket/file.txt .  # Download
```

---

## 📦 PIP CHEAT SHEET (Python Packages)

### Installation
```bash
pip install package_name       # Instaluj
pip install package==1.2.3     # Konkrétní verzi
pip install -r requirements.txt # Z requirements.txt
```

### Management
```bash
pip list                       # Pokaž nainstalované
pip show pandas                # Info o balíčku
pip freeze > requirements.txt  # Export do requirements.txt
pip uninstall package_name     # Odinstaluj
```

### Virtual Environment
```bash
python -m venv venv           # Vytvoř venv
source venv/bin/activate      # Aktivuj (Mac/Linux)
venv\Scripts\activate          # Aktivuj (Windows)
deactivate                     # Deactivuj
```

---

## 🎓 CO SI PAMATOVAT

**GIT:**
- `git add .` + `git commit -m "..."` + `git push` = workflow
- Dělej commits často!
- Má messaging je super pro recruiteery!

**PYTHON:**
- Indentation je povinná!
- Virtual env = izolace
- f-strings pro formatting: f"Ahoj {jméno}!"

**SQL:**
- JOIN je king
- SELECT * je špatná praxe
- Window functions = power moves

**TERMINAL:**
- Tab auto-complete = tvůj nejlepší kamarád
- Ctrl+C = zastaví program
- Arrow keys = navigace v historii

**VSCODE:**
- Cmd+P = nejužitečnější zkratka
- Format on Save = hezkej kód
- Integrated Terminal = bez přepínání

---

## 🔴 常見CHYBY & ŘEŠENÍ

| Chyba | Řešení |
|-------|--------|
| `command not found: git` | Git není nainstalovaný |
| `Permission denied (publickey)` | SSH klíč není nastaven |
| `ModuleNotFoundError: No module named 'pandas'` | `pip install pandas` v aktivovaném venv |
| `python: command not found` | Python není nainstalovaný, zkus `python3` |
| `Port already in use` | Jiný program používá port, `kill` process |
| `Connection refused` | Server není běhující, check status |

---

## 📖 DOPORUČENÉ ZDROJE

- **Python:** https://docs.python.org/3/
- **SQL:** https://www.w3schools.com/sql/
- **Git:** https://git-scm.com/doc
- **GCP:** https://cloud.google.com/docs
- **Bash:** https://www.gnu.org/software/bash/manual/
- **PostgreSQL:** https://www.postgresql.org/docs/

---

**Vždycky si pamatuj:** Google je tvůj nejlepší kamarád! 🚀
