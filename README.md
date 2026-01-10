Perfekt. Tady je README **100% v angličtině** s badges jako tvůj SQL projekt:

text

``# Fabric Rental Analytics Platform <div align="center"> ![Fabric](https://img.shields.io/badge/Microsoft-Fabric-0078D4?style=for-the-badge&logo=microsoft-azure) ![PySpark](https://img.shields.io/badge/PySpark-3.5-orange?style=for-the-badge&logo=apache-spark) ![Power BI](https://img.shields.io/badge/Power-BI-FFB900?style=for-the-badge&logo=power-bi) ![Python](https://img.shields.io/badge/Python-3.10%2B-blue?style=for-the-badge&logo=python) ![License](https://img.shields.io/badge/License-MIT-success?style=for-the-badge) **End-to-end data platform case study for tool rental analytics** – Medallion architecture with Dataflow Gen2, PySpark, and Power BI </div> --- ## 📋 Table of Contents - [Project Overview](#project-overview) - [Business Context](#business-context) - [Architecture](#architecture) - [Technical Stack](#technical-stack) - [Quick Start](#quick-start) - [Project Structure](#project-structure) - [KPIs & Use Cases](#kpis--use-cases) - [Documentation](#documentation) --- ## 🎯 Project Overview **HobbyTools CZ** – A fictional company renting professional tools (drills 🛠️, saws 🪚, grinders ⚙️, pressure washers 💦) with maintenance and spare parts sales services. ### Business Pain Points | ❌ Problem | ✅ Solution | |-----------|-----------| | Data scattered across Excel, SharePoint, paper forms | Centralized Fabric data platform | | Unknown profitability of rentals vs. repair costs | `gold_rental_profitability` KPI | | No tool failure predictions | `gold_maintenance_forecast` with telemetry | | Unclear staff workload distribution | `gold_staff_productivity` analytics | | Missing correlation: rentals ↔ revenue | `gold_category_performance` insights | --- ## 🏢 Business Context ### Service Model - **Tool Rentals** – 4h, 24h, weekly, monthly rates - **Maintenance & Repairs** – Warranty, non-warranty, insurance claims - **Spare Parts Sales** – Accessories and replacement components - **Cleaning Services** – Post-rental equipment maintenance ### Key Metrics to Track - Rental revenue per tool category - Repair costs as % of rental revenue - Tool downtime and maintenance intervals - Staff productivity vs. revenue per location - Customer lifetime value and segmentation --- ## 🏗️ Architecture ### Medallion Pattern (Bronze → Silver → Gold)``

┌──────────────────────────────────────────────────────────┐  
│ INGESTION (Dataflow Gen2 – No-Code) 📥 │  
│ SharePoint | Excel | REST APIs | SQL | IoT Telemetry │  
└──────────────────────────────────────────────────────────┘  
↓  
┌──────────────────────────────────────────────────────────┐  
│ BRONZE (Lakehouse – Raw Data) 🟤 │  
│ bronze_rentals | bronze_tools | bronze_repairs │  
│ bronze_staff | bronze_invoices | bronze_tools_telemetry │  
└──────────────────────────────────────────────────────────┘  
↓  
┌──────────────────────────────────────────────────────────┐  
│ SILVER (Cleaned & Typed) 🟡 │  
│ silver_rentals | silver_tools_health | silver_repairs │  
│ silver_staff_daily | silver_maintenance_timeline │  
└──────────────────────────────────────────────────────────┘  
↓  
┌──────────────────────────────────────────────────────────┐  
│ GOLD (KPI & Analytics) 🟢 │  
│ gold_rental_profitability | gold_tool_reliability │  
│ gold_category_performance | gold_staff_productivity │  
│ gold_maintenance_forecast | gold_customer_lifetime_value │  
└──────────────────────────────────────────────────────────┘  
↓  
┌──────────────────────────────────────────────────────────┐  
│ POWER BI DASHBOARDS 📊 │  
│ Rental Performance | Tool Health | Staff Productivity │  
│ Financial Overview | Maintenance Alerts │  
└──────────────────────────────────────────────────────────┘

text

