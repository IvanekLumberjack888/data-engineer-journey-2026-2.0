# 🟣 MODUL 005: VS Code Setup - Tvůj editor

**⏱️ Doba: 45 minut | Schwízkost: ⭐ Lehká | Předchází: 001, 003, 004 | Pokračuje: 006+**

---

## 🤔 PROČ TO POTŘEBUJEŠ?

VS Code = **editor** kde budeš psát kód (Python, SQL, YAML, Markdown).

**Proč VS Code?**
- Zdarma
- Nejtěžší na Internetu
- Pracuje i na notebooku + TV
- Integrovaný Terminal
- Extensiony pro vše (Python, Perplexity, GitHub, Markdown)

**Vs. PyCharm:**
- PyCharm = těžký, pro Pure Python
- VS Code = lehký, pro ALL languages (Python, SQL, JSON, YAML, Bash, Go, Rust...)

Data engineeři pracují s více jazyky - VS Code je ideální!

---

## 🎯 CO SE DNESKA NAUČÍŠ

```
✓ VS Code instalace
✓ Extensions: Python, Pylance, Perplexity, GitHub Copilot
✓ Workspace setup (tvůj projekt)
✓ Settings (indentation, formatting, atd.)
✓ Integrated terminal (bez sepraného okna)
```

---

## 🛠️ INSTALACE (10 minut)

### Krok 1: Stáhni VS Code

Jdi na https://code.visualstudio.com a stáhni pro Mac/Windows/Linux.

Instaluj jako normální aplikaci.

### Krok 2: Otevři tvůj projekt

```bash
cd ~/Projects/data-engineer-study-2026
code .
```

**Co to dělá?** Otevře tvůj projekt ve VS Code.

