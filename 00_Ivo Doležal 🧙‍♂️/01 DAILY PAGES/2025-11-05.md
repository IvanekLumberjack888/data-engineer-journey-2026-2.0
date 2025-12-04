---
date: <% tp.date.now("YYYY-MM-DD") %>
week: <%= Math.floor((new Date() - new Date(2025, 10, 1)) / (7 * 24 * 60 * 60 * 1000)) %>
type: daily
---

# Daily Note - <% tp.date.now("dddd, D. MMMM") %>

## 🎯 Dneška plánuji
- [ ] Lekce: (která čísla? 001? 002?)
- [ ] Coding: (co budeš dělat?)
- [ ] Commit: (jakou zprávu?)

## 📚 Teorie
Tady si poznamenávej co se učíš...

## 💻 Kóding
Tady si poznamenávej kód a výsledky...

## 🐛 Problémy
Tady si poznamenávej co ti nefungovalo...

## ✅ Dneška jsem zvládnul
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
