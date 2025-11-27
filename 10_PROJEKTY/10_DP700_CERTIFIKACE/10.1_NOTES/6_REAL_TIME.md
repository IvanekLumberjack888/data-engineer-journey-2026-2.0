# 6️⃣ REAL-TIME INTELLIGENCE

**Cíl:** Pochopit real-time analytics a event sourcing

---

## 📖 TEORIE

### Co je Real-Time Intelligence?

Schopnost analyzovat data v reálném čase.

**Komponenty:**
- Eventstreams (ingestion)
- Eventhouse (storage)
- KQL (querying)
- Dashboards (visualization)

### Eventstreams

Schopnost příjímat data z více zdrojů.

**Zdroje:**
- Event Hubs
- IoT Hub
- Kafka
- Sample sources (bicycles)

**Transformace:**
- Aggregate
- Filter
- Enrich
- Deduplicate
- Group by with temporal windows

### Eventhouse

KQL database pro real-time analytics.

**Vlastnosti:**
- Automatic indexing
- High ingestion rate
- Low latency queries
- Built-in retention policies

### Event Sourcing

Design pattern: Uklady všechny eventy jako immutable log.

**Příklad:**
- Event 1: Order placed ($100)
- Event 2: Item shipped
- Event 3: Delivery confirmed
- State = reconstruct z events

---

## 🛠️ PRAXE

- [ ] Create Eventhouse
- [ ] Create Eventstream
- [ ] Add sample source (Bicycles)
- [ ] Configure transformations (Group By)
- [ ] Add destination (Eventhouse)
- [ ] Publish eventstream
- [ ] Query data in KQL

---

## 🔗 EXTERNÍ LINKY

- Real-Time Hub: https://learn.microsoft.com/fabric/real-time-intelligence/real-time-hub-overview
- Eventstreams: https://learn.microsoft.com/fabric/real-time-intelligence/eventstreams/overview
- Event Sourcing: https://learn.microsoft.com/en-us/azure/architecture/patterns/event-sourcing

---

## NEXT → [[7_KQL_EVENTHOUSE]]
