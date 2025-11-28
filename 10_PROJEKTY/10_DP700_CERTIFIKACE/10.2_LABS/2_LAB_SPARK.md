# 🔬 Lab 2: Spark Notebook Transformations

**Cíl:** Napsat PySpark transformace a pochopit lazy evaluation

---

## ⏱️ Čas
60 minut

## 📋 Prerequisites
- Dokončený Lab 1
- Table `bronze_sales` existuje

---

## 🔨 Kroky

### 1️⃣ Create Notebook

1. V lakehouse klikni **Open notebook** → **New notebook**
2. Název: `Lab02_Transformations`

---

### 2️⃣ Load Data

```python
# Load bronze table
df = spark.read.table("bronze_sales")

# Show schema
df.printSchema()

# Count rows
print(f"Total rows: {df.count()}")
```

---

### 3️⃣ Filter Data

```python
# Filter: Only sales > $100
df_filtered = df.filter(df["SalesAmount"] > 100)

# POZOR: Zatím se NIC neprovedlo! (lazy evaluation)

# Action - TEĎ se provede
print(f"Rows with sales > 100: {df_filtered.count()}")
```

---

### 4️⃣ Select Columns

```python
# Select only certain columns
df_selected = df_filtered.select(
    "OrderDate",
    "ProductName",
    "SalesAmount"
)

display(df_selected.limit(10))
```

---

### 5️⃣ Aggregate Data

```python
from pyspark.sql.functions import sum, count, avg

# Group by ProductName
df_agg = df.groupBy("ProductName").agg(
    sum("SalesAmount").alias("TotalSales"),
    count("*").alias("OrderCount"),
    avg("SalesAmount").alias("AvgSale")
)

display(df_agg.orderBy("TotalSales", ascending=False))
```

---

### 6️⃣ Write to Silver Layer

```python
# Write aggregated data to silver table
df_agg.write.format("delta")\
    .mode("overwrite")\
    .saveAsTable("silver_product_summary")

print("✅ Silver table created!")
```

---

### 7️⃣ Verify Silver Table

```sql
-- Change to SQL cell
SELECT * FROM silver_product_summary
ORDER BY TotalSales DESC
```

---

### 8️⃣ Test Lazy Evaluation

```python
# Chain multiple transformations
df_lazy = df\
    .filter(df["SalesAmount"] > 50)\
    .select("ProductName", "SalesAmount")\
    .groupBy("ProductName")\
    .sum("SalesAmount")

print("Transformations defined!")
print("Nothing executed yet!")

# NOW execute
df_lazy.show(10)  # Action triggers execution
```

---

## ✅ Success Criteria

- [ ] Notebook `Lab02_Transformations` vytvořený
- [ ] PySpark filter, select, groupBy běží
- [ ] Silver table `silver_product_summary` vytvořená
- [ ] Rozumíš lazy evaluation (transformations vs actions)
- [ ] Umíš chain multiple transformations

---

## 💡 Tips

- **Transformations** (lazy): filter, select, join, groupBy
- **Actions** (execute): show, count, write, collect
- Chain transformations před action pro lepší optimization
- `display()` je Fabric-specific (use `show()` in production)

---

## 🔗 Linky

- **Teorie:** [[10.1_NOTES/2_LAKEHOUSE_SPARK|Note 2: Lakehouse & Spark]]
- **Další Lab:** [[3_LAB_DATAFLOW|Lab 3: Dataflow Gen2]]
- **Předchozí:** [[1_LAB_LAKEHOUSE|Lab 1: Lakehouse]]
- **Index:** [[10_INDEX|Zpět na index]]

---

## NEXT → [[3_LAB_DATAFLOW|Lab 3: Dataflow Gen2]]
