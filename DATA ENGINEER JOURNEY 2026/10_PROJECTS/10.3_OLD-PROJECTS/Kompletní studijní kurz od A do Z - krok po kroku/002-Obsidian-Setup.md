# 🟠 MODUL 002: Obsidian Vault Setup - Tvůj druhý mozek

**⏱️ Doba: 45-60 minut | Schwízkost: ⭐ Lehká | Předchází: 001 | Pokračuje: Všechny ostatní**

---

## 🤔 PROČ TO POTŘEBUJEŠ?

Obsidian = **tvůj druhý mozek** kde:

- Zapisuješ si co se učíš
- Propojuješ koncepty (A souvisí s B, B souvisí s C)
- Vyhledáváš staré poznámky
- Máš je na notebooku (OFFLINE! bez internetu)
- Všechno je v **plain text** souborech (GitHub-friendly)

**Vs. OneNote/Notion:**
- OneNote/Notion = cloud (bez internetu = nic)
- Obsidian = tvůj disk (offline = veškeré poznámky dostupné)
- Obsidian = propojovatelné ("backlinks" - poznámky se odkazují na sebe)

**Proč Obsidian?**
- Pracuješ s notebookem + TV = offline skvělý
- Vše je v Markdown (stejný format jako GitHub README!)
- Nula vendor lock-in (je to jenom soubory na disku)

---

## 🎯 CO SE DNESKA NAUČÍŠ

```
✓ Obsidian instalace
✓ Vault struktura (složky pro ADHD mozek)
✓ Plugins: Daily Notes, Templater, Dataview
✓ Denní template (otevřeš, máš automaticky strukturu)
✓ Propojení s Git (vault v Gitu!)
```

---

## 🛠️ INSTALACE (10 minut)

### Krok 1: Stáhni Obsidian

Jdi na https://obsidian.md a stáhni pro Mac/Windows/Linux.

Spusť a instaluj (standardní postup).

### Krok 2: Vytvoř Vault

Obsidian se ptá "Kde chceš svůj vault?" (= složka s poznámkami).

```
Příklad cesty:
/Users/ivo/Projects/Data Engineer Study 2026/Obsidian-Vault

NEBO

C:\Users\ivo\Projects\Data Engineer Study 2026\Obsidian-Vault
```

**Klik: Create new vault**
- Jméno: `Data Engineer Study 2026`
- Cesta: Vytvoř si ji v `~/Projects/`

---

## 📁 STRUKTURA (5 minut)

Vytvoř tuhle strukturu složek v Obsidianu:

```
Obsidian-Vault/
├── Daily/                (Každý den tady je tvůj záznam)
├── Learn/                (Teorias o technologiích)
├── Projects/             (Info o tvých 3 projektech)
├── Docs/                 (Dokumentace, čemuž jsi se naučil)
├── Templates/            (Šablony - nové soubory se budou kopírovat odtud)
└── _Sidebar.md           (Povinné - index)
```

Jak to udělat v Obsidianu:
1. Klikni "New folder" (levý panel)
2. Zadej jméno
3. Opakuj 6x

---

## 🔧 PLUGINS - Instalace (15 minut)

Plugins = rozšíření Obsidianu. Potřebuješ jen 3!

### Krok 1: Otevři plugin store

Settings (levo dole, ikona ozubeného kola) → Community Plugins → Browse

### Krok 2: Instaluj "Daily Notes"

- Hledej "Daily Notes"
- Klikni "Install"
- Klikni "Enable"

**Nastavení:**
- Settings → Daily notes
- Date format: `YYYY-MM-DD`
- Template location: `Templates/Daily-Note.md`

### Krok 3: Instaluj "Templater"

- Hledej "Templater"
- Klikni "Install"
- Klikni "Enable"

**Nastavení:**
- Settings → Templater → "Enable system command"
- Nic jiného se neměnit nemusí!

### Krok 4: Instaluj "Dataview"

- Hledej "Dataview"
- Klikni "Install"
- Klikni "Enable"

Dataview ti dá superschopnost: Můžeš psát dotazy na své poznámky!

