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

## 6️⃣ REAL-TIME INTELLIGENCE

**Cíl:** Pochopit real-time event streaming a KQL

### 🔑 3-5 Key Bullet Points (EN)

- Eventstream in Fabric captures real-time data from IoT devices, applications, and cloud services, routing events to lakehouse, warehouse, or KQL database
- KQL (Kusto Query Language) provides sub-second query performance on streaming data through automatic indexing and columnar compression for real-time dashboards
- Event Hubs integration enables Fabric to consume from Azure Event Hubs, Kafka topics, or custom HTTP endpoints with automatic schema evolution
- Real-time dashboards and Power BI reports connected to KQL databases update instantly as events arrive, supporting operational monitoring
- Latency in real-time intelligence is measured in seconds (ingestion to query availability) rather than minutes/hours, enabling true real-time decision-making

### ❓ 5 DP-700 Style Exam Questions (EN)

1. You need to monitor 10,000 IoT sensors with millisecond latency. Should you use Eventstream → KQL or Eventstream → Lakehouse + SQL warehouse?

2. An Eventstream captures events from IoT hub where schema evolves monthly (new sensors). How does Fabric handle schema changes?

3. Your organization needs a real-time dashboard showing active sessions updated every 5 seconds. Which KQL feature provides best performance?

4. Comparing Azure Stream Analytics vs. Fabric Eventstream + KQL, what is the primary advantage of Fabric's integrated solution?

5. A KQL query aggregates 1 million events per second. Performance is slow. Which optimization technique would help most?

### ✅ Checklist: Co musím umět (CZ)

- ✅ Vytvořit Eventstream z IoT hub nebo Event Hubs
- ✅ Napsat základní KQL query s filtrováním
- ✅ Implementovat real-time dashboard s KQL daty
- ✅ Pochopit latency a throughput limitace
- ✅ Designovat schema pro stream events
- ✅ Konfigurovat alerting na KQL data
- ✅ Pochopit retention policies pro streaming data

### 🔗 Linky
- Praxe: [[6_LAB_KQL|Lab 6: KQL Queries]]
- Následující: [[7_KQL_EVENTHOUSE|Note 7: KQL & Eventhouse]]
- Zpět: [[5_MEDALLION_ARCHITEKTURA|Note 5: Medallion Architektura]]

---