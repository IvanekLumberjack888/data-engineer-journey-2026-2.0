# 🖥️ WORKSPACE SETUP - Notebook + TV Rozšířená Obrazovka

**Vaše situace:** Notebook + občas TV jako rozšířená obrazovka

Tady je perfektní setup pro maximální produktivitu!

---

## 🎯 LAYOUT - NOTEBOOK SAM

### Situace: Jste jen na notebooku

**Ideální rozlišení:** 1920×1080 minimálně (Full HD)

```
┌─────────────────────────────────────────────────────────────┐
│ VS Code (Main)                    │ Browser/Perplexity   │
│                                   │                      │
│ editor.py (50%)                   │ Perplexity Pro (50%) │
│                                   │                      │
│                                   │ Tab 2: GitHub        │
│                                   │ Tab 3: Docs          │
├─────────────────────────────────────────────────────────────┤
│ Terminal (40% výšky)                                         │
│ $ python script.py                                           │
│ >> Output here                                               │
└─────────────────────────────────────────────────────────────┘
```

### Jak to nastavit v VS Code:

**Editor Layout:** Klikni View → Editor Layout → Two Columns

```bash
# Keyboard:
Cmd+\ (Mac) / Ctrl+\ (Windows) = Split editor horizontálně
Cmd+J (Mac) / Ctrl+J (Windows) = Toggle terminal
```

### Spouštění oken:

```bash
# Otevření všeho:
1. VS Code (2 sloupce)
2. Browser s Perplexity Pro (jinou aplikaci)
3. Obsidian (v background, otevři Cmd+Tab když potřebuješ)
```

**Navigace mezi aplikacemi:**
- Mac: Cmd+Tab
- Windows: Alt+Tab
- Případně: Plocha se 3-4 "workspaces" (Spaces na Mac)

---

## 📺 LAYOUT - NOTEBOOK + TV (Rozšířená obrazovka)

### Situace: Máte TV připojenou

