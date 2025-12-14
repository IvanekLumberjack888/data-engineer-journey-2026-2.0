# 1 Fabric Workspace Settings

Here are a detailed English study notes, with Czech hints for tricky terms.

---

## 1. Spark in Fabric – conceptual overview

Spark in Fabric is a distributed data processing engine used mainly via **Spark Notebooks** for cleaning, transforming and loading data.  
It scales by splitting data across multiple nodes and processing partitions in parallel, which makes it suitable for large datasets and heavy transformations.

---

## 1.1 Starter Pool in Fabric

- When you run a notebook in Fabric without any special configuration, it uses the **Starter Pool** by default.
    
- The Starter Pool is a pre‑configured shared Spark cluster that is “good enough” for small and medium workloads and can autoscale up when needed.
    

Key characteristics:

- **Fast startup time** – a Spark session typically starts in under 10 seconds, because Fabric connects you to a shared 24/7 Spark cluster; billing applies only while your code executes. (rychlý start, sdílený cluster)
    
- **Fixed node size (Medium)** – you cannot change node size on the Starter Pool; for special needs you move to custom pools.
    

Use the Starter Pool when:

- You are developing or testing notebooks.
    
- Your datasets and transformations are moderate in size and complexity.
    

---

## 1.2 When do you need a Custom Spark Pool?

A **Custom Pool** (vlastní Spark pool) gives you more control over compute resources and is useful when the Starter Pool is not sufficient.

Typical use cases:

- **Data size** – very large datasets that cause long runtimes or failures on the Starter Pool.
    
- **Concurrency** – many users or jobs running Spark at the same time, competing for the same capacity; dedicated pools help isolate and control this. (současné běhy / konkurence)
    
- **Variance in job requirements** – some jobs are tiny, some extremely heavy; separate pools with different configurations can be more efficient.
    
- **Job type** – data science / ML model training often needs more memory/cores or GPUs and thus custom Spark settings.
    

---

## 2. Where can Spark be configured in Fabric?

Spark configuration is layered; you can tune it at several levels, each with a different scope.

1. **Capacity level** (úroveň kapacity)
    
    - Your chosen Fabric capacity SKU (e.g. F64) defines the total Spark resources (vCores) available.
        
    - Example: an F64 capacity gives 2 Spark vCores per capacity unit (128 vCores), with the ability to burst up to 3× for short periods (max 384 vCores during peaks).
        
    - Capacity admins can restrict whether workspaces are allowed to create custom pools or even disable Starter Pools.
        
2. **Workspace level** (úroveň pracovního prostoru)
    
    - Default Spark pool and behavior for **all notebooks and Spark jobs in that workspace**.
        
    - Additional settings: concurrency, allocation strategy, default Environment.
        
3. **Environment level** (prostředí)
    
    - Defines job‑specific Spark configs and libraries; multiple environments can exist inside one workspace.
        
    - Notebooks / jobs choose which Environment to run with.
        
4. **Session level** (uživatelská relace)
    
    - Some Spark settings are **mutable** and can be changed dynamically via code (for example with `%%configure`).
        
    - These changes apply only to the current session and are not persisted.
        

---

## 3. Capacity‑level administration (high‑level)

At capacity level you control global Spark resources and some governance around pools.

Key points:

- The capacity SKU determines the **upper limit** of Spark vCores and therefore how much parallel work you can run.
    
- A **Capacity Administrator** can:
    
    - Allow or block workspace admins from creating custom workspace pools.
        
    - Disable Starter Pools for workspaces if a stricter governance model is required.
        

---

## 4. Workspace‑level Spark settings

Workspace Spark settings define the **default behavior** for Spark in that workspace. By default, all notebooks use these settings unless overridden by Environment or session‑level config.

## 4.1 Spark Workspace Setting: Pool

On the **Pool** tab you can:

- **Create and select a Custom Pool** for all Spark items in the workspace.
    
    - Configure:
        
        - **Node size** (velikost uzlu – cores & memory per node).
            
        - **Autoscaling** – on/off and min–max number of nodes.
            
        - **Dynamic Executor Allocation** – on/off and range of executors, to let Spark scale executors based on workload.
            
- **Allow compute customization per item**
    
    - When this is enabled (default), users may adjust some compute settings at session level (e.g. driver/executor cores and memory).
        
    - This gives flexibility but can also cause noisy‑neighbour issues if not governed. (riziko přetížení kapacity)
        

## 4.2 Spark Workspace Setting: Environment

On the **Environment** tab you can:

- Set a **default Environment** for the workspace (výchozí prostředí).
    
- Choose the **Runtime version** – which Spark and Delta Lake versions the workspace uses by default.
    

Environment‑level configs (covered in more detail later) define libraries, engine acceleration, and fine‑grained Spark properties for that environment.

## 4.3 Spark Workspace Setting: Jobs

On the **Jobs** tab you control how Spark sessions are admitted and how long they live.

Key settings:

- **Reserve maximum cores for active Spark jobs**
    
    - By default, Fabric uses **Optimistic Job Admission**, which reserves only the **minimum** cores needed for a job and grows as needed.
        
    - This setting flips behavior: it reserves the **maximum expected** cores up front, which can improve performance consistency but uses more capacity.
        
- **Spark session timeout** (výpadek relace)
    
    - Default: 20 minutes of inactivity. After that, the session is terminated.
        
    - Lower values can save capacity; higher values are more convenient for interactive users.
        

## 4.4 Spark Workspace Setting: High concurrency

High concurrency settings control whether multiple notebooks can share the same Spark application.

You can:

- Enable high concurrency for **Notebooks**.
    
- Enable high concurrency for **Data Pipelines that trigger notebooks**, using **Session Tags** (značky relací) to route runs to shared sessions.
    

Benefits: better utilization when many small notebooks run frequently; risk: contention if poorly configured.

## 4.5 Spark Workspace Setting: Automatic Log

This setting controls automatic logging of ML activities with **MLflow**.

- You can choose whether all ML training activities should be automatically tracked (parameters, metrics, models) for experiments and reproducibility.
    

---

## 5. Environment‑level Spark configuration

An **Environment** (prostředí) packages libraries and Spark settings that can be reused by notebooks and jobs inside a workspace.  
The main idea is: “one environment per job type or project”, with consistent configuration and versioning.

## 5.1 What can you configure in an Environment?

1. **Libraries** (knihovny)
    
    - Install from public sources (e.g. PyPI).
        
    - Install custom libraries from local files (such as `.whl` wheels).
        
2. **Spark settings**
    
    - **Acceleration** – enable the native execution engine to speed up certain workloads.
        
    - **Compute** – specify the pool and low‑level compute configuration (drivers/executors) for this environment.
        
    - **Individual Spark properties** – fine‑grained tuning (e.g. shuffle settings, memory fractions), applied to notebooks and Spark job definitions that use this environment.
        

## 5.2 Pros and cons of Environments

**Pros:**

- Everyone using the same Environment gets **identical configurations and libraries**, which improves reproducibility.
    
- Environments can be **tracked in Version Control** (Git), aligning them with CI/CD processes.
    

**Drawbacks:**

- Environments are **workspace‑scoped** only; you cannot share them across workspaces, which limits reuse.
    
- Publishing or updating libraries (especially from public feeds) can be slow (10+ minutes).
    
- There can be instability with packages (e.g. libraries occasionally disappearing), so environments must be managed carefully.
    

---

## 6. Summary check‑list (for exam and practice)

Use this as a quick mental map:

- Starter Pool for quick start and simple/medium workloads.
    
- Custom Pool when you need specific node sizes, autoscaling ranges, or isolation by job type/concurrency.
    
- Capacity level defines global limits and admin guardrails.
    
- Workspace level sets defaults: pool, environment, jobs behavior, concurrency and logging.
    
- Environment level standardizes libraries and Spark settings per job type and can be version‑controlled.
    
- Session level allows temporary overrides for advanced tuning or experimentation.
    

---

## 1.2 Domain workspace settings – core idea

A **Domain** is a logical grouping of data and workspaces that belong to the same business area (e.g. Sales, Finance, HR).  
Domains help users find content in the OneLake Catalog more easily and allow limited governance delegation from central IT to domain‑level admins. (delegace správy)

High‑level workflow:

- Design business domains that reflect how the organization is structured (by department, region, function).
    
- Assign Fabric workspaces into these domains using clear rules.
    
- Gradually delegate some configuration and governance tasks to **Domain Admins**, while central **Fabric Admins** keep overall control.
    

---

## Domain‑related roles

There are three key roles tied to domains in Fabric.

- **Fabric Admin**
    
    - Manages the overall Fabric tenant, including creating and deleting domains.
        
    - Controls global governance policies and who can be Domain Admin.
        
- **Domain Admin**
    
    - Manages settings and workspace assignments **inside a specific domain**.
        
    - Can add/remove workspaces, adjust domain‑level options where delegation is allowed.
        
- **Domain Contributor**
    
    - Has more limited permissions within the domain (for example, contributing content or managing some metadata), but not full domain administration.
        