```
Příklad (zjistí všechny soubory s #learning tag):
```dataview
LIST
FROM #learning
```

Teď máš tři nejdůležitější pluginy! 🎉

---

## 📝 TEMPLATES - Vytvoř teplátky (20 minut)

Templates = Když vytvoříš nový soubor, automaticky se zkopíruje šablona.

### Template 1: Daily Note

Vytvoř soubor: `Templates/Daily-Note.md`

```markdown
---
date: <% tp.date.now("YYYY-MM-DD") %>
week: <%= Math.floor((new Date() - new Date(2025, 10, 1)) / (7 * 24 * 60 * 60 * 1000)) %>
type: daily
---

# Daily Note - <% tp.date.now("dddd, D. MMMM") %>

## 🎯 Dneška plánujem
- [ ] Lekce: (která čísla? 001? 002?)
- [ ] Coding: (co budeš dělat?)
- [ ] Commit: (jakou zprávu?)

## 📚 Teorie
Tady si poznamenávej co se učíš...

## 💻 Kóding
Tady si poznamenávej kód a výsledky...

## 🐛 Problémy
Tady si poznamenávej co ti nefungovalo...

## ✅ Dneška jsem zvlédnul
- Bod 1
- Bod 2

## 🔗 Propojené poznámky
[[Learn/Git-GitHub]]
[[Projects/Project-1]]
[[Docs/Glossary]]

## 📊 XP dneska
- Daily: 5 XP
- Tasks: ?? XP
- Projects: ?? XP
- **TOTAL: ?? XP**

---
*Zapsal jsem si to: [TIME] | Poslední update: <% tp.date.now("YYYY-MM-DD HH:mm") %>*
```

### Template 2: Learning Note

Vytvoř soubor: `Templates/Learn-Note.md`

```markdown
---
type: learning
tag: #learning
date-created: <% tp.date.now("YYYY-MM-DD") %>
---

# Lekce: <% tp.file.title %>

## Proč to potřebuji?
(Vysvětlení z modulu)

## Klíčové koncepty
- Koncept 1
- Koncept 2
- Koncept 3

## Princip a návaznosti
Jak to souvisí s ostatním?

## Příklady
```python
# Kód nebo příkład
```

## Kontrola - Co jsem se naučil?
- [ ] Rozumím základům
- [ ] Zvládnu praktiku
- [ ] Mohu to vysvětlit někomu jinému

## Další zdroje
- [[Modul-002-kapcsolat]]
- [[Modul-003-reference]]

## Poznámky pro budoucnost
Co si pamatovat?
```

### Template 3: Project Note

Vytvoř soubor: `Templates/Project-Note.md`

```markdown
---
type: project
status: 🔴 not-started
date-started: <% tp.date.now("YYYY-MM-DD") %>
---

# Projekt: <% tp.file.title %>

## Cíl (jednou větou)
Co projekt dělá?

## Tech Stack
- Programovací jazyk: Python
- Cloud: GCP
- Nástroje: Airflow, dbt, BigQuery

## Fáze
- [ ] Fáze 1: Plánování
- [ ] Fáze 2: Setup
- [ ] Fáze 3: Development
- [ ] Fáze 4: Testing
- [ ] Fáze 5: Documentation

