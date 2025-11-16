# 3️⃣ DELTA LAKE

## Teorie

### ACID Transactions

**ACID = Atomicity, Consistency, Isolation, Durability**

- **Atomicity:** All or nothing (whole transaction succeeds or fails)
- **Consistency:** Data always valid (constraints respected)
- **Isolation:** Concurrent writes don't interfere
- **Durability:** Once committed, data persists

**Why matters:** 
- Multiple people writing simultaneously = no corruption
- If process fails halfway = rollback (no partial data)

### Time Travel

Query data from any point in time.

**Syntax:**
```sql
SELECT * FROM my_table VERSION AS OF 0  -- Version 0
SELECT * FROM my_table TIMESTAMP AS OF '2025-11-17 10:00:00'  -- Specific time
```

**Use case:**
- Recover deleted data
- Audit data changes
- Compare versions

### Schema Evolution

Add/remove/rename columns over time.

**Example:**
```
v1: id, name, amount
v2: id, name, amount, email (added)
v3: id, full_name, amount, email (renamed: name → full_name)
```

Delta Lake tracks all versions automatically.

### Optimization Commands

**VACUUM:** Delete old file versions (clean up storage)
```sql
VACUUM my_table RETAIN 7 DAYS  -- Keep 7 days, delete older
```

**OPTIMIZE:** Compact small files into bigger ones
```sql
OPTIMIZE my_table
```

**ANALYZE:** Update statistics for query planning
```sql
ANALYZE TABLE my_table COMPUTE STATISTICS
```

**Best practice:**
Run OPTIMIZE before big queries for better performance.

### Z-Ordering

Co-locate related columns for faster filtering.

```sql
OPTIMIZE my_table ZORDER BY (customer_id, date)
```

Result: Queries filtering by customer_id OR date będzie faster.

---

## Praxe

- [ ] Create Delta table from CSV
- [ ] Insert new data
  ```python
  new_data = spark.createDataFrame([(1, "John", 1000)], ["id", "name", "amount"])
  new_data.write.mode("append").saveAsTable("my_table")
  ```
- [ ] Time travel query
  ```sql
  SELECT * FROM my_table VERSION AS OF 0  -- First version
  ```
- [ ] DESCRIBE HISTORY
  ```sql
  DESCRIBE HISTORY my_table  -- See all versions
  ```
- [ ] OPTIMIZE table
  ```sql
  OPTIMIZE my_table
  ```

---

## Otázky

- Jak dlouho se historii uchovávají (default retention)?
- Jaký je impact VACUUM na performance?

---

## Key Takeaways

1. **Delta Lake** = ACID guarantees for data lakes
2. **Time Travel** = Query historical versions
3. **Schema Evolution** = Add/modify columns without breaking
4. **VACUUM** = Clean storage
5. **OPTIMIZE** = Improve query performance

---

## Next: [[4_DATAFLOW_PIPELINE|4. Dataflow & Pipeline]]