---

## Assigning workspaces to a Domain – three methods

There are **three ways** to link a workspace to a Domain.

1. **Within Domain Settings**
    
    - In the Domain configuration, you can add workspaces using different criteria:
        
        - **By workspace name** – directly select one or more workspace names.
            
        - **By workspace admin** – automatically include all workspaces owned/managed by specific admins.
            
        - **By capacity** – include all workspaces running on a particular capacity.
            
2. **Within Workspace Settings**
    
    - Open the specific workspace and choose which Domain it belongs to.
        
    - Good when a workspace owner wants to explicitly attach their workspace to the correct business domain.
        
3. **Default Domain assignment**
    
    - Automatic assignment based on internal heuristics (e.g. workspace metadata, creator, location).
        
    - Useful to reduce manual work, but you should still review how the logic behaves in your tenant and adjust if needed.
        

---

## Important note: Purview vs Fabric Domains

- **Domains in Microsoft Purview** and **Domains in Fabric** are currently independent; they do **not** integrate or share configuration.
    
- This means you must create and manage domain structures **separately** in Purview and in Fabric for now.
    

---

## Moderator / self‑check questions for NotebookLM

Use these to quiz yourself after listening to a video or audio summary.

1. **Concept & purpose**
    
    - What is a Domain in Microsoft Fabric and how does it help with data governance and discoverability?
        
    - Why would an organization group workspaces into Domains rather than managing everything only at tenant level?
        
2. **Roles**
    
    - What are the responsibilities and permissions of a Fabric Admin compared to a Domain Admin?
        
    - In which situations would you assign someone the Domain Contributor role instead of Domain Admin?
        
3. **Workspace assignment**
    
    - Describe the three different ways to assign workspaces to a Domain.
        
    - In what scenario would you prefer to assign workspaces by **workspace name**?
        
    - When might it be more efficient to assign workspaces by **workspace admin** or by **capacity**?
        
4. **Default Domain assignment**
    
    - What is the purpose of Default Domain assignment and what are potential risks if you rely on it without review?
        
    - How would you verify that automatic assignment is correctly reflecting your organization’s domain design?
        
5. **Integration with other tools**
    
    - How do Domains in Fabric relate to Domains in Microsoft Purview today?
        
    - What governance implications does it have that you must currently manage domains separately in Purview and Fabric?
        
6. **Design & exam‑style thinking**
    
    - Given a company with Finance, Sales and HR departments, how would you design a Domain structure and workspace‑to‑domain assignment strategy?
        
    - In an exam scenario, if the requirement is to **delegate some governance to business teams while keeping central oversight**, which role/domain combination would you choose and why?
        

---

## 1.3 OneLake workspace settings – core concepts

OneLake is the unified data lake for Fabric; some items automatically store their data there, others do not unless you turn on integration.  
Workspace‑level settings mainly affect how users can access OneLake data (OneLake File Explorer) and which items expose their tables into OneLake.

---

## OneLake File Explorer

- OneLake File Explorer exposes OneLake on your local machine similarly to how OneDrive shows document libraries. (OneLake průzkumník)
    
- It is useful for business users who want to drag‑and‑drop files into a Lakehouse or download data out of it.
    

To use it, two conditions must be met:

- A **Fabric admin** must enable the tenant setting:  
    “Users can sync data in OneLake with the OneLake File Explorer.”
    
- The user installs the OneLake File Explorer client on their computer.
    

What you see by default in OneLake File Explorer:

- **Lakehouse** and **Data Warehouse** items, because these store their data in OneLake natively.
    
- **You do NOT see** Power BI semantic models or KQL databases by default, because their data is not automatically written into OneLake.
    

---

## OneLake integration for KQL databases

- Each KQL database (Eventhouse / KQL DB) has a setting to enable **OneLake integration**.
    
- Turning it on causes KQL tables to appear as OneLake tables, so other Fabric experiences can access them (e.g. via shortcuts).
    

Important exam nuance:

- Microsoft later added **backfill** support: when you enable OneLake availability, existing tables can now be written into OneLake as well.
    
- DP‑700 questions may still reflect the older behavior (no backfill), so for the exam you should assume the documented exam‑era behavior (no automatic historical backfill).
    

---

## OneLake integration for Power BI semantic models

To expose semantic model data into OneLake, there are **two levels of configuration**.

1. **Tenant‑level setting** (správa na úrovni tenant):
    
    - Fabric / Power BI admin must enable:  
        “Semantic models can export data to OneLake.”
        
2. **Item‑level setting** on each semantic model:
    
    - In the model’s Settings, you explicitly turn on **OneLake integration**.
        

Benefits once enabled:

- Tables from the semantic model become visible in OneLake, which allows:
    
    - Creating **shortcuts** to semantic model tables from a Lakehouse.
        
    - Re‑using curated semantic data in other Fabric experiences without duplicating ETL.
        

---

## Shortcut caching (OneLake shortcuts to external storage)

Shortcuts let you reference external data (e.g. AWS S3, GCS) as if it lived in OneLake, without copying it. (zkratky na externí úložiště)  
**Shortcut caching** is an optimization to reduce cross‑cloud egress costs and improve performance when repeatedly reading external files.

Key DP‑700 rules to remember:

- Caching applies **only** when the shortcut points to:
    
    - Google Cloud Storage
        
    - Amazon S3 or S3‑compatible locations
        
- **24‑hour rule (exam‑relevant)**:
    
    - If a cached file is not accessed for more than 24 hours, it is removed from the cache.
        
    - The next access after 24 hours reads from the original source again (and may re‑cache it).
        
- **1 GB rule**:
    
    - Individual files larger than **1 GB** are **not cached**.
        

Even though Microsoft later introduced configurable retention up to 28 days, DP‑700 questions are likely still written with the simple 24‑hour rule; answer accordingly for the exam.

---

## Quick self‑check questions (for NotebookLM or Obsidian)

1. What tenant‑level setting must be enabled before users can use OneLake File Explorer to sync data?
    
2. Which Fabric items are visible in OneLake File Explorer by default, and which are not?
    
3. What does enabling OneLake integration do for a KQL database?
    
4. What two configuration steps are required to enable OneLake integration for a Power BI semantic model?
    
5. Why might you want to shortcut a semantic model table into a Lakehouse?
    
6. For shortcut caching, which external storage types are supported?
    
7. What is the **24‑hour rule** for shortcut caching and how does it affect where data is read from?
    
8. What is the **1 GB rule** in the context of shortcut caching?
    
9. In an exam question that mentions “shortcut caching” and “files not accessed for more than a day”, what behavior should you describe?
    

---

## 1.4 Apache Airflow job – core idea

The **Apache Airflow job** (previously _Data Workflow_) is a Fabric item (preview) that lets you run **Apache Airflow DAGs** as a managed service inside Fabric.  
You focus on authoring Python‑based DAGs; Fabric hosts and operates the Airflow runtime, similar in spirit to how Data Pipelines are managed for you.

Key contrast:

- **Data Pipeline** – low‑code / visual orchestration.
    
- **Apache Airflow job** – code‑first orchestration with Python DAGs (directed acyclic graphs).
    

---

## Managed Airflow in Fabric vs. self‑hosted Airflow

Traditionally you must:

- Provision and manage Airflow servers or use a SaaS provider like Astronomer.
    
- Handle upgrades, scaling, high availability and monitoring yourself.
    

In Fabric:

- Airflow is offered as a **managed service**; you do **not** deploy servers or a separate SaaS.
    
- You only configure and maintain your DAGs and some runtime settings; Fabric owns the infrastructure side.
    

---

## Workspace‑level Apache Airflow runtime settings

Airflow runtime is configured in **Workspace Settings**, in the section **Apache Airflow runtime settings**.  
Here you decide how the Airflow jobs in this workspace will run.

Two options:

1. **Starter Pool (default)**
    
    - A shared, pre‑configured Airflow pool provided by Fabric.
        
    - Suitable for experimentation, small workloads and simple DAGs.
        
2. **Custom Airflow pool**
    
    - A dedicated Apache Airflow pool (not the same as a Spark pool).
        
    - You define runtime characteristics (e.g. size/throughput/concurrency) appropriate for your DAG workload.
        

Important nuance:

- **Airflow pool ≠ Spark pool** – they are different compute concepts, even though both are configured at workspace level.
    
- For the exam, expect questions that check whether you can distinguish **Spark configuration** from **Airflow runtime configuration**.
    

---

## How to think about Airflow pools (for DP‑700 scenarios)

Use **Starter Pool** when:

- You are testing or prototyping DAGs.
    
- You have light, non‑critical workloads.
    

Use a **custom Airflow pool** when:

- You need predictable resources and isolation for production DAGs.
    
- You run many Airflow jobs concurrently and want to control concurrency and scaling explicitly.
    

---

## Self‑check / moderator questions

You can feed these to NotebookLM or use them as flashcards:

1. What is an **Apache Airflow job** in Microsoft Fabric and how does it differ from a classic Data Pipeline?
    
