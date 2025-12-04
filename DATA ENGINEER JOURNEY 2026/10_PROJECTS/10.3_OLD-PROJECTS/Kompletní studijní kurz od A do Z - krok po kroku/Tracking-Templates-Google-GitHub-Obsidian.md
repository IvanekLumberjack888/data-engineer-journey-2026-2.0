# 📊 TRACKING TEMPLATES - Praktické nástroje na monitoring pokroku

Zde jsou konkrétní šablony pro tracking vaší cesty!

---

## 📱 OPTION 1: GOOGLE SHEETS TRACKER (Nejjednodušší!)

### Jak se to nastaví:

1. Jdi na https://sheets.google.com
2. Vytvoř "Data Engineer Quest" spreadsheet
3. Zkopíruj tuhle strukturu:

### Tab 1: DAILY LOG

```
Sloupce:
A - Date
B - Quest/Modul
C - XP Earned
D - Commit Link
E - Obsidian Note
F - Notes/Comments

Řádek 1 (Header):
| Date | Quest | XP | Commit | Obsidian | Notes |
|------|-------|-----|--------|----------|-------|
| 1.11 | 001-Git | 50 | github.com/... | ✅ | SSH setup done |
| 2.11 | 001-Git | 45 | github.com/... | ✅ | First commit! |
...

Formule (v horním řádku):
- C: =SUMIF(C:C,">0") → Celkový XP
- Auto-formula pro LEVEL: =INT(C2/500)
```

### Tab 2: WEEKLY SUMMARY

```
Sloupce:
A - Week #
B - Total XP
C - Target XP
D - Modules Done
E - Projects
F - Commits
G - LinkedIn Posts
H - Status

Řádek 1:
| Week | XP | Target | Modules | Projects | Commits | Posts | Status |
|------|-----|--------|---------|----------|---------|-------|--------|
| 1 | 400 | 525 | 2/2 | - | 7 | 1 | 🟡 OK |
| 2 | 325 | 525 | 1/2 | - | 5 | 2 | 🟡 OK |
...
```

### Tab 3: LEVEL TRACKER

```
Sloupce:
A - Level
B - Name
C - XP Required
D - Current XP
E - Progress Bar
F - Status
G - Unlocked Date

| Level | Name | XP Req | Current | Progress | Status | Date |
|-------|------|--------|---------|----------|--------|------|
| 1 | Initiate | 500 | 400 | ████░░░░░ | IN PROGRESS | 1.11 |
| 2 | Apprentice | 700 | 0 | ░░░░░░░░░░ | LOCKED | - |
| 3 | Explorer | 800 | 0 | ░░░░░░░░░░ | LOCKED | - |
...
```

### Tab 4: BADGES

```
| Badge | Tier | Unlocked | Date | Points |
|-------|------|----------|------|--------|
| Git Pioneer | Bronze | ✅ | 1.11 | 10 |
| Terminal Novice | Bronze | ⏳ | - | 10 |
| Python Starter | Bronze | ⏳ | - | 10 |
| Code Committer | Bronze | ⏳ | - | 10 |
| SQL Seeker | Silver | ⏳ | - | 25 |
```

### Tab 5: MONTHLY REPORT

```
| Metric | November | December | January | February | March |
|--------|----------|----------|---------|----------|-------|
| Total XP | - | - | - | - | - |
| Level | - | - | - | - | - |
| Modules | - | - | - | - | - |
| Commits | - | - | - | - | - |
| Projects | - | - | - | - | - |
| Badges | - | - | - | - | - |
| Grade | - | - | - | - | - |
```

---

## 🎯 OPTION 2: GITHUB WIKI TRACKER (Pro Git-savvy)

Vytvoř GitHub Wiki v svém repozitáři:

### `/wiki/Quest-Log.md`

```markdown
# 🎮 Quest Log

## November 2025

### Week 1 (1-7.11)

#### Quest 001: Git & GitHub Basics
- **Status**: ✅ COMPLETED
- **Date Started**: 1.11.2025
- **Date Completed**: 3.11.2025
- **XP Earned**: 150
- **Difficulty**: ⭐ EASY
- **Commits**: 5
- **Key Learnings**:
  - SSH key setup
  - First repository created
  - Basic git commands

#### Quest 002: Obsidian Setup
- **Status**: 🔄 IN PROGRESS
- **Date Started**: 4.11.2025
- **Progress**: 60%
- **XP Earned**: 75 (of 150)
- **Key Tasks**:
  - [ ] Vault created
  - [ ] Plugins installed
  - [ ] Templates set up
  - [ ] Daily notes started

### Weekly Stats (Week 1)
- Total XP: 225 (target: 525)
- Modules: 1.5 / 2
- Commits: 5 / 7 expected
- LinkedIn posts: 1 / 1
```

