# 6️⃣ LAB: KQL QUERIES

## Cíl

Psát KQL dotazy v Eventhouse. Agregace, filtrování, grouping.

---

## Praxe - Krok za krokem

### Krok 1: Basic Query

```kql
BikeData
| take 10
```

- [ ] First 10 rows viditelné

### Krok 2: Filter

```kql
BikeData
| where bike_count > 5
| take 20
```

- [ ] Filtrované výsledky

### Krok 3: Aggregation

```kql
BikeData
| summarize 
  AvgBikes = avg(bike_count),
  MaxBikes = max(bike_count),
  TotalEvents = count()
```

- [ ] Agregace zobrazena

### Krok 4: Group by

```kql
BikeData
| summarize TotalBikes = sum(bike_count) by station_id
| sort by TotalBikes desc
```

- [ ] Grouping + sort funguje

### Krok 5: Time Window

```kql
BikeData
| summarize BikeCount = sum(bike_count) by bin(timestamp, 5m)
| sort by timestamp asc
```

- [ ] 5-minute windows viditelné

### Krok 6: Multiple Conditions

```kql
BikeData
| where bike_count > 3
| summarize Avg = avg(bike_count), Max = max(bike_count) by station_id
| where Avg > 4
| sort by Max desc
```

- [ ] Komplexní query funguje

---

## Pozorování

- Která stanice má nejvíc průměrně kol?
- Jaký je trend v čase?

---

## Next: [[7_LAB_SECURITY.md]]