2. Why is Airflow in Fabric considered a **managed service**, and what operational tasks does this remove from your responsibility?
    
3. Where in Fabric do you configure **Apache Airflow runtime settings** for a workspace?
    
4. What is the difference between using the **Starter Pool** and creating a **custom Airflow pool**?
    
5. Why is it important to recognize that an **Airflow pool is not a Spark pool** in exam questions?
    
6. In what kind of scenario would you recommend a **custom Airflow pool** instead of the Starter Pool?
    
7. If a question mentions Python‑based orchestration using DAGs inside Fabric, which feature is it likely referring to?
    

---
---

# 2 LIFECYCLE MANAGEMENT

## 2.1 Configure Version Control – core idea

Version control in Fabric means connecting a **workspace** to a **Git repository** (Azure DevOps or GitHub) so that changes to items are tracked as code.  
For DP‑700 you need to know required tenant settings, how the connection works, and **what is / is not committed** to Git.

---

## Tenant‑level settings (Fabric admin)

Before any workspace can sync to Git, a **Fabric tenant admin** must enable specific settings.

Key options:

- “Users can synchronize workspace items with their Git repositories.”
    
- If using GitHub: “Users can sync workspace items with GitHub repositories.”
    
- Optional but relevant: “Users can export items to Git repositories in other geographical locations.” (cross‑region export)
    

Exam angle: if a scenario says “users cannot connect workspaces to Git”, check tenant‑level permissions first.

---

## Connecting a workspace to Azure DevOps Git

When linking a Fabric workspace to **Azure DevOps (ADO)**, you must specify:

- ADO **Organization**.
    
- ADO **Project**.
    
- **Repository** within that project.
    
- **Branch** to sync with.
    
- Optional: **folder path** – if set, workspace content is written into that subfolder; if empty, it goes to the repo root.
    

Fabric then writes definitions of supported items into the repo; changes can be committed, reviewed (PRs) and deployed.

---

## Connecting a workspace to GitHub

For **GitHub** integration, configuration is slightly different:

- **Display name** for the connection (any friendly name).
    
- **Personal Access Token (PAT)** generated in GitHub with appropriate scopes.
    
- **Repository URL** (including owner/name).
    

Once connected, Fabric syncs supported item definitions to that repo and branch, similar to ADO.

---

## What gets committed to version control?

DP‑700 expects you to know that not everything in Fabric is stored in Git.

General rules:

- **NOT committed**:
    
    - Tabular **data** in data stores or semantic models (no actual data rows).
        
    - **Files** (e.g. Lakehouse files area, Environment files).
        
    - **Refresh schedules**.
        
- **Data Warehouse**:
    
    - The **structure** of the warehouse (CREATE TABLE / CREATE VIEW etc.) is committed as code.
        
    - A **SQL Project** representation of the warehouse is also checked in (ties into database projects later).
        
- **Lakehouse**:
    
    - Only **metadata** like name and description is versioned; actual files/data are not.
        

Implication (very exam‑relevant):

> If something is **not** in version control, it typically also **cannot be deployed** via standard CI/CD and deployment pipelines.

---

## Self‑check / moderator questions

You can use these as NotebookLM prompts or flashcards:

1. Which **tenant‑level settings** must be enabled before users can connect a Fabric workspace to Git?
    
2. What specific fields are required to connect a workspace to an **Azure DevOps** Git repository?
    
3. What credentials and information are needed to connect to **GitHub** from a Fabric workspace?
    
4. Name three things that **do NOT** get checked into version control from a Fabric workspace.
    
5. What aspects of a **Data Warehouse** are stored in version control, and why is this important for CI/CD?
    
6. What is actually committed for a **Lakehouse** when syncing to Git?
    
7. In an exam scenario, if the requirement is “deploy warehouse schema changes between environments using CI/CD”, which artifact must exist in Git?
    
8. How would you explain to a stakeholder why data rows themselves are not stored in Git, only definitions and code?
    

---
## 2.3 Deployment Pipelines – core idea

Deployment Pipelines move (copy) supported Fabric items through **stages** like DEV → TEST → PROD, where each stage is a separate Fabric workspace.  
Goal: enforce a way of working where content is tested before reaching Production, either manually or via REST API‑driven automation.

---

## Key exam concepts

- **Stages**
    
    - 2–10 stages per pipeline; each stage maps to one workspace (names are arbitrary: Dev/Test/Prod/UAT, etc.).
        
    - Deploying means copying items from one stage’s workspace to the next stage’s workspace.
        
- **Item pairing**
    
    - When an item is first deployed from Stage A to Stage B, a hidden pairing link is created.
        
    - Even if you rename items later, the pairing remains; subsequent deployments overwrite the paired item in the target stage.
        
- **Auto‑binding**
    
    - Some items are auto‑bound to dependencies during deployment.
        
    - Examples:
        
        - Reports auto‑bind to their semantic models.
            
        - Notebooks auto‑bind to their default Lakehouse and Environment.
            
    - Result: you often cannot deploy just one item; its bound dependency is deployed or re‑bound as well.
        
- **Deployment Rules**
    
    - Rules that automatically adjust settings/parameters when deploying between stages.
        
    - Used to switch connections (e.g. Dev DB → Test DB → Prod DB), change Lakehouse, or other environment‑specific configs without manual edits.
        

---

## Supported Fabric items (high‑level)

Deployment Pipelines support many item types, including (preview where noted):

- Dashboards, Reports, Paginated reports, Real‑time Dashboards.
    
- Semantic models (from .pbix, non‑PUSH).
    
- Data pipelines (preview), Dataflows Gen2 (preview), Datamarts (preview).
    
- Lakehouse (preview), Warehouse (preview), SQL database (preview), Mirrored database (preview).
    
- Notebook, Environment (preview), Eventhouse/KQL database, Eventstream (preview), KQL Queryset.
    
- Activator, Org apps (preview), Power BI Dataflows.
    

For DP‑700, you mainly need to know **they exist and are supported**, not every nuance per item.

---

## What actually gets deployed?

Same rule as with Version Control: **if something is not written to Git, it is not deployed between stages.**

- **NOT deployed:**
    
    - Tabular **data** in data stores or semantic models (only definitions move, not rows).
        
    - **File data** (Lakehouse files area, Environment files, etc.).
        
    - **Refresh schedules** – must usually be configured manually in Production and are not easily scripted with current REST APIs.
        
- **Data Warehouse:**
    
    - **Schema/structure** (tables, views, etc.) is deployed, but data is not.
        
- **Lakehouse:**
    
    - Lakehouse **tables and files are not deployed** between stages.
        

Exam‑relevant principle:

> If you need data in each stage, you must load it there (e.g. via pipelines), not rely on the deployment pipeline to move data.

---

## Deployment Pipelines API (for automated CI/CD)

While the UI allows any user to promote content between stages, you can also automate deployments via REST APIs.

Key endpoint:

- **Deploy Stage Content** – deploys items from a specified stage of a pipeline.
    
    - Can deploy **all items** in that stage or a **selected subset**.
        
    - Uses **List Deployment Pipeline Stages** to find stage IDs.
        
    - Integrated with **Long Running Operations** APIs to check operation state and results for up to 24 hours after completion.
        

This enables hybrid patterns: simple manual deployments for day‑to‑day work, plus scripted deployments embedded in a CI/CD pipeline when needed.

---

## Self‑check / moderator questions

1. What is a **Deployment Pipeline** in Fabric and how does it relate to workspaces and stages?
    
2. How does **item pairing** work and what happens if you rename an item in one of the stages?
    
3. Explain **auto‑binding** in the context of reports, semantic models, notebooks and Lakehouses. When can auto‑binding surprise you?
    
4. What are **Deployment Rules** used for and give an example of a typical rule between Dev, Test and Prod.
    
5. Name at least five different Fabric item types that are supported by Deployment Pipelines.
    
6. List three things that **do not get deployed** between stages and explain why.
    
7. What gets deployed for a **Data Warehouse**, and what does **not**?
    
8. How would you ensure data exists in Test and Prod stages if Deployment Pipelines do not move data?
    
9. Which REST API operation allows you to deploy content from one stage to another, and how do you monitor its progress?
    

---

## 2.2 Implement database projects – core idea

A **Database Project** is a way to manage a Fabric **Data Warehouse schema as code**, so you can deploy changes reliably across environments using CI/CD.  
It is an additional option next to Deployment Pipelines; the big advantage is that the technology and tooling (SQL projects + DACPAC) have been proven in SQL Server world for many years.

---

## How Fabric uses Database Projects

- When you connect a Fabric **Data Warehouse** to Git, the warehouse is stored in the repo as a **SQL Database Project** automatically.
    
- The project contains the warehouse schema (tables, views, etc.) in a structured, file‑based format that can be edited, built and deployed.
    

This setup enables:

- **Code review** of schema changes in PRs.
    
- **Automated builds** and **deployments** via Azure Pipelines.
    

---

## Typical workflow with SQL Database Projects (VS Code)

A common manual/semiautomated process looks like this:

1. **Clone** your Azure DevOps repository locally.
    
