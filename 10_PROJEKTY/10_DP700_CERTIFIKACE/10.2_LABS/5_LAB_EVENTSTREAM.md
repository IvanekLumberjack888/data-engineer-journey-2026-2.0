# 5️⃣ LAB: EVENTSTREAM

## Cíl

Vytvořit Eventstream pro real-time data. Nastavit transformace a destinace.

---

## Praxe - Krok za krokem

### Krok 1: Create Eventhouse

```
1. New item → Eventhouse
2. Name: "SalesRealTime"
3. Create
```

- [x] Eventhouse vytvořen

### Krok 2: Create Eventstream

```
1. New item → Eventstream
2. Name: "SalesEvents"
3. Create
```

- [x] Eventstream vytvořen

### Krok 3: Add Source (Sample Data)

```
1. Eventstream canvas
2. Add source
3. Sample data → Bicycles (built-in)
4. Create
```

- [x] Zdroj přidán

### Krok 4: Add Transformation

```
1. Add transform → Group by
2. Group by: station_id
3. Aggregate: COUNT() as bike_count
4. Time window: 1 minute
5. Create
```

- [x] Transformace přidána

### Krok 5: Add Destination

```
1. Add destination → Eventhouse
2. Select your Eventhouse
3. Table name: "BikeData"
4. Create
```

- [x] Destinace přidána

### Krok 6: Publish

```
1. Publish
2. Data začne téct do Eventhouse
```

- [x] Eventstream běží

### Krok 7: Query Eventhouse

Přepni na Eventhouse:
```kql
BikeData
| take 100
```

- [ ] Data viditelná v Eventhouse

---

## Pozorování

- Kolik events/sec přichází?
- Jaké jsou top 3 stanice?

---

## Next: [[6_LAB_KQL]]