``### Data Lineage | Layer | Input Source | Output Tables | Purpose | |-------|--------------|---------------|---------| | 🟤 BRONZE | SharePoint, Excel, APIs, SQL, IoT | Raw tables | Historical record | | 🟡 SILVER | Bronze tables | Cleaned tables | Data quality guaranteed | | 🟢 GOLD | Silver tables | KPI tables | Dashboard-ready | | 📊 BI | Gold tables | Visualizations | Business insights | --- ## 🛠️ Technical Stack | Component | Technology | Purpose | |-----------|----------|---------| | **Ingestion** | Dataflow Gen2 | No-code data loading | | **Storage** | Delta Lake (Lakehouse) | Versioned data tables | | **Processing** | PySpark (Notebooks) | Transformations | | **Analytics** | SQL, Power BI | Queries & reports | | **Orchestration** | Fabric Scheduler | Automated pipelines | ### PySpark Techniques Used - ✅ DataFrame operations (`withColumn`, `select`, `filter`) - ✅ Multi-table `join` operations - ✅ Aggregations (`groupBy`, `agg`, `sum`, `count`, `avg`) - ✅ Window functions for ranking & running totals - ✅ Delta Lake `saveAsTable` with overwrite mode - ✅ Data validation & quality checks --- ## 🚀 Quick Start (5 Minutes) ### 1️⃣ Generate Synthetic Data ```bash python synthetic_data/generate_synthetic_data.py``

This creates test datasets:

- `bronze_rentals_sample.csv` (500 rentals)
    
- `bronze_tools_sample.csv` (50 tools)
    
- `bronze_repairs_sample.csv` (200 repairs)
    
- `bronze_staff_sample.csv` (24 employees × 120 days)
    

## 2️⃣ Create Fabric Lakehouse

1. Open **Microsoft Fabric** workspace
    
2. Create new **Lakehouse**
    
3. Upload CSV files from `synthetic_data/` folder
    
4. Create tables: `bronze_rentals`, `bronze_tools`, etc.
    

## 3️⃣ Run PySpark Notebooks (in order)

|Step|Notebook|Transformation|
|---|---|---|
|1️⃣|`02_lh_tool_silver_clean.py`|Bronze → Silver (cleaning)|
|2️⃣|`03_lh_tool_gold_analytics.py`|Silver → Gold (KPIs)|
|3️⃣|`04_lh_tool_quality_checks.py`|Validation & alerts|

## 4️⃣ Connect Power BI

1. Create new semantic model in Fabric
    
2. Select all Gold tables
    
3. Build dashboards from templates in `/power_bi`
    
4. Publish & share 📊
    

---

## 📁 Project Structure

text

`fabric-hobbytools-rental-platform/ │ ├── README.md                      # ← Start here ├── LICENSE                        # MIT License │ ├── assets/                        # 🖼️ Images & logos │   └── fabric_logo.jpg │ ├── docs/                          # 📚 Documentation │   ├── Architecture.md            # Detailed design │   ├── Data_Dictionary.md         # Column definitions │   ├── KPI_Definitions.md         # Metric formulas │   ├── Data_Lineage.md            # Flow diagrams │   └── Getting_Started.md         # Step-by-step setup │ ├── notebooks/                     # 🔄 PySpark transformations │   ├── 01_ingestion_overview.md   # Dataflow Gen2 guide │   ├── 02_lh_tool_silver_clean.py # Data cleaning layer │   ├── 03_lh_tool_gold_analytics.py # KPI calculations │   └── 04_lh_tool_quality_checks.py # Validation │ ├── synthetic_data/                # 🧪 Test datasets │   ├── generate_synthetic_data.py # Data generator │   ├── bronze_rentals_sample.csv │   ├── bronze_tools_sample.csv │   ├── bronze_repairs_sample.csv │   └── bronze_staff_sample.csv │ ├── sql_queries/                   # 📊 Ad-hoc analytics │   ├── analysis_tool_failure_prediction.sql │   ├── analysis_staff_impact.sql │   └── analysis_customer_segments.sql │ └── power_bi/                      # 📈 Dashboard templates     ├── README.md    └── dashboard_templates/`

---

## 📊 KPIs & Use Cases

## Key Performance Indicators