2. **Install** the **SQL Database Projects** extension in VS Code.
    
3. **Open/connect** the local Database Project in VS Code using the extension.
    
4. **Modify** the warehouse schema in the project (add/alter tables, views, etc.).
    
5. **Build** the project to create a **DACPAC** file (Data‑tier Application Package).
    
6. **Publish** the DACPAC to a Fabric Data Warehouse (manual or via Azure Pipeline).
    

In a proper CI/CD pipeline:

- A developer commits changes to Git.
    
- Azure Pipelines automatically triggers: build Database Project → produce DACPAC → deploy DACPAC to the target warehouse.
    

---

## Why DACPAC and Database Projects matter (exam view)

- A **DACPAC** is a packaged representation of the desired database schema that deployment tools can compare with the target and generate the necessary changes (diff deploy).
    
- It provides a consistent and repeatable way to roll schema changes through Dev → Test → Prod without manually scripting all ALTER statements.
    

Key points to remember:

- Database Projects + DACPAC are the **primary mechanism** when the question is about _automated, repeatable schema deployment_ for Fabric Data Warehouses.
    
- Deployment Pipelines move Fabric items between workspaces, but Database Projects give you **fine‑grained control over schema evolution** and fit naturally into Azure Pipelines‑based CI/CD.
    

---

## Self‑check / moderator questions

1. What is a **Database Project** in the context of a Fabric Data Warehouse, and how does it relate to Git?
    
2. Why might you choose **Database Projects + DACPAC** instead of relying only on Deployment Pipelines for warehouse changes?
    
3. Describe the typical VS Code‑based workflow for changing a Fabric Data Warehouse schema using a Database Project.
    
4. What is a **DACPAC** and how is it used in CI/CD for database deployments?
    
5. In an automated pipeline, what are the main steps that happen after a developer commits a schema change to Git?
    
6. In an exam scenario asking for a “reliable, automated way to promote Data Warehouse schema changes across environments”, which combination of tools would you propose and why?
    

---
---

# 3 Security and Governance

## 3.1 Workspace-level access controls – core idea

Workspace access is granted to **users or groups (Entra ID / M365)**, and this access applies to **everything inside that workspace** unless overridden at item level.  
When you share a workspace, you always assign one of the **workspace roles**: Admin, Member, Contributor, or Viewer.

---

## Workspace roles and precedence

- The **creator** of a workspace automatically becomes a **Workspace Admin**.
    
- If a person has multiple role assignments (e.g. via several security groups), the **highest role wins**.
    

High‑level capabilities (you do not need the full table for DP‑700, just the gist):

- **Admin** – full control: manage workspace, roles, settings, and all items.
    
- **Member** – can create, edit, delete most items and publish content.
    
- **Contributor** – can create and edit some content, but with more restrictions than Member.
    
- **Viewer** – read‑only access, can view and interact with reports/dashboards but not edit.
    

For exact capabilities per role, Microsoft has an official table, but DP‑700 usually tests whether you conceptually know who can **manage** vs. who can **edit** vs. who can only **view**.

---

## Self-check / moderator questions

You can use these in NotebookLM or Obsidian:

1. When you share a workspace with a user or Entra ID security group, what are you actually assigning to them?
    
2. What are the four workspace‑level roles in Fabric and, at a high level, what kind of permissions does each imply?
    
3. Who becomes **Admin** of a new workspace by default, and how can this be changed later?
    
4. If a user is both in a Viewer group and a Member group for the same workspace, which role is effective and why?
    
5. In an exam scenario, which role would you assign to:
    
    - someone who should **manage access and settings** for the workspace?
        
    - someone who should **build and publish reports and datasets**?
        
    - someone who should **only consume reports and dashboards**?
        

---

## 3.2 Item-level access controls – core idea

Item-level access is used when you **do not want to give someone access to everything in a workspace**, but only to specific objects (items).  
Almost all Fabric items support item-level sharing, except **Data Pipelines** and **Dataflows**, which still rely on workspace-level access.

---

## How item-level sharing works

- Each item type (Warehouse, Lakehouse, Report, Semantic model, etc.) has its **own specific set of permissions** when you share it.
    
- When you grant item-level access, the user or group can find that item via the **OneLake data hub**, even if they do not have workspace access.
    

Practical use:

- Use item-level sharing to expose **only the needed objects** to consumers or partner teams, while keeping the rest of the workspace isolated.
    

---

## Example: Data Warehouse item permissions

When you share a **Data Warehouse** at item level, you see several permission checkboxes; they layer on top of each other.

- **Read** (no extra boxes checked)
    
    - User can see the Warehouse in OneLake data hub, but **no access to any tables** by default.
        
    - This is useful if you plan to assign **granular T‑SQL permissions** later (e.g. object-level security).
        
- **ReadData**
    
    - Grants read access to **all tables** in the Warehouse via the **T‑SQL endpoint**.
        
- **ReadAll**
    
    - Extends ReadData: user can also read the **underlying OneLake files**, so data is available to other engines (e.g. Spark).
        
- **Build**
    
    - Allows the user to **build reports** on top of the **default semantic model** generated by the Warehouse.
        

For DP‑700 you mainly need to distinguish:

- Read vs ReadData vs ReadAll.
    
- Build as the permission required to create reports on the Warehouse model.
    

---

## Self-check / moderator questions

1. Why would you use **item-level access** instead of giving someone workspace-level access?
    
2. Which Fabric items **do not** currently support item-level sharing and still require workspace‑level permissions?
    
3. What does a user actually gain if you share a Warehouse with them at **Read** level only?
    
4. How does **ReadData** differ from **ReadAll** for a Warehouse item?
    
5. Which permission must a user have to **build reports** on top of a Warehouse’s default semantic model?
    
6. In a scenario where a data engineer wants Spark access to Warehouse data without workspace access, which Warehouse permission is needed and why?
    

---

## 3.3 RLS / CLS / OLS / File-level access – core principles

Granular security in Fabric is always applied **per engine** (Warehouse, Lakehouse, KQL, Semantic model, etc.), and high‑level access (workspace / item) can **override** granular rules.  
For DP‑700 you must understand how to implement **RLS** (row‑level), **CLS** (column‑level), **OLS** (object‑level) in a Warehouse, and **file‑level access** in a Lakehouse.

---

## RLS in Data Warehouse – 3‑step pattern

Prerequisite: the user/role must already have access to the table via either: workspace Viewer, item‑level ReadData, or object‑level security.

Implementation pattern:

1. (Optional) Create a dedicated **Security schema** to keep all security objects together.
    
2. Create a **T‑SQL inline table‑valued function** that returns allowed rows based on the logged‑in user (`USER_NAME()`).
    
3. Create a **SECURITY POLICY** that applies the filter predicate to the target table.
    

Exam takeaway: RLS in Warehouse is implemented through **security policies + filter functions**, not via simple WHERE clauses in views.

---

## CLS & OLS in Data Warehouse

Prerequisite for CLS/OLS demo pattern: the user/role should have **Read** permission only at item level on the Warehouse (no workspace role).

- **OLS (Object‑Level Security)** – control access at table level.
    
    - Grant `SELECT` on specific tables to a role/user (e.g. `GRANT SELECT ON Sales.Orders TO [SalesReps];`).
        
    - Users see only allowed tables; others are effectively hidden.
        
- **CLS (Column‑Level Security)** – control access at column level.
    
    - Grant `SELECT` on **specific columns** in a table to a role/user (e.g. `GRANT SELECT ON Sales.CustomerDetails (CustomerId, AccountCreationDate) TO [SalesReps];`).
        
    - Sensitive columns not granted are not visible.
        

Key principle: combine **Read** at item level with precise `GRANT` statements to implement CLS/OLS.

---

## File-level access for Lakehouse (preview)

Workspace Admins, Members and Contributors can define **folder‑level roles** for Lakehouse tables/files.

Pattern:

1. Define a **role** and select which **tables and files/folders** it can access.
    
2. Add **users or groups** to that role.
    

This uses the **OneLake data access model** and gives RBAC‑style control over which folders in the Lakehouse users can read/write, separate from workspace roles.

`%%text` 
#### `RBAC‑style = **Role-Based Access Control**, česky „řízení přístupu založené na rolích“.`

##### `Co to znamená`

- `Neuděluješ oprávnění jednotlivým uživatelům „kus po kuse“, ale nejdřív vytvoříš **roli** (např. SalesReaders, DataEngineers), té roli přiřadíš oprávnění, a **uživatele jen přidáváš do rolí**.`
    
- `Uživatel tak nepřímo zdědí všechna práva, která má daná role – jednodušší správa i audit, hlavně ve velkých týmech.`
    

##### `Proč je to důležité ve Fabricu`

- `Stejný princip používáš u **Warehouse CLS/OLS** (role + GRANT SELECT) i u **Lakehouse file-level access** (role + povolené složky/tabulky).`
    
- `Když se změní tým nebo přijdou noví lidi, jen je přesuneš mezi rolemi, nemusíš editovat stovky individuálních přístupů.`
    


