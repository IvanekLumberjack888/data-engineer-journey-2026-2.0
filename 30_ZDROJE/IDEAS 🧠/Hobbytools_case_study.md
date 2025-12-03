# Case Study: Data Platform pro Pronajímání Nářadí + Servis

## Kontext: HobbyTools CZ

Anonymizovaná společnost "HobbyTools CZ" - pronajímá profesionální nářadí a vybavení pro domácnosti a staveniště.

**Produk:** Vrtačky, pily, brusky, stroje na vysokotlakové čištění (Kärcher style), zahradní vybavení, průmyslové čističe.

**Byznys model:**

- Pronajímání nářadí (4h, 24h, týdenní, měsíční sazby)
    
- Servis a opravy pronajímaného vybavení (záruční, bez záruk, pojistné)
    
- Prodej doplňků a náhradních dílů
    
- Čištění a údržba nářadí po vrácení
    

**Problémy:**

- Data jsou rozptýlená (Excel, SharePoint, papírové formuláře)
    
- Neznámá ziskovost pronajímek (vs náklady na servis)
    
- Nemohou predikovat, které stroje se Often porouchají
    
- Neznají, kolik lidí v obchodě se věnuje servisům vs pronajímání
    
- Nemohou vidět korelace: počet rentálů vs počet zaměstnanců

---


✅ **HobbyTools CZ** – realistická společnost (nářadí, servisy, IoT senzory)  
✅ **Data sources** – 8+ zdrojů (SharePoint, Excel, APIs, IoT, legacy SQL)  
✅ **Silver layer** – Python notebooky s real transformacemi  
✅ **Gold layer** – KPI analýzy: profitabilita, nástroje na odprodej, staff impact  
✅ **Data Quality** – checks na anomálie  
✅ **Power BI** – 4 dashboardy  
✅ **GitHub struktura** – ready na veřejný repo  
✅ **Real insights** – co by firma zjistila ("Drills jsou ztráta", "Pondelí vs víkend")

| Aspekt          | Auto              | Nářadí                     |
| --------------- | ----------------- | -------------------------- |
| Cena pronajímky | 500–2000 CZK/den  | 50–500 CZK/den             |
| Servis          | Skoro žádný       | Kritický (filtry, těsnění) |
| IoT             | GPS, stav         | Usage hours, error codes   |
| Customer        | Dlouhá pronajímka | Krátkodobá (4h–1 týden)    |
| Risk            | Havárie           | Rozbití, zneužití          |

---
## Zdroje dat

```
Ingestion Layer (Dataflow Gen2)
├── SharePoint Lists
│   ├── tools_inventory (vrt, pila, brušt...)
│   └── rental_customers (kontakty, historie)
├── Excel files (CloudStorage)
│   ├── weekly_rentals (pronajímky minulý týden)
│   ├── repairs_log (servis zápisy)
│   └── replacement_parts_sales (prodej dílů)
├── API
│   ├── HR system (zaměstnanci, dovolenou, přesčasy)
│   ├── Invoicing system (faktury, platby, DPH)
│   └── Customer feedback API (recenze pronajímek)
├── SQL Database (legacy system)
│   ├── tools_maintenance_history
│   ├── rental_transactions
│   └── customer_complaints
└── IoT Sensors (Kärcher-style equipment)
    ├── Usage hours counter (v nářadí)
    ├── Error codes (když se něco pokazí)
    └── GPS location (kde je nástroj pronajat - staveniště)
```