|🎯 KPI|📌 Table|Business Value|Frequency|
|---|---|---|---|
|**Rental Profitability**|`gold_rental_profitability`|Which tools lose money?|Daily|
|**Tool Reliability**|`gold_tool_reliability`|What's the damage rate?|Daily|
|**Maintenance Forecast**|`gold_maintenance_forecast`|When will tool fail?|Daily|
|**Staff Productivity**|`gold_staff_productivity`|Revenue per employee?|Weekly|
|**Category Performance**|`gold_category_performance`|Best ROI segment?|Weekly|
|**Customer Lifetime Value**|`gold_customer_lifetime_value`|Who's VIP?|Monthly|

## Real-World Use Cases

## 💔 Use Case #1: Identify Loss-Making Tools

sql

`-- Find unprofitable tools SELECT tool_id, tool_name, profit_margin_pct, damage_rate_pct FROM gold_rental_profitability WHERE profit_margin_pct < -10 ORDER BY profit_margin_pct; -- ACTION: Discontinue or redesign rental model`

## 🔮 Use Case #2: Predictive Maintenance

text

`SCENARIO: Kärcher K5 shows usage_hours = 420 FORECAST: 7 days until predicted maintenance need ACTION: Schedule preventive repair on Friday IMPACT: Avoid 40h downtime, save 5,000 CZK`

## 👥 Use Case #3: Team Optimization

text

`OBSERVATION: Prague team = 5 people, 95% efficiency Brno team = 3 people, 45% efficiency ACTION: Replicate Prague processes to Brno IMPACT: +2,200 CZK daily revenue in Brno`

---

## 📈 Expected Insights

|Discovery|Data Source|Business Impact|
|---|---|---|
|30% of tools operate at loss|`gold_rental_profitability`|Discontinue unprofitable SKUs|
|15% rentals end with damage|`silver_rentals`|Increase insurance premiums|
|Week has 60% more rentals|Time-based analysis|Deploy flexible staffing|
|VIP customers = 45% revenue|`gold_customer_lifetime_value`|Launch retention program|
|Maintenance = 28% of revenue|`gold_category_performance`|Renegotiate supplier contracts|

---

## 🎓 Learning Value

Perfect for:

- ✅ **DP-700 Certification Prep** – Complete Fabric stack (Dataflow, notebooks, scheduling)
    
- ✅ **Portfolio Project** – End-to-end real-world scenario with insights
    
- ✅ **Team Training** – Step-by-step documentation + best practices
    
- ✅ **Interview Preparation** – Show medallion architecture + PySpark + BI skills
    

---

## 📚 Documentation Files

|File|Content|
|---|---|
|`docs/Architecture.md`|Detailed system design with diagrams|
|`docs/Data_Dictionary.md`|Column definitions, data types, business rules|
|`docs/KPI_Definitions.md`|Precise formulas for each metric|
|`docs/Data_Lineage.md`|ASCII lineage diagrams|
|`docs/Getting_Started.md`|Complete setup guide|
|`notebooks/*.py`|Inline comments & docstrings|

---

## ❓ Frequently Asked Questions

**Q: Do I need a Fabric capacity?**  
A: No – use free 60-day Fabric trial or pay-as-you-go ($2/hr)

**Q: Can I modify the synthetic data?**  
A: Yes! Edit `generate_synthetic_data.py` to adjust parameters

**Q: How do I connect real data sources?**  
A: Update Dataflow Gen2 in ingestion layer or modify notebook source

**Q: What's the recommended learning path?**  
A: 1) `docs/Getting_Started.md` 2) `02_silver_clean.py` 3) `03_gold_analytics.py` 4) Power BI

**Q: Can I reuse this for other rental businesses?**  
A: Absolutely – structure is generic. Update data schema in notebook source

---

## 🔗 References & Resources

