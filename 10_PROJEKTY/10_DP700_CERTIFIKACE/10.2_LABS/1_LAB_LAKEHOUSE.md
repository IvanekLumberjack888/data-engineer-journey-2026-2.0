# 🔬 Lab 1: Lakehouse Setup

**Cíl:** Vytvořit Fabric Lakehouse a nahrát první data

---

## ⏱️ Čas
45 minut

## 📋 Prerequisites
- Fabric trial account aktivní
- Workspace vytvořený

---

## 🔨 Kroky

### 1️⃣ Vytvoř Lakehouse

1. Otevři workspace
2. **+ New** → **Lakehouse**
3. Název: `Lab01_Lakehouse`
4. **Create**

---

### 2️⃣ Upload Sample Data

Download: [sales.csv](https://raw.githubusercontent.com/MicrosoftLearning/dp-data/main/sales.csv)

Upload do Files folder

---

### 3️⃣ Vytvoř Delta Table

```python
df = spark.read.format("csv")\
    .option("header", "true")\
    .load("Files/sales.csv")

df.write.format("delta")\
    .mode("overwrite")\
    .saveAsTable("bronze_sales")
```

---

### 4️⃣ Verify

Check Tables folder → `bronze_sales` existuje

---

## ✅ Success Criteria

- [x] Lakehouse vytvořený
- [x] Data uploadovaná
- [x] Delta table vytvořená
- [x] SQL query funguje

---

## 🔗 Linky

- **Teorie:** [[10.1_NOTES/2_LAKEHOUSE_SPARK|Note 2]]
- **Další:** [[2_LAB_SPARK|Lab 2: Spark]]

---

NEXT → [[2_LAB_SPARK|Lab 2]]
