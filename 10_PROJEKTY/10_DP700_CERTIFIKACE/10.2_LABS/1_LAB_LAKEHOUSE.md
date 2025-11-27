# 1️⃣ LAB: LAKEHOUSE

## Cíl

Vytvořit Lakehouse, načíst data, provést SQL dotazy na souborech a tabulkách.

---

## Praxe - Krok za krokem

### Krok 1: Create Lakehouse

```
1. Jdi do tvého workspace (Data Engineer Journey)
2. New item → Lakehouse
3. Name: "Sales_DW"
4. Create
```

- [ ] Lakehouse vytvořen

### Krok 2: Upload Data

```
1. Lakehouse → Files
2. Upload → Vyber CSV soubor
3. (Nebo si stáhni: https://aka.ms/fabric-sample-data)
```

- [ ] CSV nahran do Files

### Krok 3: Load to Table

```
1. Files → Pravý klik na CSV
2. Load to New Table
3. Confirm schema
```

- [ ] Tabulka vytvořena z CSV

### Krok 4: SQL Query na File

```sql
SELECT TOP 10 * FROM 'Files/sales.csv'
```

- [ ] Query spuštěn

### Krok 5: SQL Query na Table

```sql
SELECT TOP 10 * FROM Sales
```

- [ ] Query spuštěn (měl by být rychlejší než Files)

### Krok 6: Aggregation Query

```sql
SELECT 
  Category,
  SUM(Amount) as Total,
  COUNT(*) as Count
FROM Sales
GROUP BY Category
ORDER BY Total DESC
```

- [ ] Aggregace funguje

---

## Pozorování

**Files vs Tables:**
- Files query: Pravděpodobně pomalejší (bez indexů)
- Table query: Rychlejší (indexed)

**Poznámka si:**
- Jak dlouho trvala Files query?
- Jak dlouho trvala Table query?

---

## Výstup

Screenshot SQL results ✓

---

## Next: [[2_LAB_SPARK]]