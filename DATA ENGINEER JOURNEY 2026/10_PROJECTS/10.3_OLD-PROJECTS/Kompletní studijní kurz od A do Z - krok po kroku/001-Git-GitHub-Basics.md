# 🔴 MODUL 001: Git & GitHub - Absolutní základy

**⏱️ Doba: 60-90 minut | Schwízkost: ⭐ Nula | Předchází: Nic | Pokračuje: 002, 003, 004**

---

## 🤔 PROČ TO POTŘEBUJEŠ?

Git a GitHub jsou jako **verze kontrola pro tvůj kód**. Představ si:

- Píšeš Python script
- Něco ses zlomíš
- Chceš se vrátit k staré verzi
- V Excelu bys měl "script_v1.py", "script_v2.py", "script_v2_final.py", "script_v2_final_REAL.py"
- V Gitu máš **jednu verzi**, ale vidíš všechny staré verze v historii

**GitHub** = cloudové úložiště pro Git + sociální síť programátorů + tvoje portfolio! 

Firmy ti řeknou: "Pošli GitHub link" → oni tam vidí tvoje projekty → JOBS!

---

## 🎯 CO SE DNESKA NAUČÍŠ

```
✓ Co je Git? (local, na tvém notebooku)
✓ Co je GitHub? (cloud, na internetu)
✓ Jak je propojit?
✓ Tvůj první commit!
✓ Daily workflow s Gitem
```

---

## 📚 TEORIE (15 minut)

### Git = Verze kontorla
```
Představ si:
├── Script v1 (1.11.2025 16:00)
├── Script v2 (1.11.2025 16:30)
│   └── Změnil jsem funkci XY
├── Script v3 (1.11.2025 17:00)
│   └── Opravil jsem bug
└── Script v4 (1.11.2025 17:30) ← TEĎKA
    └── Přidal jsem novou feature

Git ti pamatuje všechny verze + kdo co změnil + KDY + PROČ
```

### GitHub = Cloud + Portfolio
```
GitHub = společnost vlastněná Microsoftem
Jejich slogan: "The home for all developers"

Pro tebe znamená:
- Tvoje kód je v cloudu (pokud tvůj notebook shoří, máš backup!)
- Recruiteři vidí tvoje projekty
- Můžeš se s ostatními collaborovat
```

### Terminologie (zapamatuj si to!)

| Termín | Vysvětlení |
|--------|-----------|
| **Repository (repo)** | Složka s tvým projektem + Git historii |
| **Commit** | "Snapshot" tvého kódu - "Mám hotový feature X" |
| **Branch** | Paralelní verze kódu (např. "develop" vs "production") |
| **Push** | Poslání tvého kódu z notebooku do cloudu (GitHub) |
| **Pull** | Stažení kódu z cloudu do notebooku |
| **Merge** | Spojení dvou branchí dohromady |

---

## 🛠️ INSTALACE (15 minut)

### Krok 1: Zjisti, zda máš Git instalovaný

Otevři **Terminal** (Mac/Linux) nebo **PowerShell** (Windows):

```bash
git --version
```

**Výstup:**
```
git version 2.39.0 (nebo nějaká verze)
```

**Pokud to nefunguje:**

- **Mac**: 
  ```bash
  brew install git
  ```
  (Pokud nemáš Brew: `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`)

- **Windows**: Stáhni z https://git-scm.com/download/win

- **Linux**:
  ```bash
  sudo apt-get install git
  ```

### Krok 2: Nastav Git s tvým jménem a emailem

Git chce vědět KDO dělá commity. Vyplň to jednou:

```bash
git config --global user.name "Ivo Dolezal"
git config --global user.email "ivo@example.com"
```

Ověř, že to funguje:

```bash
git config --global user.name
git config --global user.email
```

### Krok 3: Vytvoř GitHub účet

Jdi na https://github.com a zaregistruj se:
- Username: **ivodolezal** (nebo tvoje varianta)
- Email: Tvůj email
- Password: Silné!

### Krok 4: Připoj GitHub ke Git (SSH klíče)

To je trochu složitější, ale je to jednodesítka:

```bash
# Generuj SSH klíč
ssh-keygen -t ed25519 -C "ivo@example.com"

# Prostě stiskni ENTER 3x (žádné heslo)
```

Výstup bude:
```
Your identification has been saved in ~/.ssh/id_ed25519
```

Teď zkopíruj veřejný klíč:

```bash
# Mac/Linux:
cat ~/.ssh/id_ed25519.pub | pbcopy

# Windows (PowerShell):
Get-Content ~/.ssh/id_ed25519.pub | Set-Clipboard
```

Jdi na GitHub:
1. Settings (klikni na fotku vpravo nahoře)
2. SSH and GPG keys
3. New SSH key
4. Vlepte klíč (Ctrl+V)
5. Add SSH key

**TEST:** V terminálu:
```bash
ssh -T git@github.com
```

Měl bys dostat:
```
Hi ivodolezal! You've successfully authenticated, but GitHub does not provide shell access.
```

---

## 💻 PRAKTIKA (30 minut)

### Cvičení 1: Tvůj první Git repo

**Cíl**: Vytvořit local repo, udělat commit, a pushnout do GitHub.

#### Krok 1: Vytvoř složku

```bash
cd ~/Projects
mkdir data-engineer-study-2026
cd data-engineer-study-2026
```

#### Krok 2: Inicializuj Git

```bash
git init
```

Výstup:
```
Initialized empty Git repository in /Users/ivo/Projects/data-engineer-study-2026/.git
```

**Co se stalo?** Git vytvoří hidden složku `.git` - tam jsou všechny verze tvého kódu!

