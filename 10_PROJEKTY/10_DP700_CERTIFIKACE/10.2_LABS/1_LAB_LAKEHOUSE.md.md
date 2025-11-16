# 1️⃣ LAB: LAKEHOUSE

## Co dělám

Vytvoř lakehouse, nahraj data, queryuj.

---

## Kroky

### Fáze 1: Create

Workspace → New item → Lakehouse
Name: "Sales_DW"
Create

- [ ] Hotovo

### Fáze 2: Load Data

Upload files (CSV/Parquet)
To: Tables

- [ ] Hotovo

### Fáze 3: Query

```sql
SELECT TOP 100 * FROM table_name
```

- [ ] Hotovo

---

## Co jsem zjistil

Files vs Tables:
- Files: raw
- Tables: indexed, queryable

---

## Next: [[2_LAB_SPARK.md]]

---

## 30_ZDROJE/SLOVNÍK_CZ.md

```markdown
# 📚 SLOVNÍK - EN → ČJ

| EN | CZ | Kontext |
|----|----|----|
| Aggregate | Agregovat | summarize |
| Architecture | Architektura | design |
| Authentication | Ověřování | login |
| Backfill | Zpětné naplnění | mat. view |
| Bronze | Bronze | layer 1 |
| Capacity | Kapacita | resources |
| Cluster | Shluk | Spark |

...doplňuji jak potřebuji