(Pokud `code` příkaz nefunguje na Macu, podívej se sem: https://code.visualstudio.com/docs/setup/mac)

---

## 🔌 EXTENSIONS - Instalace (20 minut)

Extensions = super schopnosti pro VS Code.

### Extension 1: Python (POVINNÉ)

1. Klikni na Extensions (levý panel, ikonka se čtverci)
2. Hledej "Python"
3. Instaluj extension od Microsoftu (má vlajku)

**Co to dělá?** VS Code rozumí Python kódu - highlighting, formatting, debugging.

### Extension 2: Pylance (POVINNÉ)

1. Hledej "Pylance"
2. Instaluj

**Co to dělá?** Intelisense (auto-complete) pro Python.

### Extension 3: Perplexity (DOPORUČUJI)

1. Hledej "Perplexity"
2. Instaluj od Perplexity

**Co to dělá?** Můžeš se ptát Perplexity přímo z VS Code bez přepínání oken!

**Jak to používat:**
- Ctrl+Shift+P (Mac: Cmd+Shift+P)
- Napíšeš "Perplexity: Ask"
- Píšeš otázku
- Dostáneš odpověď vpravo

### Extension 4: GitHub Copilot (VOLITELNÉ)

1. Hledej "GitHub Copilot"
2. Instaluj

**Co to dělá?** AI auto-complete pro kód. (Ale máš již Perplexity, tak to není kritické.)

### Extension 5: Live Share (VOLITELNÉ, ale cool)

1. Hledej "Live Share"
2. Instaluj

**Co to dělá?** Můžeš se podílet na kódu se někým jiným v reálném čase.

### Extension 6: Markdown All in One (DOPORUČUJI)

1. Hledej "Markdown All in One"
2. Instaluj

**Co to dělá?** Lepší podpora Markdownu (seznam, tabulky, formatting).

### Extension 7: Git Graph (VOLITELNÉ)

1. Hledej "Git Graph"
2. Instaluj

**Co to dělá?** Vizuální zobrazení Git historii. Super pro pochopení branching!

---

## ⚙️ SETTINGS - Konfigurace (10 minut)

VS Code má miliony nastavení. Zde je pro tebe důležité:

### Krok 1: Otevři Settings

Cmd+, (Mac) nebo Ctrl+, (Windows/Linux)

### Krok 2: Hledej "Tab Size"

Nastav na **4** (Python standard)

```
Tab Size: 4
```

### Krok 3: Hledej "Format on Save"

Zaškrtni:
```
Editor: Format On Save ✓
```

**Co to dělá?** Když uložíš soubor, automaticky se zformátuje!

### Krok 4: Hledej "Python Default Interpreter"

Měl by automaticky zvolit tvůj `venv`! Pokud ne:

1. Cmd+Shift+P (Mac) nebo Ctrl+Shift+P (Windows)
2. Napíšeš "Python: Select Interpreter"
3. Vyber `/Users/ivo/Projects/data-engineer-study-2026/venv/bin/python`

### Krok 5: Hledej "Render Whitespace"

Nastav na "boundary":
```
Render Whitespace: boundary
```

**Co to dělá?** Ukazuje ti mezery - super pro debugging!

---

## 🎨 THEME - Vzhled (5 minut)

Hezký theme je důležitý! (Pro motivaci)

### Hledej: "Color Theme"

Doporučuji:
- **Dracula** (temný, pro noc)
- **One Dark Pro** (temný, moderní)
- **Synthwave '84** (cool retro vibes!)
- **Nord** (studený modrý, super pro data!)

Zkus si několik a vyber co se ti líbí!

---

## 📂 WORKSPACE - Struktura v VS Code (5 minut)

V levém panelu vidíš soubory. Mělo by to vypadat takto:

```
data-engineer-study-2026/
├── 📁 .git/ (skrytá)
├── 📁 .github/
├── 📁 Obsidian-Vault/
├── 📁 projects/
│   ├── 📁 project-1-etl/
│   ├── 📁 project-2-cloud/
│   └── 📁 project-3-streaming/
├── 📁 venv/ (skrytá - ale viditelná)
├── 📄 .gitignore
├── 📄 README.md
└── 📄 requirements.txt
```

### Ignorování venv/ (neviditelné)

`.gitignore` by měl obsahovat:
```
venv/
.DS_Store
__pycache__/
*.pyc
.env
```

Pokud neobsahuje, přidej!

---

## ⌨️ KEYBOARD SHORTCUTS - Top 10

| Shortcut | Co dělá |
|----------|---------|
| Cmd+B (Mac) | Skryj/Ukaž levý panel |
| Cmd+` (backtick) | Otevři/Zavři Integrated Terminal |
| Cmd+P | Hledaj soubor (magic!) |
| Cmd+Shift+P | Command palette (ALL commands) |
| Cmd+/ | Comment/Uncomment řádek |
| Cmd+D | Select next occurrence (pro refactoring!) |
| Cmd+L | Select celý řádek |
| Cmd+Shift+L | Select všechny výskyty slova |
| Cmd+Enter | Insert řádek níže |
| Cmd+Shift+Enter | Insert řádek výše |

---

## 💻 PRAKTIKA (5 minut)

### Cvičení 1: Nový Python soubor

```bash
# V VS Code:
# 1. Klikni na projects/project-1-etl/
# 2. Right-click → New File
# 3. Název: hello.py
```

Napíšeš:

```python
def hello(name):
    """Szdraví osobu jménem name."""
    return f"Ahoj {name}!"

if __name__ == "__main__":
    print(hello("Ivo"))
```

### Cvičení 2: Spustit Python skript

```bash
# Otevři Integrated Terminal (Cmd+`)
# Měl by být v ~/Projects/data-engineer-study-2026

cd projects/project-1-etl
python hello.py

# Výstup:
# Ahoj Ivo!
```

### Cvičení 3: Formování

```bash
# Udělej nějaký "špatný" kód:
x=1
y=2
z=x+y

# Ulož soubor (Cmd+S)
# VS Code automaticky zformátuje:
x = 1
y = 2
z = x + y
```

---

## ✅ CHECKLIST

- [ ] VS Code je nainstalovaný
- [ ] Můžeš otevřít svůj projekt (`code .` funguje)
- [ ] Extension "Python" je nainstalovaný
- [ ] Extension "Pylance" je nainstalovaný
- [ ] Extension "Perplexity" je nainstalovaný
- [ ] Tab Size je nastaven na 4
- [ ] Format on Save je zapnutý
- [ ] Python interpreter je tvůj venv
- [ ] Integrated Terminal funguje (Cmd+`)
- [ ] Můžeš spustit Python skript

---

## 🔗 PROPOJENÍ - Kam jde dál?

```
TEĎKA (Ty): 005-VS-Code-Setup
├─ ✅ VS Code je tvůj editor

PŘÍŠTĚ:
├─ 006-Python-Refresher-Part1 (Píšeš Python!)
├─ 007-Python-Refresher-Part2 (OOP)
└─ 008-SQL-Basics-Part1 (SQL queries)

VŠE BUDE PSÁNO:
└─ V VS Code!
```

---

## 📝 GITHUB TASK

```bash
# Pushni hello.py do projektu

git add projects/project-1-etl/hello.py
git commit -m "🎨 VS Code setup - first Python script"
git push
```

---

## 🎓 SHRNUTÍ

VS Code je teď tvůj home! Pamatuj si:

1. **Extensions** = super schopnosti (Python, Perplexity, Git)
2. **Settings** = tvůj kód bude hezký (format on save!)
3. **Integrated Terminal** = bez přepínání oken
4. **Keyboard Shortcuts** = budeš asi 2x rychleji

**Příští lekce:** Python refresher - začneš programovat!

---

**Máš otázky?** Perplexity: "Jaké jsou nejlepší VS Code extensions pro Python?"
