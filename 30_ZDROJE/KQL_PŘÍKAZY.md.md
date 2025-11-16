# ⚡ KQL SNIPPETY

Kopír-vlož KQL kódy

---

## BASIC

### First N rows
```kql
TableName
| take 10
```

### Filter
```kql
TableName
| where column_name > 100
| where column_name == "value"
| where column_name contains "text"
```

### Select columns
```kql
TableName
| project column1, column2, column3
```

### Rename column
```kql
TableName
| project column1_new = column1
```

### Multiple conditions
```kql
TableName
| where column1 > 10 and column2 == "value"
| where column1 in (1, 2, 3)
```

---

## AGGREGATION

### Count
```kql
TableName
| summarize count()
```

### Sum, Average, Min, Max
```kql
TableName
| summarize 
  Total = sum(column),
  Average = avg(column),
  Minimum = min(column),
  Maximum = max(column)
```

### Group By
```kql
TableName
| summarize count() by category
```

### Multiple aggregates
```kql
TableName
| summarize 
  Sales = sum(amount),
  Count = count(),
  Avg = avg(amount)
  by region, product
```

---

## SORTING

### Sort ascending
```kql
TableName
| sort by column asc
```

### Sort descending
```kql
TableName
| sort by column desc
```

### Multiple columns
```kql
TableName
| sort by column1 desc, column2 asc
```

---

## TIME WINDOWS

### 5-minute buckets
```kql
TableName
| summarize count() by bin(timestamp, 5m)
```

### Daily aggregation
```kql
TableName
| summarize Total = sum(amount) by bin(timestamp, 1d)
```

### Top N per group
```kql
TableName
| summarize count() by category
| top 5 by count_
```

---

## JOINS

### Inner join
```kql
table1
| join kind=inner table2 on key
```

### Left join
```kql
table1
| join kind=left table2 on key
```

### Right join
```kql
table1
| join kind=right table2 on key
```

---

## ADVANCED

### Distinct values
```kql
TableName
| distinct category
```

### Fill missing values
```kql
TableName
| make-series count() default=0 on timestamp from start to end step 1h
```

### Percentiles
```kql
TableName
| summarize percentiles(column, 50, 95, 99)
```

### String operations
```kql
TableName
| where name contains "text"
| where name startswith "A"
| where name endswith "z"
```

### Date operations
```kql
TableName
| where timestamp > ago(7d)
| where timestamp between (start_time .. end_time)
```

---

## MATERIALIZED VIEWS

### Create view
```kql
.create materialized-view MyView on table TableName {
  TableName
  | summarize count() by category
}
```

### Query view
```kql
MyView
| sort by count_ desc
```

---

Interní: [[7_KQL_EVENTHOUSE.md]]
External: https://learn.microsoft.com/en-us/kusto/query/