---

## Critical exam warnings

- If you give users **higher‑level access** (e.g. workspace Contributor or item‑level wide permissions), they can bypass your fine‑grained RLS/CLS/OLS/file rules.
    
- You must define access **for each engine** plus again in the **semantic model**; securing only the Warehouse is not enough if users query via Power BI model.
    
---

## 3.4 Dynamic Data Masking – core behavior

- When a user runs a T‑SQL query on a masked column, they see a masked value; the real value stays unchanged in storage.
    
- Users with high‑privilege roles (e.g. db_owner / elevated permissions) can still bypass or inspect unmasked data, hence DDM is a **privacy/convenience feature**, not a full security boundary.
    

You apply masks **per column**, either:

- At table creation with `CREATE TABLE ... MASKED WITH (FUNCTION = '...')`, or
    
- Later with `ALTER TABLE ... ALTER COLUMN ... ADD MASKED WITH (FUNCTION = '...')`.
    

---

## Four mask function types

1. **Default mask**
    
    - Generic full masking, format depends on data type (e.g. strings become Xs, numbers 0).
        
    - Syntax example: `Phone varchar(12) MASKED WITH (FUNCTION = 'default()')`.
        
2. **Email mask**
    
    - Shows first letter + generic domain, e.g. `aXXX@XXXX.com`.
        
    - Syntax example: `Email varchar(100) MASKED WITH (FUNCTION = 'email()')`.
        
3. **Random mask (for numeric types)**
    
    - Returns a random value in a specified numeric range.
        
    - Example: `Account_Number bigint MASKED WITH (FUNCTION = 'random(1000, 9999)')`.
        
4. **Custom String / Partial mask**
    
    - Shows prefix and/or suffix, masks the middle with a pattern string.
        
    - Generic syntax: `MASKED WITH (FUNCTION = 'partial(prefix,[padding],suffix)')`.
        
    - Example: `ALTER COLUMN [PhoneNumber] ADD MASKED WITH (FUNCTION = 'partial(1,"XXXXXXX",0)')`.
        

Special note:

- **DATETIME** has no dedicated mask; using `default()` will show `1900‑01‑01 00:00:00` for all values.
    

---

## Relationship to RLS / CLS / OLS

- DDM should **always be used together** with proper access controls (RLS/CLS/OLS), not as a standalone security measure.
    
- It is relatively easy to work around if a user already has broad query capabilities, so think of it as **data obfuscation for less‑privileged roles**, not a hard security wall.
    
Dynamic Data Masking (DDM) changes **how data is shown in query results**, not the underlying stored values.  
In Fabric, it works in **Data Warehouse** and **Lakehouse SQL endpoint** for T‑SQL queries and must always be combined with RLS/CLS/OLS, not used as the only protection.

---

## 3.5 Apply sensitivity labels to items – core idea

- Applying a label to a Fabric item signals how it should be handled (sharing, export, encryption, warnings, etc.).
    
- In some regulated industries, using labels is required for compliance with information protection regulations.
    

Typical examples:

- Label a semantic model containing personal data as **Confidential**.
    
- Label a public, non‑sensitive report as **Public** or **General**.
    

---

## Relationship to Domains and default labels

- One of the **Domain‑level settings** in Fabric allows you to specify a **default sensitivity label for that domain**.
    
- This means that new items created in that domain can automatically inherit a baseline label (for example, all Finance domain items start as _Confidential_).
    

This ties domain‑based data organization directly to information protection policies from Purview.

Sensitivity labels are a **data governance / information protection** feature that classify how sensitive a Fabric item is (e.g. _Public, Internal, Confidential, Highly Confidential_).  
They are created and centrally managed in **Microsoft Purview**, and then applied to Fabric items like semantic models, reports or datasets.

---

## Admin prerequisites

- A Fabric admin must enable:
    
    - **Item certification** in the Admin Portal.
        
    - **Master data endorsement** in the Admin Portal.
        
- Only then can users see and use **Certified** and **Master data** badges in the UI.
    

---

## Promoted

- Meaning: item is **ready for sharing and reuse**, as judged by its creators.
    
- Who can apply: **any user with write permissions** on the item.
    
- Scope: all Fabric and Power BI items **except Power BI dashboards** can be promoted.
    

Use case: mark “good, but not formally approved” content so others know it is suitable for broader use.

---

## Certified

- Meaning: item **meets the organization’s quality standards** and is considered reliable and authoritative across the org.
    
- Who can request: **any user** can request certification.
    
- Who can approve/apply: only **users designated by a Fabric admin** (certifiers).
    

Use case: official, governed datasets/reports that business users should prefer over ad‑hoc versions.

---

## Master data

- Meaning: item is a **core, authoritative source of organizational data** – a “single source of truth” for things like product codes or customer lists.
    
- Scope: only items that **contain data** (e.g. Lakehouse, semantic model) can be labeled as Master data.
    
- Who can apply: only **specific users configured by the Fabric admin** in tenant settings.
    

Use case: signal which data objects are the master source to be used by downstream systems and reports.

Item endorsement is a **governance signal** that marks which Fabric items are recommended or authoritative for reuse: **Promoted**, **Certified**, or **Master data**.  
Whether you can use these badges at all depends on **tenant settings** that Fabric admins must enable first.

---
---

# 4 Orchestration

## 4.1 Orchestration 🎼
## 4.1.1 With Data Pipeline – core idea

For DP‑700, the **primary orchestration tool** you must know is the **Data Pipeline**.  
It is a low/no‑code orchestrator that can control almost any Fabric item plus many external services (Databricks, ADF, Functions, REST APIs, etc.).

---

## Data Pipeline as orchestrator

- Pipelines let you chain activities into a workflow: ingest, transform, load, notify, call external systems.
    
- Compared to notebook‑based orchestration, pipelines are more declarative, visual and easier for mixed teams (data engineers + analysts).
    

Typical orchestration actions:

- Run Copy Data activities.
    
- Trigger notebooks, stored procedures, REST endpoints.
    
- Branch logic based on success/failure, outputs or conditions.
    

---

## Copy Data activity – main ingestion mechanism

Copy Data is the **main activity for ingesting data into Fabric** via pipelines.

**Sources** (examples):

- On‑prem SQL and other DBs via on‑premises data gateway.
    
- Most Azure services, major cloud storage providers.
    
- REST APIs with basic pagination.
    
- HTTP endpoints and open web data.
    

**Destinations**:

- **File data** → Lakehouse **Files** area.
    
- **Table data** → any Fabric data store (Lakehouse tables, Warehouse, KQL DB, etc.).
    
- Many external data stores as sinks.
    

---

## Dependencies between activities

Activities are connected with **dependency conditions** that control flow:

- **On Success** – run next activity only if previous one succeeded.
    
- **On Fail** – run next activity only if previous one failed (e.g. send alert).
    
- **On Skip** – run next activity only if previous one was skipped.
    
- **On Completion** – run next activity after previous one finishes, regardless of outcome.
    

This allows classic patterns: retry branches, notification flows, cleanup steps, etc.

---

## Active vs Inactive activities

- Activities can be marked **Active** or **Inactive**.
    
- Inactive activities remain in the pipeline design but do not execute, which is useful for temporarily disabling steps without deleting them.
    
---

## 4.1.2 Orchestration with Notebook – core idea

A Fabric **Notebook** can act as an orchestrator by calling other notebooks via the `notebookutils` package.  
This lets you build custom flows in Python, either **in parallel** or via a simple in‑code **DAG (directed acyclic graph)** definition.

---

## Parallel execution with `runMultiple`

- Import helper: `from notebookutils import notebook as nb`.
    
- Run several notebooks in parallel:
    
    - `nb.runMultiple(['NotebookNameOne', 'NotebookNameTwo'])` executes all listed notebooks at the same time.
        

Use when:

- You have independent steps that do not depend on each other and can safely run in parallel to reduce total time.
    

---

## Ordered execution with a DAG object

You can define a **Python DAG object** describing activities, timeouts, retries and dependencies.

Key DAG elements:

- `activities`: list of notebook activities; each has:
    
    - `name` – unique activity name.
        
    - `path` – notebook path.
        
    - `timeoutPerCellInSeconds`.
        
    - Optional: `retry`, `retryIntervalInSeconds`, `dependencies` (list of other activity names).
        
- `timeoutInSeconds`: max total runtime for the entire DAG (default 12 hours).
    

Behavior:

- If `Notebook2` lists `dependencies: ["Notebook1"]`, it will **only start after Notebook1 finishes successfully**, i.e. a simple in‑code orchestration graph.
    

---

## Pipelines vs Notebook‑based orchestration

Historically, the advantage of notebook‑orchestrated flows was that **all notebooks shared the same Spark session**, saving capacity.  
With the introduction of **Session Tags** in Data Pipelines, you can now also have multiple pipeline‑triggered notebooks share the same Spark session, so the capacity benefit is less critical; the main difference is now **code‑first (Notebook) vs visual (Pipeline)** orchestration style.

---

## 4.2 Triggers – core idea