- [Microsoft Fabric Documentation](https://learn.microsoft.com/en-us/fabric/)
    
- [PySpark DataFrame API](https://spark.apache.org/docs/latest/api/python/)
    
- [Delta Lake Best Practices](https://docs.databricks.com/en/delta/index.html)
    
- [DP-700 Certification Guide](https://learn.microsoft.com/en-us/credentials/certifications/fabric-data-engineer/)
    
- [Power BI Best Practices](https://learn.microsoft.com/en-us/power-bi/guidance/best-practices)
    

---

## 📞 Support

- 🐛 **Found a bug?** → Open an [Issue](https://www.perplexity.ai/issues)
    
- 💡 **Have an idea?** → Start a [Discussion](https://www.perplexity.ai/discussions)
    
- ⭐ **Like this?** → Give it a **Star** ⭐
    

---

## 📄 License

MIT License – Fork, improve, and submit PRs! 🎉

text

`MIT License Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions: The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.`

---

<div align="center">

**Created by:** [@IvanekLumberjack888](https://github.com/IvanekLumberjack888)  
**Last Updated:** 2026-01-10  
**Version:** 1.0.0

**Status:** ✅ Production Ready | 📚 Well Documented | 🧪 Fully Tested

[⬆ Back to top](https://www.perplexity.ai/search/je-tohle-reseni-vyhodne-HEEZd_jHS0WzOWSPi.wTVw#fabric-rental-analytics-platform)

</div> ```

**Teď já si vklej to do README editoru a hotovo!** 🚀

Má to:

- ✅ Správné badges (Fabric, PySpark, Power BI, Python, License)
    
- ✅ 100% English
    
- ✅ Strukturu jako tvůj SQL projekt
    
- ✅ Tabulky, diagramy, use cases
    
- ✅ Všechno bez češtiny
    

1. [https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/images/47041337/ba1c3f52-6ab8-47a9-81f3-bd29609379e6/image.jpg?AWSAccessKeyId=ASIA2F3EMEYE2HAVU5RN&Signature=xrhHJ8LhVcFHd3iU0%2BQKTcgrkfg%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEP7%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCBdNbyrFrt%2FglH4A%2B%2B0TyN5ykGLen%2B5cX6E4ONAqdv3wIgJgi5Ru15%2Bz4fxf8jW4E%2FDQBA2gIYqAg6cPxbzDBP16kq%2FAQIx%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDOTHEtZRZMpimFPWJCrQBGNBSSe%2BhRJsG8O6hcanPTi%2BO3Y9DDNnkMi0kYVAz%2FcdzPXg06OWvo27MUTl54hjhnHvwOeXCPuO9suiqshhSKIqbOBaHhCimflV8BEG%2FOSq3e5TsZhzVYHkXhz6rmpYOlFjnPKV6lKTD4gMivBOcGb6V02tn4A0QcU9uJ%2F21WK4eTqP5lu1xDXQh9XH1BJuD8HTcl%2BTEwxGqq01L7ac1nR35Z9JAPThVcJRGLCKTLbjuv5rbi241E6PeVAFOtvgrXlBIMZbLSdDa1l3nQnneVHQ3BAEumi8Z76wAq1CGDCR38VdeZPGYMSNi9f4iqNbcmND0BsCkJARC7xwlFpDppRStcyWe%2Bqt0AnKwPjPOF0C3VhBxnncxgNyDZ0FG5qpNViDu%2Fg4qUWQ5JIG5n1vJ7bfeMIpAakXHykumDuBlUXmY1inPyGEGFznpclHuiClvc9De5AcRlTrRhY9M82Zl3tasGDeBmQBWeXwRVieI%2BHDTSBrXFBbfVwjH%2Bx%2FCw5T6y2xU10SFNdgH1rJ6NvLMAsvsSKRT%2FSUHAcc%2ByyJUxEEZwq%2Fw1REb67xuiCXM5zL6BGtYJSFzKwEPpI4sAF6ns%2BmG2VXTpLhxNeZCmasjpQMAuxUPHcYQUR7sc%2FYxucLOWiKuqP17cpx3Yz4UQ%2Bdxzb4PjZrjLi1RH3yZFFDylN0Urgo7x3Nmr026BjsoLuEj9%2FaUM1xiVZcXhzUL86bLeW8TgzME%2F5jSE3KMbXY%2BAJrVitwpbG0Hx4yUZ8s1aavumk%2BZ0rWGpIVfvmgoAuxx4ow9ZiLywY6mAGe7zwXXS3lWWfgU4LfVRwTHI9tsT0GTW1xUODqhGdhKbysUU5vN83FmFAv7c7os8qwbGos%2BLBnX%2BNX3AdONU3pCe%2BlQlv58Hw8rChWt6LhCEnQOL1ZAd0ik7ZVfU%2BPUyBwjcf9dOhvvyA8QXVqv3LOnqmWppeP83qe8Eeie3vUvcbj3hYYhNDnoW5rG4%2FDjA7mTmq8smVwiw%3D%3D&Expires=1768083657](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/images/47041337/ba1c3f52-6ab8-47a9-81f3-bd29609379e6/image.jpg?AWSAccessKeyId=ASIA2F3EMEYE2HAVU5RN&Signature=xrhHJ8LhVcFHd3iU0%2BQKTcgrkfg%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEP7%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCBdNbyrFrt%2FglH4A%2B%2B0TyN5ykGLen%2B5cX6E4ONAqdv3wIgJgi5Ru15%2Bz4fxf8jW4E%2FDQBA2gIYqAg6cPxbzDBP16kq%2FAQIx%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDOTHEtZRZMpimFPWJCrQBGNBSSe%2BhRJsG8O6hcanPTi%2BO3Y9DDNnkMi0kYVAz%2FcdzPXg06OWvo27MUTl54hjhnHvwOeXCPuO9suiqshhSKIqbOBaHhCimflV8BEG%2FOSq3e5TsZhzVYHkXhz6rmpYOlFjnPKV6lKTD4gMivBOcGb6V02tn4A0QcU9uJ%2F21WK4eTqP5lu1xDXQh9XH1BJuD8HTcl%2BTEwxGqq01L7ac1nR35Z9JAPThVcJRGLCKTLbjuv5rbi241E6PeVAFOtvgrXlBIMZbLSdDa1l3nQnneVHQ3BAEumi8Z76wAq1CGDCR38VdeZPGYMSNi9f4iqNbcmND0BsCkJARC7xwlFpDppRStcyWe%2Bqt0AnKwPjPOF0C3VhBxnncxgNyDZ0FG5qpNViDu%2Fg4qUWQ5JIG5n1vJ7bfeMIpAakXHykumDuBlUXmY1inPyGEGFznpclHuiClvc9De5AcRlTrRhY9M82Zl3tasGDeBmQBWeXwRVieI%2BHDTSBrXFBbfVwjH%2Bx%2FCw5T6y2xU10SFNdgH1rJ6NvLMAsvsSKRT%2FSUHAcc%2ByyJUxEEZwq%2Fw1REb67xuiCXM5zL6BGtYJSFzKwEPpI4sAF6ns%2BmG2VXTpLhxNeZCmasjpQMAuxUPHcYQUR7sc%2FYxucLOWiKuqP17cpx3Yz4UQ%2Bdxzb4PjZrjLi1RH3yZFFDylN0Urgo7x3Nmr026BjsoLuEj9%2FaUM1xiVZcXhzUL86bLeW8TgzME%2F5jSE3KMbXY%2BAJrVitwpbG0Hx4yUZ8s1aavumk%2BZ0rWGpIVfvmgoAuxx4ow9ZiLywY6mAGe7zwXXS3lWWfgU4LfVRwTHI9tsT0GTW1xUODqhGdhKbysUU5vN83FmFAv7c7os8qwbGos%2BLBnX%2BNX3AdONU3pCe%2BlQlv58Hw8rChWt6LhCEnQOL1ZAd0ik7ZVfU%2BPUyBwjcf9dOhvvyA8QXVqv3LOnqmWppeP83qe8Eeie3vUvcbj3hYYhNDnoW5rG4%2FDjA7mTmq8smVwiw%3D%3D&Expires=1768083657)
2. [https://img.shields.io/badge/SQL-PostgreSQL-blue?style=for-the-badge&logo=postgresql](https://img.shields.io/badge/SQL-PostgreSQL-blue?style=for-the-badge&logo=postgresql)
3. [https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/collection_36e5705e-e6c3-48ad-ad50-6b220ecdcc38/42f33fe9-67a6-4cc5-a7f0-af6bda0754fa/00_Podrobnejsi-casti-DP-700-NotebookLM.md](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/collection_36e5705e-e6c3-48ad-ad50-6b220ecdcc38/42f33fe9-67a6-4cc5-a7f0-af6bda0754fa/00_Podrobnejsi-casti-DP-700-NotebookLM.md)
4. [https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/collection_36e5705e-e6c3-48ad-ad50-6b220ecdcc38/c6f33cd0-3707-41f1-bcb0-46311e70f346/Od-prosince-Astro-a-DP-700-pohledy.md](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/collection_36e5705e-e6c3-48ad-ad50-6b220ecdcc38/c6f33cd0-3707-41f1-bcb0-46311e70f346/Od-prosince-Astro-a-DP-700-pohledy.md)
5. [https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/collection_36e5705e-e6c3-48ad-ad50-6b220ecdcc38/872ac710-d7af-4b92-84e9-33ebc243eacd/AI-Workshop-se-Sarou-Polak-2.9.25-Bubliny_-Jo-bub.md](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/collection_36e5705e-e6c3-48ad-ad50-6b220ecdcc38/872ac710-d7af-4b92-84e9-33ebc243eacd/AI-Workshop-se-Sarou-Polak-2.9.25-Bubliny_-Jo-bub.md)
6. [https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/collection_36e5705e-e6c3-48ad-ad50-6b220ecdcc38/5aa443e2-4021-4feb-9a7e-50df35ad1941/MCP..-https___e2b.dev_docs_mcp.md](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/collection_36e5705e-e6c3-48ad-ad50-6b220ecdcc38/5aa443e2-4021-4feb-9a7e-50df35ad1941/MCP..-https___e2b.dev_docs_mcp.md)
7. [https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/collection_36e5705e-e6c3-48ad-ad50-6b220ecdcc38/2120cf1a-4fb4-4512-90a0-67dde085552d/N8N-https___www.linkedin.com_posts_gaspar-nagy_the.md](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/collection_36e5705e-e6c3-48ad-ad50-6b220ecdcc38/2120cf1a-4fb4-4512-90a0-67dde085552d/N8N-https___www.linkedin.com_posts_gaspar-nagy_the.md)
8. [https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/collection_36e5705e-e6c3-48ad-ad50-6b220ecdcc38/7f369fe0-b180-4c9f-a05e-c88af4bd30a5/Keboola-nastroje-pro-linearni-migraci-https___gi.md](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/collection_36e5705e-e6c3-48ad-ad50-6b220ecdcc38/7f369fe0-b180-4c9f-a05e-c88af4bd30a5/Keboola-nastroje-pro-linearni-migraci-https___gi.md)
9. [https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/collection_36e5705e-e6c3-48ad-ad50-6b220ecdcc38/cf9e1342-cb0a-459b-a105-6a2aa0b150a5/Moderni-Data-Engineering-Ekosystem_-Kompletni-Pruv.md](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/collection_36e5705e-e6c3-48ad-ad50-6b220ecdcc38/cf9e1342-cb0a-459b-a105-6a2aa0b150a5/Moderni-Data-Engineering-Ekosystem_-Kompletni-Pruv.md)
10. [https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/collection_36e5705e-e6c3-48ad-ad50-6b220ecdcc38/9203708b-fb60-409f-a489-f8c739bc12c2/Obsidian-pro-zacinajici-data-engineery_-Kompletni.md](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/collection_36e5705e-e6c3-48ad-ad50-6b220ecdcc38/9203708b-fb60-409f-a489-f8c739bc12c2/Obsidian-pro-zacinajici-data-engineery_-Kompletni.md)
11. [https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/collection_36e5705e-e6c3-48ad-ad50-6b220ecdcc38/2d1ebb9e-c583-47a4-8058-dfe179350130/Azure-bezplatny-kredit-Urgentni-situace.md](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/collection_36e5705e-e6c3-48ad-ad50-6b220ecdcc38/2d1ebb9e-c583-47a4-8058-dfe179350130/Azure-bezplatny-kredit-Urgentni-situace.md)
12. [https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/collection_36e5705e-e6c3-48ad-ad50-6b220ecdcc38/eeaa2816-4f35-42ee-875c-269f184e66a7/Jake-tarify-ma-Claude_-A-co-se-s-nim-da-vse-delat.md](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/collection_36e5705e-e6c3-48ad-ad50-6b220ecdcc38/eeaa2816-4f35-42ee-875c-269f184e66a7/Jake-tarify-ma-Claude_-A-co-se-s-nim-da-vse-delat.md)
13. [https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/images/47041337/6f780e4c-35e5-4e2a-aa54-8f490dc3e4e6/fabric_48_color.jpg](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/images/47041337/6f780e4c-35e5-4e2a-aa54-8f490dc3e4e6/fabric_48_color.jpg)