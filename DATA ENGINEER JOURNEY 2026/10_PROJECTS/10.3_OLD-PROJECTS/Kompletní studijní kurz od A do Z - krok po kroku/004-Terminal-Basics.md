# 🟢 MODUL 004: Terminal Basics - Jak se pohybovat v terminálu

**⏱️ Doba: 45-60 minut | Schwízkost: ⭐ Lehká | Předchází: 001 | Pokračuje: Všechny ostatní**

---

## 🤔 PROČ TO POTŘEBUJEŠ?

Terminal = **text-basovaná komunikace s tvým počítačem**.

**Proč ne GUI (klikání)?**
- Programátoři jsou lazí - psaní je rychlejší než klikání 😄
- Terminal je powerfulnější
- Data engineeři pracují na serverech bez GUI
- Git, Python, Docker - všechno se ovládá z terminálu

**Analogie:**
- GUI = telefonování (pomalé, pěkné, limitované)
- Terminal = SMS (rychlé, textové, neomezené)

---

## 🎯 CO SE DNESKA NAUČÍŠ

```
✓ Otevření terminálu
✓ Základní příkazy (pwd, ls, cd, mkdir, touch, rm)
✓ File system orientace (cesty, absolutní vs relativní)
✓ Vytváření souborů a složek
✓ Navigace mezi složkami
✓ Git příkazy v terminálu
```

---

## 📚 TEORIE - File system (10 minut)

### Adresářová struktura

Tvůj počítač má následující strukturu:

**Mac/Linux:**
```
/Users/ivo/                    ← Home directory (~)
├── Projects/                  ← Tvoje projekty
│   ├── data-engineer-study-2026/
│   ├── other-project/
│   └── ...
├── Documents/
├── Downloads/
└── ...
```

**Windows:**
```
C:\Users\ivo\                  ← Home directory
├── Projects\
│   ├── data-engineer-study-2026\
│   └── ...
├── Documents\
└── ...
```

### Absolutní vs Relativní cesty

**Absolutní** = od root do složky (úplná cesta):
```
/Users/ivo/Projects/data-engineer-study-2026
```

**Relativní** = od tvého současného místa:
```
# Jestli jsi v /Users/ivo/, pak:
Projects/data-engineer-study-2026  ← to je relativní cesta
```

---

## 🛠️ ZÁKLADNÍ PŘÍKAZY (20 minut)

### Otevření terminálu

**Mac:**
- Cmd+Space → napíšeš "terminal" → Enter

**Windows:**
- Win+R → napíšeš "powershell" → Enter

**Linux:**
- Ctrl+Alt+T

### Příkaz 1: pwd (Print Working Directory)

```bash
pwd
```

Výstup:
```
/Users/ivo/Projects/data-engineer-study-2026
```

**Co to dělá?** Řekne ti, kde právě jsi v file systemem.

### Příkaz 2: ls (List)

```bash
ls
```

Výstup:
```
Obsidian-Vault      README.md           venv
projects            requirements.txt
```

**Co to dělá?** Ukáže ti co je v aktuální složce.

**Užitečná varianta:**
```bash
ls -la   # Pokaž i skryté soubory (začínají .)
```

### Příkaz 3: cd (Change Directory)

```bash
cd Projects/data-engineer-study-2026
```

**Co to dělá?** Jdeš do zadané složky.

**Speciální cesty:**
```bash
cd ~                # Jdi do Home directory
cd -                # Jdi zpátky kde jsi byl
cd ..               # Jdi o jednu úroveň výš
```

### Příkaz 4: mkdir (Make Directory)

```bash
mkdir my-new-folder
```

**Co to dělá?** Vytvoří novou složku.

### Příkaz 5: touch (Create File)

```bash
touch my-file.txt
```

**Co to dělá?** Vytvoří prázdný soubor.

### Příkaz 6: cat (Concatenate)

```bash
cat my-file.txt
```

**Co to dělá?** Vypíše obsah souboru.

### Příkaz 7: rm (Remove)

```bash
rm my-file.txt       # Smaž soubor
rmdir my-folder      # Smaž prázdnou složku
rm -rf my-folder     # Smaž složku i s obsahem (POZOR!)
```

**Co to dělá?** Smažeme věci. ⚠️ Nevratné!

### Příkaz 8: cp (Copy)

```bash
cp original.txt kopie.txt
```