Triggers define **when and how** Fabric items (notebooks, dataflows, pipelines, semantic models) are executed: on a schedule, on demand, or in reaction to events (Fabric/Azure/real‑time).  
DP‑700 expects you to recognize **where** each trigger type is configured and which trigger fits a given scenario (batch vs event‑driven vs real‑time).

---

## Triggers for core Fabric items

**Notebooks**

- Can be run by a **Schedule trigger** directly on the notebook.
    
- Can also be triggered from:
    
    - Data Pipeline **Notebook activity**.
        
    - Other notebooks via `notebookutils`.
        
    - Real‑time events from the Real‑Time Hub (alerts).
        

**Dataflows**

- Support a **Schedule trigger** (refresh on a defined cadence).
    
- Can also be triggered from a **Data Pipeline Dataflow activity**.
    

**Data Pipelines**

- Support a **Schedule trigger** in the pipeline itself (classic batch scheduling).
    
- Support **Azure Blob Storage event triggers** – when a blob/file is created/changed, run the pipeline.
    
- Can also be triggered from:
    
    - Other data pipelines (Invoke Pipeline activity).
        
    - Azure Data Factory pipelines.
        
    - **Job Scheduler API** (REST).
        
    - Real‑time events from the Real‑Time Hub.
        

**Semantic Models**

- For **DirectLake** models:
    
    - Option: **auto‑refresh on OneLake file changes** (near‑real‑time refresh).
        
- For DirectLake and Import models:
    
    - **Scheduled Refresh** in semantic model settings.
        
    - **Semantic Model Refresh** activity in a Data Pipeline.
        
    - Programmatically via **Semantic Link**: `fabric.refresh_dataset()` in `sempy`, or `sempy_labs.refresh_semantic_model()` from a Fabric Notebook.
        

---

## Real-Time Hub events as triggers

Real-Time Hub adds event‑driven automation on top of the above.

When an alert/condition is met, you can:

- Send notifications (Outlook, Teams).
    
- Run a **Data Pipeline** or **Notebook** in Fabric.
    
- Integrate with Eventstream‑based flows.
    

**Fabric Events** (subscribe in Real-Time Hub):

- **Job events** – job created, succeeded, failed (monitor activities).
    
- **OneLake events** – file/folder created, deleted, renamed.
    
- **Workspace item events** – workspace item created, deleted, renamed.
    

**Azure Events** (via Real-Time Hub):

- **Azure Blob Storage events** – blob created, deleted, renamed.
    

These let you build patterns like: “When a file lands in Blob or OneLake → trigger pipeline → refresh semantic model → notify in Teams.”

---
## 4.3 Orchestration patterns – core idea

For DP‑700, it is enough to understand **why orchestration frameworks are useful** and to recognize two key patterns: **metadata‑driven pipelines** and **parent/child architecture**.  
Good orchestration should be scalable, modular, testable, low‑maintenance and provide simple, centralized logging.

---

## Metadata‑driven pipeline architecture

Instead of hard‑coding sources, targets and options in the pipeline, you store them as **metadata** (table/JSON) and have **one generic pipeline** loop over that metadata.

Typical use cases:

- Ingest 25 tables from Azure SQL into 25 Warehouse tables.
    
- Call 10 REST endpoints from a SaaS API and land all raw JSON into Lakehouse Files.
    

Key idea:

- The pipeline first **reads metadata**, then for each row/entry runs the same logic with different parameters (source table, target table, endpoint URL, etc.).
    
- Adding a new table or endpoint = **add a row in metadata**, not build a new pipeline.
    

---

## Parent/Child architecture

Here you separate orchestration into a **Parent pipeline** and one or more **Child pipelines**.

**Parent pipeline**:

- Contains an **Invoke Pipeline** activity to call the child.
    
- Usually reads metadata and **passes parameters** to the child (e.g. table name, schema, file path).
    

**Child pipeline**:

- Defines **pipeline parameters** to receive values from the Parent.
    
- Uses those parameters dynamically in activities (sources, sinks, queries).
    

Benefits:

- Reuse the same Child pipeline logic for many entities.
    
- Keep the Parent focused on “which things to run” and the Child on “how to process one thing”.
    

---
---
# 5 How to Loading?
## 5.1 Full and Incremental Loading – core idea

As a data engineer you often need to **replicate source tables into Fabric** (Lakehouse/Warehouse) and keep them up to date.  
You must choose between **Full load** (always reload everything) and **Incremental load** (load only changes), and know basic implementation options.

---

## Full load – concept, pros, cons

**Definition**

- Full load = copy the **entire source table** into Fabric every time, regardless of what changed.
    

**Pros**

- Simple to implement, reason about and debug; easy to rerun if something fails.
    
- Often more robust when there is no good change tracking in the source.
    

**Cons**

- Expensive in capacity, IO and time for large tables.
    
- Depending on implementation, users might see **partially loaded** destination table during the load window.
    

---

## Full load – PySpark implementation examples

All examples assume `df` is a Spark DataFrame.

1. **Overwrite managed Lakehouse table**
    
    - `df.write.mode("overwrite").format("delta").saveAsTable("Sales")`
        
    - Overwrites contents of Lakehouse table `Sales`; creates it if it does not exist.
        
2. **Overwrite managed table using `save`**
    
    - `df.write.mode("overwrite").format("delta").save("Tables/Sales")`
        
    - Same logical result as above, but with explicit path; `save` can also write to Files.
        
3. **Overwrite unmanaged Delta in Files**
    
    - `df.write.mode("overwrite").format("delta").save("Files/Sales")`
        
    - Writes or overwrites an **unmanaged** Delta table in the Lakehouse **Files** area at that path.
        

---

## Incremental load – concept, pros, cons

**Definition**

- Incremental load = only extract and load **new or changed** records since the last successful load.
    

**Pros**

- Generally faster and less resource‑intensive than full load, especially for big tables.
    
- Better suited for frequent or near‑real‑time updates.
    

**Cons**

- More complex logic (watermarks, change detection, MERGE conditions).
    
- Harder to debug and to recover to a consistent state after partial failures.
    

---

## Incremental load – implementation with Delta Lake

## Method 2: MERGE using Delta Python library

High‑level steps:

1. Reference existing Delta table:
    
    - `healthcare_delta = DeltaTable.forName(spark, "healthcare_delta")`
        
2. Load **updates** into a DataFrame from Files:
    
    - Read CSV (or other format) into `updates_df` with appropriate schema.
        
3. Use `merge` with join condition:
    
    - Match on business key `PatientId`.
        
    - `whenMatchedUpdateAll()` for updates, `whenNotMatchedInsertAll()` for new rows.
        

Result: target table is updated in place with inserts/updates based on the key.

## Method 3: Spark SQL MERGE

Equivalent pattern using SQL over Delta tables:

- `MERGE INTO healthcare_delta AS target USING initial_healthcare_load AS source ON target.PatientId = source.PatientId WHEN MATCHED THEN UPDATE SET * WHEN NOT MATCHED THEN INSERT *`
    

Same logic: update existing rows, insert new ones based on matching key.

---

## Where else is incremental loading supported in Fabric?

Incremental logic is not limited to PySpark/Delta:

- **T‑SQL MERGE** in **Data Warehouse** – now supported; same conceptual MERGE pattern on warehouse tables.
    
- **Copy job incremental loading** – built‑in incremental options for Copy activities.
    
- **Dataflow Gen2** – supports incremental refresh / loading patterns.
    

---
## 5.2 Loading into a Dimensional model – core idea

For DP‑700 you need to understand **Kimball dimensional modelling** and how to implement it in Fabric Data Warehouse: **keys**, **facts**, **dimensions** and **Slowly Changing Dimensions (SCD)**.  
Implementation examples are shown in T‑SQL for Warehouse, but the concepts apply equally to Lakehouse/Spark.

---

## Implementing keys in Fabric DW

- Primary keys can only be added **after** table creation using `ALTER TABLE ... ADD CONSTRAINT ... PRIMARY KEY ... NOT ENFORCED`.
    
- Fabric DW primary keys are **nonclustered only** and **not enforced** (no actual uniqueness enforcement at engine level).
    

Implication: keys are mainly **modelling and documentation constructs**, not hard integrity constraints; you must still ensure data quality via ETL.

---

## Facts, dimensions, SCD – concepts

- **Fact tables** store numeric measures from real‑world events (e.g. `FactSalesTransactions`).
    
- **Dimension tables** store descriptive context (e.g. `DimStores` with store attributes) and have a single primary key referenced by facts as a foreign key.
    

Slowly Changing Dimensions (SCD) are strategies for handling **changes in dimension attributes over time** (e.g. store moves, manager changes).

---

## SCD Type 1 – overwrite, no history

- When a dimension row changes, the existing row is **updated/overwritten**, no historical versions kept.
    
- Pros: simple to implement. Cons: you **lose historical states**, cannot easily answer “what did this look like last year?”.
    

---

## SCD Type 2 – full history with versions

- For each change, a **new row** is added to the dimension; the old row remains, usually with date/version metadata.
    
