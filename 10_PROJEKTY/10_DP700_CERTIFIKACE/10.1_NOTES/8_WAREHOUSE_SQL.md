# 8️⃣ WAREHOUSE & SQL

**Cíl:** T-SQL a Data Warehouse specific operations

---

## 📖 TEORIE

### Data Warehouse vs Lakehouse

| Aspekt | Warehouse | Lakehouse |
|--------|-----------|-----------|
| Schema | Fixed | Flexible |
| Query | SQL only | SQL + Spark |
| Format | Proprietary | Delta Lake |
| Optimization | Columnstore | Flexible |

### T-SQL Basics

**DDL (Define):**
```sql
CREATE TABLE Sales (ID INT, Amount DECIMAL(10,2))
ALTER TABLE Sales ADD COLUMN Region VARCHAR(50)
DROP TABLE Sales
```

**DML (Manipulate):**
```sql
INSERT INTO Sales VALUES (1, 100.50)
UPDATE Sales SET Amount = 200 WHERE ID = 1
DELETE FROM Sales WHERE ID = 1
```

**DQL (Query):**
```sql
SELECT * FROM Sales WHERE Amount > 100
```

### Indexes & Performance

**Clustered Index:**
- Određuje physical row order
- Jedan po tablici
- Usually na PRIMARY KEY

```sql
CREATE CLUSTERED INDEX idx_id ON Sales(ID)
```

**Non-clustered Index:**
- Separate structure
- Više mogućih
- Za česte WHERE/JOIN kolone

```sql
CREATE NONCLUSTERED INDEX idx_region ON Sales(Region)
```

**Columnstore Index:**
- Za analitiku
- Kompresija
- Brže za agregacije

```sql
CREATE CLUSTERED COLUMNSTORE INDEX idx_ccs ON Sales
```

### Views

Saved queries kao virtual tables.

```sql
CREATE VIEW SalesView AS
SELECT Category, SUM(Amount) as Total
FROM Sales
GROUP BY Category
```

### Stored Procedures

Reusable SQL code.

```sql
CREATE PROCEDURE usp_GetSalesByRegion @region VARCHAR(50)
AS
BEGIN
  SELECT * FROM Sales WHERE Region = @region
END

EXEC usp_GetSalesByRegion 'North'
```

---

## 🛠️ PRAXE

- [ ] Create table
- [ ] Insert data
- [ ] Update rows
- [ ] Delete rows
- [ ] Create index (clustered)
- [ ] Create view
- [ ] Query view
- [ ] Create procedure
- [ ] Execute procedure
---

## 🔗 EXTERNÍ LINKY

- T-SQL Reference: https://learn.microsoft.com/en-us/sql/t-sql/language-reference
- Data Warehouse: https://learn.microsoft.com/fabric/data-warehouse/data-warehouse-overview
- Performance Tuning: https://learn.microsoft.com/en-us/sql/relational-databases/indexes/

---

## NEXT → [[9_MONITORING]]