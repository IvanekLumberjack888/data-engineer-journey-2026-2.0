# 9️⃣ MONITORING & PERFORMANCE

**Cíl:** Monitorovat a optimalizovat query performance

---

## 📖 TEORIE

### Dynamic Management Views (DMVs)

Systémové views s runtime info.

**Běžné DMVs:**
```sql
-- Query execution history
SELECT * FROM sys.dm_exec_query_stats

-- Current queries
SELECT * FROM sys.dm_exec_requests

-- Wait statistics
SELECT * FROM sys.dm_os_wait_stats
```

### Query Execution Plans

Jak SQL engine bude spouštět query.

**Analýza:**
- Sequential scan vs Index seek
- Join strategies (nested loop, hash, merge)
- Cost estimates
- Actual vs estimated rows

### Performance Metrics

**Důležité metriky:**
- CPU time
- Elapsed time
- Reads/Writes
- Row count
- Query plan

### Optimization Tips

1. **Indexing** — Správné indexy
2. **Statistics** — Aktuální table stats
3. **Partitioning** — Data split
4. **Denormalization** — Pre-aggregated data
5. **Caching** — Frequently used data

### Monitoring Tools

**Monitor Hub:**
- Real-time activity tracking
- Failed jobs
- Performance insights
- Resource consumption

**Capacity Metrics App:**
- Workspace usage
- User activity
- Resource utilization

---

## 🛠️ PRAXE

- [x] Query DMVs for stats
- [x] Analyze execution plan
- [x] Identify slow queries
- [x] Add index
- [x] Re-run query (compare)
- [x] Update statistics
- [x] Monitor in Monitor Hub
- [x] Check Capacity Metrics
---

## 🔗 EXTERNÍ LINKY

- DMVs: https://learn.microsoft.com/en-us/sql/relational-databases/dynamic-management-views/
- Execution Plans: https://learn.microsoft.com/en-us/sql/relational-databases/query-processing/
- Monitor Hub: https://learn.microsoft.com/fabric/admin/monitor-capacity

---

## NEXT → [[10_BEZPEČNOST]]