# 🔧 SQL SNIPPETY

Kopír-vlož T-SQL kódy

---

## TABLE OPERATIONS

### Create table
```sql
CREATE TABLE Sales (
  SalesID INT PRIMARY KEY,
  Date DATE,
  Amount DECIMAL(10,2),
  Category VARCHAR(50)
)
```

### Add column
```sql
ALTER TABLE Sales ADD COLUMN Region VARCHAR(50)
```

### Drop column
```sql
ALTER TABLE Sales DROP COLUMN Region
```

### Rename column
```sql
EXEC sp_rename 'Sales.Amount', 'SalesAmount'
```

---

## DATA MANIPULATION

### Insert data
```sql
INSERT INTO Sales (SalesID, Date, Amount)
VALUES (1, '2025-01-01', 100.50)
```

### Insert from select
```sql
INSERT INTO Sales_Copy
SELECT * FROM Sales WHERE Year(Date) = 2025
```

### Update data
```sql
UPDATE Sales SET Amount = 200 WHERE SalesID = 1
```

### Delete data
```sql
DELETE FROM Sales WHERE SalesID = 1
```

### Upsert (INSERT or UPDATE)
```sql
MERGE INTO Sales as target
USING Sales_New as source
ON target.SalesID = source.SalesID
WHEN MATCHED THEN UPDATE SET target.Amount = source.Amount
WHEN NOT MATCHED THEN INSERT VALUES (source.SalesID, source.Date, source.Amount)
```

---

## QUERIES

### Select all
```sql
SELECT * FROM Sales
```

### Select with conditions
```sql
SELECT SalesID, Amount FROM Sales WHERE Amount > 100
```

### Group by
```sql
SELECT Category, SUM(Amount) as Total, COUNT(*) as Count
FROM Sales
GROUP BY Category
HAVING SUM(Amount) > 500
```

### Order by
```sql
SELECT * FROM Sales ORDER BY Amount DESC
```

### Distinct
```sql
SELECT DISTINCT Category FROM Sales
```

---

## JOINS

### Inner join
```sql
SELECT s.SalesID, s.Amount, c.CategoryName
FROM Sales s
INNER JOIN Categories c ON s.Category = c.CategoryID
```

### Left join
```sql
SELECT s.SalesID, c.CategoryName
FROM Sales s
LEFT JOIN Categories c ON s.Category = c.CategoryID
```

### Self join
```sql
SELECT a.SalesID, b.SalesID
FROM Sales a
INNER JOIN Sales b ON a.Category = b.Category
WHERE a.SalesID < b.SalesID
```

---

## INDEXES

### Clustered index
```sql
CREATE CLUSTERED INDEX idx_sales_id ON Sales(SalesID)
```

### Non-clustered index
```sql
CREATE NONCLUSTERED INDEX idx_category ON Sales(Category)
```

### Columnstore index
```sql
CREATE CLUSTERED COLUMNSTORE INDEX idx_ccs ON Sales
```

### Drop index
```sql
DROP INDEX idx_sales_id ON Sales
```

---

## VIEWS

### Create view
```sql
CREATE VIEW SalesTotals AS
SELECT Category, SUM(Amount) as Total
FROM Sales
GROUP BY Category
```

### Query view
```sql
SELECT * FROM SalesTotals WHERE Total > 1000
```

### Drop view
```sql
DROP VIEW SalesTotals
```

---

## STORED PROCEDURES

### Create procedure
```sql
CREATE PROCEDURE usp_GetSalesByCategory @category VARCHAR(50)
AS
BEGIN
  SELECT * FROM Sales WHERE Category = @category
END
```

### Execute procedure
```sql
EXEC usp_GetSalesByCategory 'Electronics'
```

---

## ADVANCED

### CTE (Common Table Expression)
```sql
WITH CategoriedSales AS (
  SELECT Category, SUM(Amount) as Total
  FROM Sales
  GROUP BY Category
)
SELECT * FROM CategoriedSales WHERE Total > 500
```

### Window function
```sql
SELECT 
  SalesID, 
  Amount,
  ROW_NUMBER() OVER (ORDER BY Amount DESC) as Rank
FROM Sales
```

### Transaction
```sql
BEGIN TRANSACTION
INSERT INTO Sales VALUES (999, '2025-01-01', 100.00)
IF @@ERROR <> 0 ROLLBACK ELSE COMMIT
```

---

Interní: [[8_WAREHOUSE_SQL.md]]
External: https://learn.microsoft.com/en-us/sql/t-sql/language-reference