## GitHub Repo
[Link do repo](https://github.com/ivodolezal/...)

## Learning outcomes
- [[Learn/Python]]
- [[Learn/SQL]]
- [[Learn/Airflow]]

## Progress
- % done: 0%
- Last update: <% tp.date.now("YYYY-MM-DD") %>

## Next steps
Cos dělat příště?
```

---

## 📓 DAILY WORKFLOW - Jak to používat v praxi

### Každý den (60-90 minut studia)

```
17:05 - Otevřeš Obsidian
        Stiskneš: Cmd+Shift+D (Daily note)
        
        AUTOMATICKY se vytvoří: Daily/2025-11-01.md
        s tvou šablonou! (datum, čas, struktura)

17:10 - Napíšeš plán na dneska:
        - [ ] Lekce 006 - Python part 1
        - [ ] Cvičení: Funkce
        - [ ] Commit do GitHub

17:15 - Začneš studovat Modul 006...
        Kopíruješ si poznámky sem

18:00 - Wrap-up:
        Doplníš co jsi zvlédnul
        Počítáš XP
        Commituje do Git

18:05 - Close Obsidian
```

### Propojování poznámek (POWER FEATURE!)

Když napíšeš v Daily note:

```
Dneska jsem se učil [[Learn/Python-Basics]]
```

Obsidian automaticky vytvoří link! Klikni na něj → jdš na Learn/Python-Basics.md

Taky se tam vytvoří "backlink" - Learn/Python-Basics.md bude vidět, že se na něj odkazuješ z Daily note!

**Proč je to cool?**
- Vidíš propojení mezi věcmi
- Vyhledáváš rychleji
- Mozek více pochopí struktura

---

## 🔗 PROPOJENÍ S GITEM

Tvůj Obsidian vault bude v Gitu!

Soubory v Obsidianu jsou `.md` (Markdown) - to je **přesně to, co GitHub miluje**!

```
~/Projects/data-engineer-study-2026/
├── .git/ (skrytá složka s Git historií)
├── Obsidian-Vault/
│   ├── Daily/
│   ├── Learn/
│   ├── Projects/
│   └── ...
├── projects/ (tvoje Python/SQL kód)
└── README.md
```

**Workflow:**
1. Napíšeš v Obsidianu poznámku
2. Auto-save (Obsidian to dělá sám)
3. Pushneš do Git: `git add . && git commit -m "📝 Learning notes"`

**To znamená:**
- Tvoje poznámky jsou v cloudu (GitHub)
- Recruiteři vidí jak se učíš ("Look, 50 learning notes!")
- Máš backup (pokud notebook shoří)

---

## ✅ CHECKLIST

- [ ] Obsidian je nainstalován
- [ ] Vault je vytvořen v `~/Projects/`
- [ ] Složky jsou vytvořené (Daily, Learn, Projects, Docs, Templates)
- [ ] Plugin: Daily Notes je instalovaný
- [ ] Plugin: Templater je instalovaný
- [ ] Plugin: Dataview je instalovaný
- [ ] Templates jsou vytvořené (Daily-Note.md, Learn-Note.md, Project-Note.md)
- [ ] Jsi schopen otevřít Daily note (Cmd/Ctrl+Shift+D)
- [ ] Vault je v Gitu

---

## 🔗 PROPOJENÍ - Kam jde dál?

```
TEĎKA (Ty): 002-Obsidian-Setup
├─ ✅ Obsidian je tvoj druhý mozek
├─ ✅ Každý den si budeš zapisovat

PŘÍŠTĚ:
├─ 003-Python-Setup (Jak si nastavit Python?)
├─ 004-Terminal-Basics (Jak se pohybovat v terminálu?)
└─ 005-VS-Code-Setup (Kde budeš psát kód?)

VŠE BUDE ZAZNAMENÁNO:
└─ Daily notes + Obsidian propojení
```

---

## 📝 GITHUB TASK

```bash
# Tvůj Obsidian vault už má .git
# Pushni to do GitHub!

git add .
git commit -m "📝 Obsidian setup - templates a struktura"
git push
```

Na GitHub by teď měly být vidět:
```
data-engineer-study-2026/
├── Obsidian-Vault/
│   ├── Daily/
│   ├── Learn/
│   ├── Projects/
│   ├── Docs/
│   ├── Templates/
│   │   ├── Daily-Note.md
│   │   ├── Learn-Note.md
│   │   └── Project-Note.md
└── README.md
```

---

## 🎓 SHRNUTÍ

Obsidian je tvůj partner v studiu. Každý den:
1. Otevřeš Daily note (automagicky se vytvoří)
2. Poznamenáš si plán
3. Studieš modul
4. Zapíšeš si poznámky
5. Linkuješ na Learn/ a Project/ soubory
6. Počítáš XP
7. Commitneš do Git

**Příští lekce:** Terminal basics (04) nebo Python setup (03)?

---

**Máš otázky?** Perplexity: "Jak se propojují poznámky v Obsidianu?"