- Common columns:
    
    - `valid_from`, `valid_to` – effective date range.
        
    - `is_current` – flag for the active version.
        
    - `is_deleted` – to track deletions in the source.
        

Implementation notes:

- You must use a **surrogate key** (typically BIGINT) because the natural/business key repeats across versions.
    
- ETL becomes more complex (correct inserts/updates and date ranges), but you gain complete change history.
    

---
---

# 6 Ingestion 🤔 | Transformation 🪓

## 6.1 Which data store choose?

For DP‑700, choosing between **Lakehouse, Warehouse and Eventhouse (KQL DB)** mainly depends on data type, skills/tools, and workload pattern shown in that table.

---

## Lakehouse – when to choose it

- Best for **unstructured, semi‑structured and structured** data together (files + tables) with **Spark / PySpark / Spark SQL / R** as primary dev tools.image.jpg​
    
- Ideal for data engineers/data scientists, large‑scale batch processing, flexible schema, and when you want both files and tables in OneLake with shortcuts support.image.jpg​
    

---

## Warehouse – when to choose it

- Best for **structured and semi‑structured (JSON) data** where primary skill is **SQL** and you need **multi‑table transactions**.image.jpg​
    
- Fits data warehouse developers/architects, strong T‑SQL workloads, MERGE‑heavy ETL, and when you want tightly controlled schema plus CI/CD over SQL projects.image.jpg​
    

---

## Eventhouse (KQL DB) – when to choose it

- Best for **time‑series / log / telemetry** scenarios with unstructured, semi‑structured and structured event data, queried mainly via **KQL**.image.jpg​
    
- Choose it for app telemetry, monitoring, security logs, geospatial and real‑time analytics where ingestion is continuous and latency must be seconds, not minutes.image.jpg​
    
---

## 6.2 Which data transformation tool??

Choosing the right transformation tool in Fabric depends on **use case, skills, connectors, interface, and complexity**.image.jpg​

---

## Pipeline Copy activity

- **Use when:** You need robust **data ingestion / migration** with **lightweight transforms** (type conversions, column mapping, merge/split files, flatten hierarchy).image.jpg​
    
- **Persona & skills:** Data engineer / data integrator with **ETL, SQL, JSON**; prefers **no‑code / low‑code**.image.jpg​
    
- **Interface:** Wizard + pipeline canvas.image.jpg​
    
- **Connectivity:** ~30+ sources, 18+ destinations.image.jpg​
    
- **Complexity & scale:** Low–medium transformation complexity, **low–high data volume**.image.jpg​
    

Use it for straightforward copy/landing jobs inside orchestrated Data Pipelines.

---

## Dataflow Gen2

- **Use when:** You need **data ingestion + richer transformation/wrangling/profiling** in a GUI, reusable across reports/models.image.jpg​
    
- **Persona & skills:** Data engineer, integrator, **business analyst** with ETL / **M / SQL**.image.jpg​
    
- **Interface:** **Power Query** canvas.image.jpg​
    
- **Connectivity:** 150+ connectors; destinations include **Lakehouse, Azure SQL DB, Azure Data Explorer, Synapse**.image.jpg​
    
- **Complexity & scale:** Low–high transformation complexity (300+ functions), low–high data volume.image.jpg​
    

Pick this for self‑service friendly, repeatable transforms that still scale reasonably well.

---

## Spark (Notebook / Spark job definition)

- **Use when:** You need maximum flexibility for **big‑data ingestion, complex transformations, processing, profiling** across structured + semi/unstructured data.image.jpg​
    
- **Persona & skills:** Data engineer, data scientist, developer with **Scala, Python, Spark SQL, R**.image.jpg​
    
- **Interface:** Notebook or Spark job definition.image.jpg​
    
- **Connectivity:** “Hundreds of Spark libraries” as sources/destinations.image.jpg​
    
- **Complexity & scale:** Low–very high transformation complexity; low–high data volume with full distributed compute.image.jpg​
    

Use Spark when you hit the limits of low‑code tools or need ML / custom logic tightly integrated with ETL.

---

## T‑SQL in Data Warehouse

- **Use when:** You focus on **warehouse‑centric ETL/ELT**: ingest into a DW and transform inside using SQL (joins, MERGE, windowing).
    
- **Persona & skills:** Data engineer / data developer with **T‑SQL + data modeling** skills.
    
- **Interface:** T‑SQL query or notebook SQL cell.
    
- **Sources & destination:** Often **COPY INTO** from ADLS Gen2 / OneLake into **Data Warehouse tables**.
    
- **Complexity & scale:** Low–high transformation complexity, low–high volume (analytic SQL engine).
    

Best fit when the team is SQL‑heavy and the main target is a structured warehouse model.

---

## 6.3 Shortcuts
## Supported external sources (high level)

From a Lakehouse you choose **Get data → New shortcut** and can point to:

- **Dataverse/Dynamics** → appears as **shortcut tables** under `Tables/`.
    
- **Delta Lake, Iceberg** in external storage → appear as **Delta/Iceberg table shortcuts** under `Tables/`.
    
- **AWS S3, Google Cloud Storage, ADLS Gen2** folders with files (CSV, JSON, etc.) → appear as **folder shortcuts** under `Files/`.
    

Fabric then treats these shortcuts almost like native Lakehouse objects for querying and downstream processing.

---

## Why use shortcuts?

- Avoids **data duplication** and cross‑cloud copies; you query/transform external data in‑place.
    
- Simplifies **bronze layer** design: a Bronze Lakehouse can aggregate many external sources via shortcuts and expose a unified view.
    

---

## 6.4 Mirroring – core idea

Mirroring **replicates an external operational database into Fabric** in an analytics‑friendly format with **near real‑time sync and no classic ETL**.  
Fabric continuously ingests changes from the source, so you get an always‑up‑to‑date analytical copy for reporting and downstream processing.

---

## Supported mirrored sources

From **New item → Get data → Mirrored …** you can currently choose (preview set):

- Azure SQL Database
    
- Azure SQL Managed Instance
    
- Azure Cosmos DB
    
- Snowflake
    
- Databricks Unity Catalog (metadata mirroring + shortcuts)
    
- Generic **Mirrored database (preview)** and **Open Mirrored DB** for broader patterns.
    

All of them land into a **Fabric SQL Database / Mirrored DB** that behaves like a native Fabric analytical store.

---

## When to use mirroring

- You have an **OLTP / operational** system (e.g. Azure SQL, Cosmos, Snowflake) and want analytics **without building/maintaining ETL pipelines**.
    
- You need **low‑latency** replication (near real‑time) but still want separation between operational workload and reporting workload.
    
- You want to treat the mirrored DB as a **source for Lakehouse/Warehouse/Lakehouse shortcuts** or as a direct reporting source.
    

---

## Shortcuts vs Mirroring – summary

|Aspect|Shortcuts|Mirroring|
|---|---|---|
|Data movement|**No copy** – logical pointer to external data.|**Yes** – data replicated into Fabric analytical store.|
|Latency|Depends on source; reads live data at query time.|Near real‑time sync stream from source to Fabric.|
|Source types|Files, Delta/Iceberg tables, Dataverse, S3/GCS/ADLS folders.|Operational DBs: Azure SQL, SQL MI, Cosmos, Snowflake, Databricks UC, etc.|
|Workload impact on source|Queries hit source directly; can increase source load and cross‑cloud egress.|Change feed‑based replication; designed to minimize impact, analytics run on Fabric copy.|
|Governance & performance|Data stays scattered; performance and security depend on each source.|Centralized in Fabric, easier to secure, cache and optimize.|
|Typical use|Broad **data lake aggregation** without duplication, Bronze layer over many storages.|**Operational DB offloading** for analytics and reporting with minimal ETL.|

**Plusy shortcuts:** žádné kopírování dat, levné na storage, rychlé onboarding více zdrojů.  
**Mínusy shortcuts:** závislost na výkonu zdroje, možné egress náklady, složitější governance napříč systémy.

**Plusy mirroringu:** centralizovaný analytický store ve Fabricu, nízká latence, menší zátěž OLTP, snadnější zabezpečení a optimalizace.  
**Mínusy mirroringu:** data se kopírují (storage + správa), podporuje jen vybrané databázové zdroje.

---

## 6.5 Data ingestion with Data Pipelines

Data Pipelines are the **main orchestrator for batch and near real‑time ingestion** into Fabric, typically using the **Copy activity** plus supporting activities for control flow.

---

## Sources & destinations

From the Copy activity you can choose from many **sources** (image shows only a subset):

- Databases: SQL Server, Azure SQL, Oracle, SAP HANA, Snowflake, PostgreSQL, MySQL, etc.
    
- Files/services: Folders, Azure Blobs, ADLS Gen2, S3, REST/HTTP, SharePoint, Dynamics, and more.
    

**Destinations:**

- **File data** → Lakehouse **Files** area.
    
- **Table data** → any Fabric data store (Lakehouse tables, Warehouse, KQL DB, etc.).
    
- Plus many external data stores when doing outbound loads.
    

