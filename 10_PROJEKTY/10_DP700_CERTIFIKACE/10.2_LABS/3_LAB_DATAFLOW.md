# 3️⃣ LAB: DATAFLOW

## Cíl

Vytvořit Dataflow Gen2 (no-code ETL) s transformacemi.

---

## Praxe - Krok za krokem

### Krok 1: Create Dataflow Gen2

```
1. New item → Dataflow Gen2
2. Name: "Sales_ETL"
3. Create
```

- [x] Dataflow vytvořen

### Krok 2: Connect to Source

```
1. Get Data → Choose source
   - CSV file (from your Files)
   - Or SQL (from Sales table)
2. Connect
```

- [x] Zdroj připojen

### Krok 3: Add Transformations

**Transform 1: Filter**
```
1. Home → Filter rows
2. Amount > 500
3. OK
```

- [x] Filter aplikován

**Transform 2: Column rename**
```
1. Transform → Rename columns
2. Amount → SalesAmount
3. OK
```

- [x] Rename aplikován

**Transform 3: Group by**
```
1. Transform → Group By
2. Group by: Category
3. New column: SUM(SalesAmount)
4. OK
```

- [x] Agregace aplikována

### Krok 4: Set Destination

```
1. Add destination
2. Lakehouse → Sales_DW
3. Table name: "Sales_Cleaned"
4. Create new table
```

- [x] Destination nastaveno

### Krok 5: Publish & Refresh

```
1. Publish
2. Refresh
3. Wait for completion
```

- [x] Dataflow se spustil

### Krok 6: Verify Output

```
1. Go to Lakehouse
2. Find "Sales_Cleaned" table
3. View data
```

- [x] Output ověřen

---

## Pozorování

- Kolik řádků bylo transformováno? 150
- Jak dlouho trvala transformace? 00:00:23

---

## Next: [[4_LAB_WAREHOUSE]]