### `/wiki/Level-Tracker.md`

```markdown
# 📊 Level Tracker

## Current Level: 1 (Initiate)
**XP: 225 / 500** [████░░░░░]

- [ ] Level 2 (500 XP)
- [ ] Level 3 (1,200 XP)
- [ ] Level 4 (2,000 XP)
- [ ] Level 5 (3,000 XP)
- [ ] Level 6 (4,500 XP)
- [ ] Level 7 (6,000 XP)
- [ ] Level 8 (7,500 XP)
- [ ] Level 9 (9,000 XP)
- [ ] Level 10 (10,500 XP) - FINAL GOAL!

## Level Milestones
- ⏳ Level 2 (Apprentice) - Est. 8.11.2025
- ⏳ Level 3 (Explorer) - Est. 22.11.2025
- ⏳ Level 5 (Data Architect) - Est. 20.12.2025
- ⏳ Level 10 (Data Engineer) - Est. 31.3.2026 🏆
```

### `/wiki/Badges.md`

```markdown
# 🏆 Badges Unlocked

## ✅ TIER 1: FUNDAMENTY

- 🔴 **Git Pioneer** (1.11.2025)
  - First repository created
  - XP: 10
  
- ⏳ **Terminal Novice** (Coming soon)
- ⏳ **Python Starter** (Coming soon)
- ⏳ **Obsidian Scholar** (Coming soon)

## ⏳ TIER 2: PROGRAMOVÁNÍ

- ⏳ **SQL Seeker**
- ⏳ **Python Developer**
- ⏳ **DBeaver Explorer**
- ⏳ **Code Committer** (50 commits)

## ⏳ TIER 3: DATA ENGINEERING

- ⏳ **Modeler Novice**
- ⏳ **Cloud Traveler**
- ⏳ **ETL Builder**
- ⏳ **Data Architect**

## ⏳ TIER 4: EXPERT

- ⏳ **Streaming Master**
- ⏳ **BI Expert**
- ⏳ **Portfolio Builder**
- ⏳ **Interview Ready**

## ⏳ TIER 5: LEGENDARY

- ⏳ **GitHub Legend** (300+ commits)
- ⏳ **LinkedIn Influencer** (50+ connections)
- ⏳ **Job Ready** (HIRED! 🎉)

**Total Badges Earned: 1 / 30**
```

---

## 🗂️ OPTION 3: OBSIDIAN DASHBOARD (Pro Obsidian Users)

### Soubor: `Dashboard/Progress-Dashboard.md`

```markdown
---
tags: dashboard
---

# 📊 Progress Dashboard

## 🎮 Current Status

**Level:** 1 (Initiate)
**XP:** 225 / 500 [████░░░░░] 45%
**Target Level Up:** 14. listopadu 2025
**Days Elapsed:** 0
**Days Remaining:** 161

## 📋 Today's Quest

**Quest:** [[001-Git-GitHub-Basics]]
**Progress:** 60% (Task 2 of 3)
**Time Spent:** 45 min / 90 min
**XP Today:** 35 / 75
**Next Task:** SSH key setup

## ✅ Daily Checklist

- [x] Daily login (5 XP)
- [x] Read lesson (10 XP)
- [x] Practice exercise (15 XP)
- [ ] Git commit (5 XP)
- [ ] Obsidian note (5 XP)
- [ ] Perplexity question (10 XP)
- [ ] LinkedIn post (20 XP)

**Daily Progress: 45/75 XP** ⏳

## 📊 This Week

**Week 1: 1-7 November**

| Day | Quest | XP | Commits | Status |
|-----|-------|----|---------|----|
| Mon | 001 Pt.1 | 50 | 2 | ✅ |
| Tue | 001 Pt.2 | 45 | 1 | 🔄 |
| Wed | 002 Pt.1 | 0 | 0 | ⏳ |
| Thu | 002 Pt.2 | 0 | 0 | ⏳ |
| Fri | 002 Pt.3 | 0 | 0 | ⏳ |
| Sat | Mini-project | 0 | 0 | ⏳ |
| Sun | Weekly review | 0 | 0 | ⏳ |

**Week XP: 95 / 525** [████░░░░░]
**Week Commits: 3 / 7**

## 🏆 Recent Badges

- ✅ Git Pioneer (1.11.2025)

## 📈 Monthly Progress

[[202511-Monthly-Report]]

## 🎯 Upcoming Quests

1. [[002-Obsidian-Setup]] - Next
2. [[003-Python-Setup]] - Week 2
3. [[004-Terminal-Basics]] - Week 2

## 💡 Quick Links

- [[000-INDEX-Studialni-Plán]]
- [[Daily/2025-11-01]]
- [[Learn/001-Git-GitHub]]
- [[Projects/Project-1-ETL]]

---

*Last Updated: 1. listopadu 2025, 18:30 CET*
*Next Review: 8. listopadu 2025*
```