---

## Typical ingestion pattern in a pipeline

1. **Copy** from source to Bronze Lakehouse/Warehouse (full or incremental).
    
2. Optional **validation / logging** steps (stored procedures, notebooks, REST calls).
    
3. **Trigger downstream**: transformation pipelines/notebooks, semantic model refresh, or alerts.
    

You combine this with the orchestration concepts from section 4 (dependencies, triggers, metadata‑driven / parent‑child patterns) to build robust ingestion solutions.

---

## 6.6 Data Transformation 🧙🏽‍♂️
## 6.6.1 With T‑SQL – exam focus

For DP‑700, T‑SQL is mainly about **doing real warehouse work inside Fabric DW**: creating tables and loading data, modelling facts/dimensions, keys, and implementing security.  
The Fabric Dojo notebook is a deep‑dive practice file; below je shrnutí, co z něj potřebuješ umět.

---

## What this T‑SQL block covers

- **Table creation & ingestion methods** for Fabric Data Warehouse
    
    - `CREATE TABLE`, `ALTER TABLE`, `COPY INTO`, `INSERT … SELECT`, `MERGE` for upserts.
        
- **Primary keys & surrogate keys**
    
    - Defining non‑enforced PKs, using surrogate keys (BIGINT identity) in dimensional models.
        
- **Dimensional modelling in T‑SQL**
    
    - Joins mezi fakty a dimenzemi.
        
    - Implementace SCD (Type 1/2) pomocí `MERGE`, `INSERT`, `UPDATE`.
        
- **Security in Fabric DW**
    
    - RLS pomocí security policies, CLS/OLS přes role a `GRANT`, kombinace s item‑level permissions.
        

Notebook tě vede prakticky přes tyto scénáře v jednom DW připojeném k T‑SQL.

---

## What is assumed as prerequisites

Z modulu 6.6 se **neučí základy SQL**, ty musíš umět předem:

- `SELECT`, `WHERE`, `GROUP BY`, `HAVING`, agregace.
    
- `INSERT`, `UPDATE`, `DELETE`.
    
- Ranking funkce (`ROW_NUMBER`, `RANK`, `DENSE_RANK`, `NTILE`).
    
- `UNION`, `UNION ALL`.
    
- Znalost T‑SQL datových typů.
    
- Tvorba views, stored procedures, functions.
    
- Spouštění DW dotazů z Data Pipelines (Stored Procedure / Script / Lookup activities).
    

Tohle DP‑700 bere jako samozřejmý základ; zkouška tě pak testuje na **aplikaci** T‑SQL v prostředí Fabric DW, ne na syntaxi začátečníků.

---

## 6.6.2 Data Transformation with PySpark – overview

This notebook is a **PySpark deep‑dive for Fabric data engineers**, focused on what DP‑700 expects you to know: Spark engine basics, Lakehouse integration, table creation/loading and core transformations.  
It assumes you already know Python/Spark fundamentals and uses one Lakehouse plus sample files in the `Files/` folder for hands‑on work.

---

## 1. Notebook fundamentals

- Shows how to work with **multiple languages** in one Fabric notebook (PySpark, Spark SQL, Markdown) and how to **parameterize** notebooks (e.g. environment, paths).
    
- Demonstrates `notebookutils` helpers (for orchestration, file access, secrets, etc.), which you already saw in orchestration with notebooks.
    

---

## 2. Table creation in Lakehouse

- Creating and overwriting Lakehouse tables using both **Spark SQL** and **PySpark DataFrame writes** (`saveAsTable`, `save` to `Tables/` or `Files/`).
    
- Covers how managed vs unmanaged Delta tables map to **Tables/** vs **Files/** in a Fabric Lakehouse.
    

---

## 3. Loading methods

- Different ingestion paths with PySpark: reading CSV/JSON/Parquet from `Files/`, external storage, then writing to Delta tables.
    
- Shows **overwrite vs append** patterns and how they relate to **full vs incremental** loading that you studied in section 5.1.
    

---

## 4. Transformation basics

- Demonstrates common DataFrame operations that DP‑700 expects you to recognize: selects, filters, joins, aggregations, window functions, simple data quality checks, etc.
    
- Purpose is not to be exhaustive Spark training, but to make you comfortable reading and reasoning about PySpark ETL code in exam scenarios.
    

---
---

# 7 Real-time streaming

Real‑time data in Fabric means processing **continuous event streams with very low latency**, instead of periodic batch loads with a natural time lag.

---

## 7.0 Real‑time vs batch – mindset

- **Batch processing** loads and analyzes data in chunks (daily/hourly loads etc.); decisions are based on already‑stored history and some delay between event and insight is acceptable.
    
- **Real‑time systems** ingest and analyze events as they happen, often connected to the physical world via sensors (IoT, telemetry, GPS, temperature), and are more complex and costly but critical in domains like finance, fraud detection, logistics, transport and large consumer apps.
    

---

## Real‑time ecosystem in Microsoft Fabric

Fabric provides several components that you combine into real‑time solutions:

- **Spark Structured Streaming** – code‑first streaming framework running on the Spark engine for large‑scale real‑time ingestion and analysis.
    
- **Eventstreams** – no‑code streaming ingestion with basic transformations and routing from sources (e.g. Event Hubs/IoT Hub, custom endpoints) to sinks like Eventhouse and Lakehouse.
    
- **Eventhouse (KQL Databases)** – primary store for time‑series / log data, optimized for high‑rate ingestion and KQL querying.
    
- **KQL Querysets** – place to author and run KQL queries over KQL DBs, focused on interactive analytics over large time‑series datasets.
    
- **Real‑time Dashboards** – visualize KQL results live without needing Power BI, for monitoring and operational views.
    

Together these let you build pipelines where events flow from sources into Fabric, are stored in Eventhouse or Lakehouse, queried with KQL or Spark and surfaced in dashboards with second‑level latency.

---

# 7.1 Real-time Choice ➿ or 🧬

In Fabric you choose between **Spark Structured Streaming** and **Eventstreams** as the main streaming engines.

---

## Spark Structured Streaming – when to choose it

- Best when you are **already using Spark for data engineering** and want to extend batch pipelines to streaming with the same APIs.
    
- **Pro‑code** approach: you can implement complex transformations, advanced windowing, custom business logic and unit tests for reliability.
    
- Ideal for **migrating existing Spark streaming code** from other platforms and when you want to **stream directly into a Lakehouse** as your primary store.
    

Use Spark Structured Streaming for heavy, code‑driven real‑time ETL where your team is comfortable with PySpark/Scala.

---

## Eventstreams – when to choose it

- Completely **no‑code**, easy to learn and manage through a visual canvas.
    
- Fits scenarios where you **do not need very complex transformations** on the incoming stream, but mainly routing, filtering, basic aggregates and windowing.
    
- Offers a **wider set of output destinations** than Spark alone: Lakehouse, KQL Database (Eventhouse), Activator and even another Eventstream (derived streams).
    

Use Eventstreams when you want fast time‑to‑value for real‑time ingestion and routing without building or maintaining custom streaming code.

---

## 7.2 Eventstreams ➿

Eventstreams are a **no‑code streaming tool** in Fabric to ingest, transform and route real‑time data from many sources into destinations like Eventhouse, Lakehouse or Activator.

---

## Sources for Eventstreams

You can ingest from multiple real‑time and change‑data sources:

- Azure real‑time PaaS: **Event Hub, IoT Hub**.
    
- Cloud DBs with **Change Data Capture**: Azure SQL, PostgreSQL, MySQL, Cosmos DB.
    
- Third‑party streaming: **Google Pub/Sub, Amazon Kinesis, Kafka**.
    
- **Fabric/Azure events**: Fabric workspace events, Azure Blob Storage events.
    
- **Custom endpoints** via Fabric REST API/SDKs and built‑in sample streams.
    

---

## Transformations in Eventstreams

All done visually, no code:

- **Filter** – keep events matching a condition on a field (e.g. `No_Bikes = 0` or `Neighbourhood = 'Southwark'`).
    
- **Manage fields** – choose which columns to keep, rename them, and change data types; typically used early in the flow.
    
- **Aggregate** – compute running aggregates over a time window (Average, Min, Max, Sum).
    
- **Group By** – windowed aggregations with Tumbling, Hopping, Sliding, Session or Snapshot windows.
    
- **Union** – combine two compatible streams into one (non‑matching fields dropped).
    
- **Expand** – explode array‑type fields into multiple rows.
    
- **Join** – join two streams on a matching condition (stream‑to‑stream join).
    

---

## Destinations for Eventstreams

You can route the processed stream to:

- **Eventhouse (KQL DB)** – for KQL analytics and Real‑Time Dashboards.
    
- **Lakehouse** – to land streaming data alongside batch data or for Spark/ML processing.
    
- **Custom endpoint** – push to your own application.
    
- **Derived Stream** – a logical output stream after transforms, which can itself be routed and monitored in Real‑Time Hub.
    
- **Fabric Activator** – to drive alerting and automated actions based on live stream values.
    

---