**Ideální konfigurace:**
- **Notebook (27": studiová plocha)**
- **TV (55"+: reference & dokumentace)**

```
┌──────────────────────┐    ┌─────────────────────────────┐
│ NOTEBOOK (Hlavní)    │    │ TV (Reference & Output)     │
│                      │    │                             │
│ VS Code              │    │ Terminal                    │
│ Split editor:        │    │ (Full screen!)              │
│                      │    │                             │
│ LEFT (50%):          │    │ $ python script.py          │
│ - editor.py          │    │ Output:                     │
│ - Git terminal       │    │ >> Long output              │
│                      │    │ >> Debugging info           │
│ RIGHT (50%):         │    │                             │
│ - Obsidian Daily     │    │                             │
│ - Notes links        │    │                             │
└──────────────────────┘    └─────────────────────────────┘
```

### Jak to nastavit:

**Mac:**
```bash
# System Preferences → Displays
# Arrange tvé displeje tak jak sis je myslel
# Můžeš je "mirror" nebo "extend"
```

**Windows:**
```bash
# Settings → Display
# Arrange displays
# Scale & layout = nastavit resolution
```

**Keyboard shortcuts na Mac (s TV):**
```
Cmd+Ctrl+Right = Přepni na další screen
Cmd+Ctrl+Left = Přepni na předchozí screen
```

### Workflow s TV:

**Když codinguješ:**
```
NOTEBOOK (pracuješ):
├─ VS Code (80%)
│  └─ Python kód
├─ Terminal (20%)
│  └─ git commands

TV (sleduješ):
├─ Terminal output (80%)
│  └─ python hello.py output
├─ GitHub/Docs (20%)
│  └─ Reference co potřebuješ
```

**Když debuguješ:**
```
NOTEBOOK (dev):
├─ VS Code debugger
│  └─ Breakpoints, variables

TV (sleduješ):
├─ Console output (FULL!)
│  └─ Long output, logy, strace
```

---

## 💻 VS CODE MULTI-SCREEN SETUP

### Extension: "Display Ruler"

```bash
# Install:
# Extensions → "Display Ruler"
# Nastavení: Pravítko na 80 znaků
```

### Integrovaný Terminal Positioning

```bash
# Terminal lze umístit:
# - Dole (default)
# - Vpravo
# - Vlevo

# Cmd+J = toggle terminal dole
# Cmd+\ = split editor vpravo
```

### Ideální VS Code layout s TV:

```bash
# Klikni na ikonku terminálu vpravo dole
# → Select Default Profile: Terminal na RIGHT straně
# Pak: Cmd+\ split editor, Terminal zůstane vpravo
```

---

## 🎬 OBSIDIAN - MULTI MONITOR TIPS

### Obsidian je resource-light - ideální pro TV!

Nemáš to, ale můžeš:
1. Obsidian vlevo na notebooku (Daily notes, Learn)
2. TV vpravo (odkaz do dokumentace!)

**Workflow:**
```
NOTEBOOK (Obsidian):
├─ Daily note (Today's plan)
├─ Learn/Python.md (Reference)
├─ Klikni [[SQL-Basics]]
└─ Vidíš backlinks co souvisí

TV (Obsidian Graph View):
├─ Automaticky se otevře Graph
├─ Vidíš jak se tvé poznámky propojují
├─ Motivace! (Wow, kolik jsem se naučil!)
```

### Spuštění Obsidian Graph View na TV:

```bash
# V Obsidianu:
# Cmd+Shift+G (Mac) / Ctrl+Shift+G (Windows)
# = Otevře se Graph View
# Pak Cmd+Tab přesuň to okno na TV
```

---

## 🖥️ ERGONOMIE - Jak si nastavit notebook + TV

### Ideální pozice:

```
┌─────────────────┐
│ TV (nahoře)     │ ← Eye level nebo mírně výš
│ Vzdálenost: 1m  │
└─────────────────┘

┌─────────────────┐
│ Notebook        │ ← Eye level, 60cm
│ (na podstavci)  │
└─────────────────┘

└─────────────────┘
      Klávesnice
      Myš (Right-side!)
```

### Doporučení:

1. **Notebook na podstavci** (aby nebyl nízko)
2. **TV na stěně nahoře** (reference)
3. **Klávesnice & myš sepředu** (ne na notebooku!)
4. **Židle s opěradlem** (8 hodin studia!)

---

## 📱 SMARTPHONE BONUS

Máš i telefon? Super!

```
NOTEBOOK (Coding)
TV (Output & Docs)
SMARTPHONE (Perplexity mobile app!)
├─ Čteš artikl o data engineeringu
├─ Poznamenáš si Obsidian sync (wait, no sync!)
└─ Ne ideální, ale funguje!
```

**Perplexity Mobile App:**
```
- Instaluj z App Store
- Login se GitHub účtem
- Research módulem offline
- Screenshot + send to Obsidian/Notes
```

---

## 🎯 DENNÍ WORKFLOW - S MULTI-MONITOR

### Ráno (17:05-18:05)

```
SETUP:
1. Notebook: Obsidian Daily note otevřeno (LEFT)
2. Notebook: VS Code (RIGHT)
3. TV: Terminal (full screen)
4. Browser: Perplexity Pro (on dock)

WORKFLOW:
17:05 - Plan (Obsidian):
        Napíšeš co dělej dneska

17:15 - Study modul (Obsidian + Browser):
        Left: Obsidian Daily note
        Right: VS Code (studijní soubor otevřený)
        TV: Nic (nebo GitHub docs)

17:30 - Coding (VS Code + Terminal):
        Left: Python editor
        Right: Terminal
        TV: Pokaž output!

17:50 - Review (Git):
        Terminal: git status, git add, git commit
        TV: GitHub repo (kontrola)
```

### Sobota (09:00-17:00)

```
PROJECT SESSION:

09:15 - Project on Main Display:
        NOTEBOOK:
        ├─ VS Code (80%)
        │  ├─ Python code (main project)
        │  └─ Terminal (20%)
        │     └─ git commands
        TV:
        └─ Second terminal
           ├─ Running output
           ├─ Docker logs
           └─ Database queries

12:30 - BREAK

13:30 - Continue Coding:
        Při "застryí" na bugem:
        ├─ NOTEBOOK: Debugger v VS Code
        ├─ TV: Přepni na Obsidian Graph View
        │  └─ "Remind myself of concepts I learned"
        └─ Browser: Perplexity Pro
           └─ "Why am I getting this error?"

15:30 - Wrap-up:
        ├─ Code review (sám sebe)
        ├─ Documentation update
        ├─ Git push
        └─ LinkedIn post o pokroku
```

---

## ⚙️ APLIKACE - WINDOW MANAGEMENT

### Mac - Aplikace v "Spaces"

```bash
# Vytvoř si 3-4 workspaces:
# 1. VS Code (+ Terminal v ní)
# 2. Browser (Perplexity + GitHub + Docs)
# 3. Obsidian (denní notes)
# 4. Slack/Discord (community)

# Navigation:
Ctrl+1, Ctrl+2, Ctrl+3, Ctrl+4 = Switch workspace
Cmd+Tab = Switch aplikaci v aktuálním workspace
```

### Windows - Virtual Desktops

```bash
# Windows 10+:
Win+Tab = Task view
Win+Ctrl+Right = Next desktop
Win+Ctrl+Left = Previous desktop
Win+Ctrl+D = New desktop
```

---

## 🎮 GAMING MODE - Když máš volný čas (Odměna!)

Když si zaslužíš break (po XP reward):

```
NOTEBOOK:
└─ Close coding stuff
   ├─ Close VS Code
   ├─ Close Terminal
   └─ Open Steam / Epic Games

TV:
└─ Full screen gaming!
   ├─ Better visuals
   ├─ Bigger screen = more immersive
   └─ Enjoy! (2h reward)
```

---

## 📊 POROVNÁNÍ - LAPTOP SAM vs LAPTOP+TV

| Aspekt | Laptop sam | Laptop + TV |
|--------|-----------|------------|
| Produktivita | ⭐⭐⭐ Dobrá | ⭐⭐⭐⭐⭐ Vynikající |
| Čtení dlouhých outputů | ⭐ Malý | ⭐⭐⭐⭐⭐ Velký screen |
| Debugging | ⭐⭐ Těžké | ⭐⭐⭐⭐ Snadné |
| Reference & docs | ⭐⭐ Multi-tab | ⭐⭐⭐⭐⭐ Full screen |
| Ergonomie | ⭐⭐ Krk bolí | ⭐⭐⭐⭐⭐ Pohodlné |
| Zábava při breakech | ⭐⭐ Malý | ⭐⭐⭐⭐⭐ Cinema! |

---

## ✅ CHECKLIST - Setup

- [ ] Notebook nainstalován na podstavec
- [ ] TV přivolány k notebooku
- [ ] Kabel HDMI/USB-C propojuje notebook + TV
- [ ] Klávesnice & myš jsou připraveny
- [ ] Display settings jsou správné
- [ ] VS Code je s 2 sloupci
- [ ] Terminal je na TV
- [ ] Obsidian je v background
- [ ] Browser s Perplexity je připraven

---

## 🎓 SHRNUTÍ

S multi-monitor setupem budete:
- ✅ Psát kód vlevo (notebook)
- ✅ Vidět output vpravo (TV)
- ✅ Mít reference nahoře (Obsidian, GitHub)
- ✅ Být ergonomicky pohodlnější
- ✅ Psát rychleji a efektivněji

**Setup je klíč k produktivitě!** 🚀

---

**Máš otázky na setup?** Perplexity: "Jak si nastavit VS Code pro multi-monitor?"