#### Krok 3: Vytvoř první soubor

```bash
echo "# Data Engineer Study 2026" > README.md
```

#### Krok 4: Podívej se, co je "unstaged" (necommitnuté)

```bash
git status
```

Výstup:
```
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        README.md
```

**Interpretace**: Git vidí `README.md`, ale "neví", zda ho chceš commitnout.

#### Krok 5: Přidej soubor do staging area (stage)

```bash
git add README.md
```

Nebo všechny soubory najednou:

```bash
git add .
```

#### Krok 6: Podívej se na staged changes

```bash
git status
```

Výstup by měl teď říci:
```
Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   README.md
```

#### Krok 7: Commit!

```bash
git commit -m "🚀 Initial setup - starting data engineering journey"
```

Výstup:
```
[master (root-commit) abc1234] 🚀 Initial setup - starting data engineering journey
 1 file changed, 1 insertion(+)
 create mode 100644 README.md
```

**Co se stalo?** Git uložil "snapshot" tvého kódu!

### Cvičení 2: Pushni do GitHub

#### Krok 1: Vytvoř repo na GitHub

Jdi na https://github.com/new a vytvoř repo:
- **Repository name**: data-engineer-study-2026
- **Description**: My data engineering learning journey (optional)
- **Public** (aby recruiteři viděli!)
- Neklikej "Initialize with README" - již ho máš!

#### Krok 2: Propoj local repo s GitHub

GitHub ti dá příkaz něco jako:

```bash
git branch -M main
git remote add origin git@github.com:ivodolezal/data-engineer-study-2026.git
git push -u origin main
```

Prostě to zkopíruj a spusť v terminálu!

#### Krok 3: Ověř, že to je v GitHub

Jdi na https://github.com/ivodolezal/data-engineer-study-2026 - měl bys vidět tvůj README.md!

---

## ✅ CHECKLIST - Co máš zvlédnout

- [ ] Git je nainstalovaný (`git --version` funguje)
- [ ] Má nastavené tvoje jméno a email (`git config --global user.name` vrací tvoje jméno)
- [ ] Máš GitHub účet
- [ ] SSH klíče jsou nastavené (`ssh -T git@github.com` funguje)
- [ ] Máš local repo ve `~/Projects/data-engineer-study-2026`
- [ ] Máš GitHub repo na https://github.com/ivodolezal/data-engineer-study-2026
- [ ] Local repo je propojen s GitHub (`git remote -v` ukazuje `origin`)
- [ ] Máš first commit (`git log` ukazuje tvůj commit)

---

## 🔗 PROPOJENÍ - Kam jde dál?

```
┌─ TEĎKA (TY): 001-Git-GitHub-Basics
│
├─→ PŘÍŠTĚ (Další lekce):
│   ├─ 002-Obsidian-Setup
│   │   (Kde budeš psát poznámky?)
│   ├─ 003-Python-Setup
│   │   (Jak se připravit na Python coding)
│   └─ 004-Terminal-Basics
│       (Jak se hýbat v příkazové řádce)
│
└─→ BUDOUCÍ ZÁVISLOSTI:
    └─ Všechny ostatní moduly
       (006-020 – všechno je na Gitu!)
```

**Proč to nechybělo dřív?** Protože Git je ZÁKLAD. Než budeš dělat cokoliv, musíš Git zvlédnout!

---

## 📝 GITHUB TASK - Tvůj dnešní commit

Teď máš **jeden** konkrétní úkol:

```bash
# Opakuj kroky z Cvičení 1 & 2 výše!
# Na konci by měls mít:
# 1. Local repo: ~/Projects/data-engineer-study-2026
# 2. GitHub repo: https://github.com/ivodolezal/data-engineer-study-2026
# 3. First commit: "🚀 Initial setup - starting data engineering journey"
```

---

## 📓 OBSIDIAN LINK - Kam zapsat poznámky

V Obsidianu vytvoř soubor:

```
Data Engineer Study 2026/Learn/Git-GitHub.md
```

Obsah:
```markdown
# Git & GitHub

## Klíčové koncepty
- Git = local verze kontrola
- GitHub = cloud verze kontrola
- SSH klíče = autentifikace

## Příkazy co jsem se naučil
- `git init` = start Git repo
- `git add .` = stage files
- `git commit -m "..."` = snapshot
- `git push` = poslat do GitHub

## Moje GitHub URL
https://github.com/ivodolezal/data-engineer-study-2026

## Poznámky
- SSH setup byla největší část
- Zatím super!
```

Pak v Daily note (2025-11-01.md) přidej:

```markdown
## Dnešní lekce
[[Git-GitHub]] ✅ Hotovo!
- First commit na GitHub
- SSH klíče nastaveny
```

---

## 🎓 SHRNUTÍ

**Dneska jsi se naučil:**
- ✅ Co je Git a proč ho potřebuješ
- ✅ Co je GitHub a proč je důležitý
- ✅ Jak nainstalovat Git
- ✅ Jak nastavit GitHub
- ✅ Jak dělat commits a pushovat

**Hodnota:** Toto je ZÁKLAD všeho! 99% v IT používá Git!

**Příští lekce:** Teď můžeš jít na 002-Obsidian-Setup nebo 003-Python-Setup!

---

**Máš otázky?** Perplexity Pro: "Vysvětli mi co je Git commit a proč ho potřebuji"

**Máš problém?** Běžná řešení:
- `Permission denied (publickey)` → SSH klíče nejsou správně nastavené, opakuj Krok 4
- `fatal: destination path already exists` → repo již existuje, smaž `.git` složku a zkus znovu
