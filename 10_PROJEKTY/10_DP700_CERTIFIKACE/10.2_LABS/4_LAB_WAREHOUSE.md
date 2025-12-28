# 4️⃣ LAB: DATA WAREHOUSE

## Cíl

Vytvořit Data Warehouse. Načíst data. T-SQL queries.

---

## Praxe - Krok za krokem

### Krok 1: Create Warehouse

```
1. New item → Warehouse
2. Name: "SalesWarehouse"
3. Create
```

- [x] Warehouse vytvořen

### Krok 2: Create Table

```sql
CREATE TABLE Sales (
  SalesID INT,
  Date DATE,
  Category VARCHAR(50),
  Amount DECIMAL(10,2),
  Region VARCHAR(50)
)
```

- [x] Tabulka vytvořena

### Krok 3: Load Data

```sql
-- Option 1: COPY INTO ze souboru
COPY INTO Sales
FROM 'abfss://Files@...@fabric.dfs.core.windows.net/sales.parquet'
WITH (
  FILE_TYPE = 'PARQUET'
)
```

fabric.microsoft.com/0440f257-9783-43c3-a3b8-a30173258e32/Files/sales.csv
- [x] Data načtena

### Krok 4: Basic Query

```sql
SELECT TOP 100 * FROM Sales
```

- [x] Query spuštěn

### Krok 5: Create Index

```sql
CREATE CLUSTERED COLUMNSTORE INDEX idx_sales ON Sales
```

- [ ] Index vytvořen

### Krok 6: Query s Indexem

```sql
SELECT 
  Category,
  SUM(Amount) as Total
FROM Sales
WHERE Date > '2025-01-01'
GROUP BY Category
ORDER BY Total DESC
```

- [ ] Indexed query spuštěn (měl by být rychlý)

### Krok 7: Create View

```sql
CREATE VIEW SalesOverview AS
SELECT 
  Category,
  COUNT(*) as TransactionCount,
  SUM(Amount) as TotalSales,
  AVG(Amount) as AvgSale
FROM Sales
GROUP BY Category
```

- [ ] View vytvořen

### Krok 8: Query View

```sql
SELECT * FROM SalesOverview
```

- [ ] View query spuštěn

---

## Pozorování

- Jak se výkon změnil po vytvoření indexu?
- Jaké jsou top 3 kategorie dle prodeje?

---

## Next: [[5_LAB_EVENTSTREAM]]