# 2️⃣ LAB: SPARK NOTEBOOK

## Cíl

Psát PySpark kód v Notebooku. DataFrame transformace.

---

## Praxe - Krok za krokem

### Krok 1: Create Notebook

```
1. New item → Notebook
2. Name: "Sales_Transformations"
3. Create
```

- [ ] Notebook vytvořen

### Krok 2: Read Table as DataFrame

**Cell 1:**
```python
df = spark.sql("SELECT * FROM Sales")
display(df)  # Beautiful output
```

- [ ] Tabulka načtena do DataFrame

### Krok 3: Filter

**Cell 2:**
```python
from pyspark.sql.functions import col

# Filter: Amount > 1000
df_filtered = df.filter(col("Amount") > 1000)
display(df_filtered)
```

- [ ] Filtrováno

### Krok 4: Groupby + Aggregate

**Cell 3:**
```python
from pyspark.sql.functions import sum, count

df_agg = df.groupBy("Category").agg(
  sum("Amount").alias("TotalAmount"),
  count("*").alias("Count")
)
display(df_agg)
```

- [ ] Agregováno

### Krok 5: Write to Table

**Cell 4:**
```python
# Save back to Lakehouse as new table
df_agg.write.mode("overwrite").option("mergeSchema", "true").saveAsTable("Sales_Summary")
```

- [ ] Tabulka uložena

### Krok 6: Verify

**Cell 5:**
```python
# Verify the new table
df_verify = spark.sql("SELECT * FROM Sales_Summary")
display(df_verify)
```

- [ ] Ověřeno

---

## Pozorování

- Kolik řádků bylo filtrováno?
- Jaké byly top 3 kategorie?

---

## Next: [[3_LAB_DATAFLOW.md]]