**Co to dělá?** Kopíruje soubor.

### Příkaz 9: mv (Move / Rename)

```bash
mv old-name.txt new-name.txt     # Přejmenuj
mv file.txt folder/file.txt      # Přesuň do jiné složky
```

**Co to dělá?** Přesunuje nebo přejmenuje soubor.

### Příkaz 10: clear

```bash
clear
```

**Co to dělá?** Vyčistí terminál (pro přehlednost).

---

## 💻 PRAKTIKA (20 minut)

### Cvičení 1: Navigace

```bash
# Jsi v ~/Projects/data-engineer-study-2026

pwd                          # Vypiš kde jsi
ls                           # Co je tady?
cd Obsidian-Vault           # Jdi do Obsidian-Vault
pwd                          # Kde jsi teď?
ls                           # Co je v Obsidian-Vault?
cd ..                        # Jdi zpátky
pwd                          # Ověř že jsi zpátky
```

### Cvičení 2: Vytváření struktury

```bash
mkdir projects               # Vytvoř projects složku
cd projects
mkdir project-1-etl        # Vytvoř project-1-etl
mkdir project-2-cloud      # Vytvoř project-2-cloud
mkdir project-3-streaming  # Vytvoř project-3-streaming
ls                         # Ověř že všechny existují
cd ..
```

### Cvičení 3: Práce se soubory

```bash
cd projects/project-1-etl
touch main.py
touch requirements.txt
touch README.md
ls -la                     # Pokaž všechny včetně skrytých
cat README.md              # Vypíš (je prázdný)
```

### Cvičení 4: Git příkazy v terminálu

```bash
# Jsi v ~/Projects/data-engineer-study-2026

git status                 # Co se změnilo?
git add .                  # Přidej všechno na staging
git status                 # Teď je na staging
git commit -m "📁 Project structure setup"  # Commitni
git push                   # Pushni do GitHub
```

---

## ⌨️ KEYBOARD SHORTCUTS - Budeš je potřebovat

| Shortcut | Co dělá |
|----------|---------|
| Ctrl+C | Zastaví právě běžící program |
| Ctrl+L nebo `clear` | Vyčistí terminál |
| Ctrl+R | Hledej v historii příkazů |
| ↑/↓ Šipka | Procházej historii |
| Tab | Auto-complete (magické!) |
| Cmd+T (Mac) | Nový tab v terminálu |
| Ctrl+A | Skočit na začátek řádku |
| Ctrl+E | Skočit na konec řádku |

---

## ✅ CHECKLIST

- [ ] Terminal je otevřený
- [ ] Zvládneš `pwd` a víš kde jsi
- [ ] Zvládneš `ls` a víš co je v aktuální složce
- [ ] Zvládneš `cd` a můžeš se pohybovat
- [ ] Zvládneš `mkdir` a můžeš vytvářet složky
- [ ] Zvládneš `touch` a můžeš vytvářet soubory
- [ ] Zvládneš `rm` a víš jak smazat věci
- [ ] Git příkazy fungují (`git status`, `git add`, `git commit`, `git push`)
- [ ] Tab auto-complete ti funguje

---

## 🔗 PROPOJENÍ - Kam jde dál?

```
TEĎKA (Ty): 004-Terminal-Basics
├─ ✅ Terminal ovládáš

PŘÍŠTĚ:
├─ 005-VS-Code-Setup (Kde budeš psát kód?)
├─ 006-Python-Refresher-Part1 (Budeš psát Python)
└─ 007-Python-Refresher-Part2 (OOP a klasy)

VŠE BUDE SPOUŠTĚNO:
└─ Z terminálu! (python script.py, git push, atd.)
```

---

## 📝 GITHUB TASK

```bash
# Projects/project-1-etl, projects/project-2-cloud, projects/project-3-streaming

git add projects/
git commit -m "📁 Initial project directories created"
git push
```

---

## 🎓 SHRNUTÍ

Terminal je tvůj nejlepší kamarád! Pamatuj si:

1. **pwd** = Kde jsem?
2. **ls** = Co je tady?
3. **cd** = Jdu tam
4. **mkdir** = Vytvoř složku
5. **Git** = Commituj a pushuj

**Příští lekce:** VS Code setup!

---

**Máš otázky?** Perplexity: "Jaké jsou základní terminálové příkazy pro začátečníka?"
