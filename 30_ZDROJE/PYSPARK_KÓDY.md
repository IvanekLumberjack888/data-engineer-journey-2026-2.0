# 🐍 PYSPARK SNIPPETY

Kopír-vlož PySpark kódy

---

## SETUP

### Load from table
```python
df = spark.sql("SELECT * FROM table_name")
display(df)
```

### Load from CSV
```python
df = spark.read.csv("/path/to/file.csv", header=True, inferSchema=True)
```

### Load from Parquet
```python
df = spark.read.parquet("/path/to/file.parquet")
```

---

## SELECT & FILTER

### Show data
```python
df.show(10)  # First 10 rows
display(df)  # Pretty display
```

### Select columns
```python
df.select("column1", "column2")
df.select(["column1", "column2"])
```

### Filter rows
```python
from pyspark.sql.functions import col

df.filter(col("age") > 30)
df.filter((col("age") > 30) & (col("city") == "NYC"))
df.filter(col("name").contains("John"))
```

---

## TRANSFORMATIONS

### Rename column
```python
df.withColumnRenamed("old_name", "new_name")
```

### Add column
```python
df.withColumn("new_col", col("existing_col") * 2)
```

### Drop column
```python
df.drop("column_to_drop")
```

### Cast type
```python
df.withColumn("age_int", col("age").cast("int"))
```

---

## AGGREGATION

### Count
```python
df.count()
```

### Group by
```python
df.groupBy("category").count()
```

### Multiple aggregates
```python
from pyspark.sql.functions import sum, avg, count

df.groupBy("category").agg(
  sum("amount").alias("total"),
  avg("amount").alias("average"),
  count("*").alias("count")
)
```

### Describe (statistics)
```python
df.describe("column1", "column2")
```

---

## JOINS

### Inner join
```python
df1.join(df2, on="key", how="inner")
```

### Left join
```python
df1.join(df2, on="key", how="left")
```

### Right join
```python
df1.join(df2, on="key", how="right")
```

### Multi-key join
```python
df1.join(df2, on=["key1", "key2"], how="inner")
```

---

## WRITE DATA

### Save as table
```python
df.write.mode("overwrite").saveAsTable("new_table")
```

### Append mode
```python
df.write.mode("append").saveAsTable("existing_table")
```

### Parquet
```python
df.write.mode("overwrite").parquet("/path/to/file")
```

### CSV
```python
df.write.csv("/path/to/file", header=True)
```

---

## ADVANCED

### Window functions
```python
from pyspark.sql.functions import row_number, rank
from pyspark.sql.window import Window

w = Window.partitionBy("category").orderBy("amount")
df.withColumn("rank", rank().over(w))
```

### Case when
```python
from pyspark.sql.functions import when

df.withColumn("category", 
  when(col("amount") > 1000, "High")
  .when(col("amount") > 100, "Medium")
  .otherwise("Low")
)
```

### UDF (User Defined Function)
```python
from pyspark.sql.functions import udf
from pyspark.sql.types import StringType

@udf(StringType())
def upper_case(s):
  return s.upper()

df.withColumn("upper_name", upper_case(col("name")))
```

---

Interní: [[2_LAKEHOUSE_SPARK]]
External: https://spark.apache.org/docs/latest/api/python/