---

## 📝 OPTION 4: NOTION DATABASE TRACKER (Pro Notion Users)

```
Database: Data Engineer Quests

Properties:
- Name (Title)
- Quest # (Number)
- Status (Select: Not Started, In Progress, Completed)
- XP (Number)
- Week (Number)
- Difficulty (Select: ⭐, ⭐⭐, ⭐⭐⭐, ⭐⭐⭐⭐)
- Completed Date (Date)
- Commits (Rollup: Count related commits)
- Notes (Text)

Views:
- By Status (kanban: Not Started, In Progress, Done)
- By Week (table: groupby week)
- By Difficulty (gallery)
- Calendar (timeline of completions)
- Timeline (Gantt-like)
```

---

## 📱 DAILY ROUTINE - KONKRÉTNÍ CHECKLIST

### Každý den - 5-10 minut na tracking:

```
RÁNO (před studiem):
1. [ ] Otevřu spreadsheet / GitHub Wiki / Obsidian
2. [ ] Zaznamenám dnešní quest
3. [ ] Nastavím si cíl: 75 XP dneska
4. [ ] Check streak (je mi motivace!)

BĚHEM DŘE:
5. [ ] Po každém cvičení: +XP do trackeru
6. [ ] Po commitu: Link do tracker
7. [ ] Po Obsidian note: ✅ mark

VEČER (5-10 min wrap-up):
8. [ ] Sumíruju všechny XP za den
9. [ ] Update progress bar
10. [ ] Check: K dalšímu levelu?
11. [ ] Prep zítřejší quest
```

---

## 🎯 WEEKLY REVIEW TEMPLATE

Každou neděli si sednout na 30 minut:

```markdown
# Weekly Review - Týden 1 (1-7.11.2025)

## 📊 Stats
- **Total XP Earned**: 325 (Target: 525)
- **Level Progress**: 325/500 (65%)
- **Modules Completed**: 1.5 / 2
- **Git Commits**: 7 / 7 ✅
- **LinkedIn Posts**: 2 / 1 🎉
- **Badges Unlocked**: 1
- **Streak**: 7 days 🔥

## ✅ Accomplishments
- [ ] Quest 001 completed!
- [ ] GitHub repo created
- [ ] SSH keys configured
- [ ] First 7 commits
- [ ] Obsidian vault started

## ⚠️ Challenges
- Learning curve steeper than expected
- Need more sleep (3 am coding!)
- SSH setup took 2 hours (but learned a lot)

## 🎯 Next Week Goals
- [ ] Finish Quest 002 (Obsidian)
- [ ] Start Quest 003 (Python setup)
- [ ] 4+ LinkedIn posts
- [ ] Maintain 7-day streak
- [ ] Target: 525+ XP

## 📈 Progress Trend
Week 1: 325 XP (62%)
Next: 525+ XP (target for week 2)

## 💭 Notes & Reflections
- Git is easier than I thought
- Obsidian is a game changer for notes
- Need to speed up daily routine
- Feeling motivated! 🚀

---
*Review Date: 7.11.2025*
*Next Review: 14.11.2025*
```

---

## 🏅 MONTHLY REPORT TEMPLATE

Konec měsíce - kompletní analýza:

```markdown
# MONTHLY REPORT - LISTOPADU 2025

## 📊 Key Metrics

| Metric | Target | Actual | Status |
|--------|--------|--------|--------|
| Total XP | 2,275 | 2,100 | ⚠️ -3% |
| Modules Done | 5 | 5 | ✅ 100% |
| Projects Started | 1 | 0 | ⚠️ 0% |
| Commits | 150 | 140 | ⚠️ -7% |
| LinkedIn Posts | 8 | 7 | ⚠️ -1 |
| Badges | 5 | 4 | ⚠️ -1 |
| Streak Days | 30 | 28 | ⚠️ -2 |

## 📈 Performance Grade: B+ (Good progress!)

## 🏆 Highlights
- ✅ 5 modules completed (on target!)
- ✅ 140 commits (healthy streak)
- ✅ 4 badges earned
- ✅ Consistent daily studying
- ✅ Great GitHub contribution graph

## ⚠️ Areas for Improvement
- Project 1 should have started already
- Skipped 2 days mid-month
- Need to push more for XP
- LinkedIn posts slacking

## 📋 Lessons Learned
1. Terminal is powerful but need more practice
2. Obsidian setup took longer than expected
3. Git is becoming second nature
4. Need to plan projects better

## 🎯 December Adjustments
- START PROJECT 1 ASAP!
- Daily routine needs optimization
- Push for 550+ XP per week
- Don't skip days!

## 💪 Motivation Level: 8/10
- Feeling good about progress
- GitHub looks impressive
- Can see the skills building

## 📅 Next Month Plan
- Finish Python & SQL
- Complete Project 1
- Maintain streak
- 2,500+ XP target

---
*Month: LISTOPADU 2025*
*Report Date: 30.11.2025*
*Next Report: 31.12.2025*
```

---

## 🎮 GAMIFICATION STREAKS

### GitHub Contribution Streak

```
Cíl: 161 CONSECUTIVE DAYS!

Týden 1: 7/7 🔥 PERFECT WEEK!
Týden 2: 6/7 (pondělí off, ale OK)
Týden 3: 7/7 🔥 BACK ON TRACK!

Longest Streak: 14 days so far!
Current Streak: 3 days
Goal: 161 days (UNBROKEN!)

Streak Bonus:
- 7 days: 100 XP
- 14 days: 150 XP
- 30 days: 300 XP
- 60 days: 500 XP
- 161 days: 1000 XP + PLATINUM BADGE!
```

---

## 📊 VISUALIZATION - Jak to vypadá

```
Vaše dashboard by měl vypadat nějak takto:

╔════════════════════════════════════════════╗
║  📊 DATA ENGINEER QUEST - TRACKING         ║
╠════════════════════════════════════════════╣
║                                            ║
║ Level: 1 (Initiate)                       ║
║ XP: 225 / 500 [████░░░░░] 45%             ║
║ Streak: 🔥 7 dní                          ║
║                                            ║
║ WEEKLY STATS:                              ║
║ ├─ XP: 325 (target: 525)                  ║
║ ├─ Commits: 7 / 7 ✅                      ║
║ ├─ Modules: 1.5 / 2                       ║
║ └─ Posts: 2 / 1 🎉                        ║
║                                            ║
║ CURRENT QUEST:                             ║
║ 002-Obsidian-Setup [██░░░░░░░] 20%        ║
║                                            ║
║ BADGES: 🔴 Git Pioneer                    ║
║                                            ║
║ NEXT LEVEL: 14.11.2025                    ║
║                                            ║
╚════════════════════════════════════════════╝
```

---

## 🚀 FINAL WORDS

**Máte 4 opcí - vyberte si kterou se vám líbí:**

1. **Google Sheets** - Nejjednoduché, ale efektivní
2. **GitHub Wiki** - Pro Git-savvy programátory
3. **Obsidian** - Pokud už máte Obsidian setup
4. **Notion** - Pokud máte rád fancy databáze

**DOPORUČUJI**: Google Sheets (nejrychlejší start) + Obsidian Daily notes (pro learning)

---

**TEĎKA: VYBERTE SI JEDEN NÁSTROJ A ZAČNĚTE!**

**Nemusíte být perfect. Musíte být CONSISTENT! 💪🚀**

---

*Vygenerováno: 1. listopadu 2025*
*Poslední aktualizace: Teď!*
*Příští aktualizace: 8. listopadu (Weekly Review)*
