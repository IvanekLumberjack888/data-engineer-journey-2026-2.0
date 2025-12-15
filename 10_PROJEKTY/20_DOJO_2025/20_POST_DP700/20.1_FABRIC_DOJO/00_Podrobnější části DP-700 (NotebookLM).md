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

## 5.3 Streaming data patterns – core idea

Streaming data patterns describe how real‑time events flow through Microsoft Fabric from source to final analytical consumption. For DP‑700, you mainly need to recognize a simple streaming pipeline and how the medallion (bronze–silver–gold) architecture applies to streaming workloads.

---

## Simple streaming architecture

A basic streaming setup starts with a **real‑time source** such as Event Hubs, IoT devices, or applications emitting events continuously. These events are ingested into Fabric Real‑Time Intelligence, processed by a streaming engine (for example Eventstreams, Spark Structured Streaming, or KQL), and then written to sinks like Lakehouse tables, KQL databases, or warehouses for analytics and dashboards.

Typical stages you should be able to name:

- Source → ingestion into Real‑Time Intelligence.
    
- Real‑time processing / routing.
    
- Persisted storage and analytical consumption in Fabric.
    

---

## Streaming medallion architecture

The **medallion architecture** extends to streaming data by applying bronze, silver, and gold layers to event flows. Instead of only batch files, streaming events are progressively refined as they move through these layers.

Conceptual mapping:

- **Bronze (raw streaming)**: Raw or lightly processed event data, typically append‑only, stored for replay and audit.
    
- **Silver (curated streaming)**: Cleaned and standardized data with schema enforcement, quality checks, and applied business rules.
    
- **Gold (consumption‑ready)**: Aggregated, modeled, or denormalized data optimized for BI reports, semantic models, and low‑latency queries.
    

---

## Why patterns matter for DP‑700

DP‑700 scenarios often describe diagrams like “source → real‑time processing → bronze/silver/gold” and ask which Fabric components or layers to use. Understanding the simple streaming pipeline and the streaming medallion architecture helps you correctly place ingestion, transformation, storage, and reporting pieces in Real‑Time Intelligence questions.


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

## 7.3 Spark Structured Streaming

Spark Structured Streaming in Fabric lets you treat a **data stream as an unbounded table** where new events continually append as new rows.

---

## Concept and API basics

- Fabric Spark is a managed implementation of open‑source Spark, so you can use the **full Spark Structured Streaming API**.
    
- Streaming code reuses the same **DataFrame + Spark SQL** concepts as batch: you read a stream with `spark.readStream` and write it with `df.writeStream`.
    

In practice, the pattern is:

- `spark.readStream.format(...).options(...).load()` → create a streaming DataFrame from a source such as Event Hubs.
    
- Apply transformations (`withColumn`, `select`, `from_json`, joins, aggregations).
    
- `df.writeStream.format("delta").option("checkpointLocation", ...).outputMode("append").toTable("...")` → continuously append to a Delta table in a Lakehouse.
    

---

## Why it matters for DP‑700

- You must recognize that **Structured Streaming code looks very similar to batch DataFrame code**, only using `readStream`/`writeStream`.
    
- Typical exam scenario: streaming events from Event Hub into a **Lakehouse Delta table** with checkpoints for reliability, then using that table for downstream analytics.
    
---

## 7.4 Process / analyze data using KQL – core idea

This topic is about using **Kusto Query Language (KQL)** to query and analyze data stored in **Eventhouse / KQL databases** in Microsoft Fabric. For DP‑700, you need to understand where KQL fits in the real‑time stack and be able to read and compose core KQL query patterns for analytics and monitoring.

---

## Eventhouse and KQL Database

In Fabric real‑time analytics, **Eventhouse** is the logical container for one or more **KQL databases** that store high‑volume, time‑series or log data, often ingested from streaming sources. You use KQL queries over these databases for dashboards, investigative analysis, and operational monitoring scenarios.

Key expectations for DP‑700:

- Understand what an Eventhouse is and how it relates to other Fabric items such as Eventstreams, Lakehouses, and warehouses.
    
- Know that KQL databases are optimized for large append‑only telemetry and log workloads rather than classic relational modeling.
    

---

## Core KQL query skills

KQL uses a **pipe‑based** syntax where queries start from a table and apply operators in sequence like a processing pipeline. You should be comfortable with basics such as selecting and shaping data, applying expressions, and controlling result size.

Important operators for the exam:

- Basics: `take`, `limit`, `project`, `extend`, `sort` and simple scalar functions (string, numeric, datetime).
    
- Time awareness: working with timestamp fields, ordering by time, and selecting recent data.
    

---

## Filtering and aggregation patterns

Filtering is done primarily with the `where` operator, which restricts rows based on predicates like time ranges, device IDs, or severity. Typical exam scenarios will describe real‑time telemetry where you filter on a time window and some dimension (for example, a specific service or region).

Aggregations are handled with `summarize`, grouping by one or more columns such as time bins, region, or device. Common patterns include counts per time interval, averages and min/max by device, and combined aggregations for monitoring metrics.

---

## Management commands and operational aspects

KQL also includes **management commands** used to configure and operate Eventhouse and KQL databases, not to query business data directly. DP‑700 expects you to recognize these as administrative tools for controlling retention, caching, ingestion, and performance.

Examples of concepts to recognize:

- Setting or inspecting retention and caching policies on databases and tables.
    
- Checking ingestion status and system metrics to troubleshoot performance or reliability issues.
    

---

## KQL window functions

Beyond simple `summarize`, KQL supports **window functions** that perform calculations over ordered sets of rows, such as time‑series windows or partitions by key. These functions enable moving averages, running totals, and session‑like analytics that are important for advanced telemetry analysis.

For DP‑700, you should conceptually understand when a scenario calls for a window function rather than a straightforward grouped aggregate, especially when the requirement mentions running aggregates over an ordered sequence of events.

---

## Why this matters for DP‑700

KQL is a first‑class query language in the **Streaming data / Real‑time** area of Fabric and complements T‑SQL, PySpark, and Spark Structured Streaming. Exam questions will often describe data flowing into Eventhouse/KQL DB and ask how to query, aggregate, or manage it using appropriate KQL constructs and management commands.

Being familiar with KQL basics, filtering, aggregations, management commands, and window functions ensures you can choose KQL when it is the right analytical engine and interpret KQL‑based solutions in DP‑700 questions confidently.

---

## 7.5 Window functions (in Eventstreams) – core idea

Window functions in Eventstreams take an infinite real‑time stream and split it into time‑based windows so you can compute aggregates (average, min, max, sum) over each window instead of per individual event. This helps both with real‑time decision‑making (summary statistics over recent data) and with reducing stored volume by keeping, for example, 30‑second averages instead of every second‑level reading.

In Eventstreams, windowing is implemented with two transformations: **Aggregate** and **Group By**. Aggregate gives you a continuously updated view over a time window, while Group By produces one result per discrete window using specific window types.

---

## Windowing in Eventstreams: Aggregate vs Group By

**Aggregate transformation**

- Recomputes the aggregate every time a new event arrives, over a configured window length such as “last 60 seconds”.
    
- Typical question pattern: “What is the average value over the last N seconds right now?” – you want a rolling, continuously refreshed metric.
    

**Group By transformation**

- Groups events that fall inside a defined window and outputs one aggregated row for that window.
    
- Supports five window types: **Tumbling**, **Hopping**, **Snapshot**, **Sliding**, and **Session**, each designed for a different streaming pattern.
    

For the exam, decide first if the scenario describes a rolling real‑time metric (Aggregate) or discrete buckets/sessions (Group By), then pick the window type if Group By is implied.

---

## High‑level classification of window types

You can remember the five Group By window functions using two questions:

- Is the window length **fixed** or **variable**?
    
- Do windows **overlap**, or are they **non‑overlapping**?
    

This leads to:

- Fixed length, non‑overlapping → **Tumbling window**.
    
- Fixed length, overlapping with explicit hop → **Hopping window**.
    
- Fixed length, overlapping with automatic sliding → **Sliding window**.
    
- Variable length, non‑overlapping per session → **Session window**.
    
- Point‑in‑time windows keyed by timestamp → **Snapshot window**.
    

---

## Tumbling and Hopping windows

## Tumbling window

- **Description**: Fixed‑length windows that do **not** overlap; the stream is divided into consecutive blocks (for example, 1‑minute or 1‑hour chunks).
    
- **Example**: “Each hour, calculate the average air temperature in my living room.” You get 24 aggregated values per day, one for each hour, each representing all readings in that hour.
    

## Hopping window

- **Description**: Fixed‑length windows that **can overlap**; you define both the window length and a hop size (how far the window moves each time).
    
- **Example**: “Calculate the average bedroom temperature over the past hour, but recompute every 12 minutes.” The one‑hour window hops forward by 12 minutes, so many windows overlap.
    

Exam cue: if the requirement says “over the last X minutes, recomputed every Y minutes” with Y < X, it is almost always a hopping window.

---

## Snapshot and Sliding windows

## Snapshot window

- **Description**: Aggregates over **point‑in‑time snapshots**, ideal for bursty sensors that send multiple readings in a single event or at the same timestamp.
    
- **Use case**: A temperature sensor emits a batch of readings every 15 minutes; you want the average of the readings in each batch. A snapshot window groups values by the event timestamp and aggregates per timestamp.
    

## Sliding window

- **Description**: Uses a fixed time‑window length (for example 10 seconds) and automatically creates many **overlapping** windows across the stream. You typically combine it with a filter so you only emit windows whose aggregate meets some condition.
    
- **Use case**: “Raise an alert if the total number of concurrent taxi journeys is above 350 during any 10‑second period.” The sliding window continuously checks every possible 10‑second span, not just at discrete hops.
    

Exam cue: wording like “during any N‑second interval” or “whenever at any time the metric exceeds X over the last N seconds” suggests a sliding window.

---

## Session windows

## Session window

- **Description**: Groups events that occur close together in time into variable‑length sessions, usually per user or device. For a given key (user, device), session windows do not overlap; they are separated by inactivity gaps.
    
- **Use case**: Website analytics such as “total number of pages visited by a user in one session.” The user might click multiple pages, pause, and eventually leave; events during that visit form a single session window.
    

Exam cues for session windows:

- The scenario talks about “sessions”, “user visits”, or “activity separated by periods of inactivity”.
    
- The window length is not fixed ahead of time; it depends on how long the user stays active, plus a defined inactivity timeout.
    

---

## How to think about window functions for DP‑700

When you see a streaming scenario in the exam, ask yourself:

1. Do I need a **rolling** view over the last N time units (Aggregate) or **discrete blocks/sessions** (Group By)?
    
2. If Group By, is the window length fixed or variable?
    
3. If fixed, do I need overlapping windows (hopping or sliding) or clean, non‑overlapping blocks (tumbling)?
    
4. If variable, is this about user/device sessions (session) or point‑in‑time bursts with shared timestamps (snapshot)?
    

Use this quick mapping:

- Fixed + non‑overlapping → Tumbling.
    
- Fixed + overlapping with explicit hop size → Hopping.
    
- Fixed + overlapping without explicit hop, “any N‑second interval” → Sliding.
    
- Variable + session/inactivity logic → Session.
    
- Point‑in‑time burst / same timestamp → Snapshot.
    
---

# 8 MONITORING 👀🙈👓

## 8.1 Fabric-wide monitoring tools – core idea

Microsoft Fabric provides **three main tools** for monitoring at different organizational levels: **Monitoring Hub** (tenant-level), **Capacity Metrics App** (capacity-level), and **Workspace Monitoring** (workspace-level, preview).

Each tool serves a distinct purpose and monitors different aspects of your Fabric environment. Understanding which tool to use for which scenario is critical for the DP-700 exam.

---

## The three monitoring levels in Fabric

Fabric monitoring operates at three hierarchical levels:

1. **Tenant-level** – monitor all Fabric items across all capacities and workspaces you have access to.
    
2. **Capacity-level** – monitor compute consumption and billing across all workspaces within a specific Fabric capacity.
    
3. **Workspace-level** – monitor item-specific logs and operations within a single workspace.
    

Key exam distinction:

- **Monitoring Hub** = cross-workspace visibility of **run status and failures**.
    
- **Capacity Metrics App** = cross-workspace visibility of **capacity consumption and throttling**.
    
- **Workspace Monitoring** = deep **item-level logs** for specific workspace items (preview feature).
    

---

## Monitoring Hub (Tenant-level)

## What it monitors

**Run status** of Fabric items across all workspaces you have access to. You use it to identify failures, review historic runs, and navigate to failed items for detailed debugging.

## Supported items

- Data Pipelines
    
- Dataflow Gen2
    
- Notebooks
    
- Spark Job Definitions
    
- Semantic Model refreshes
    

## Key characteristics

- **Tenant-wide scope** – you see items from any workspace where you have at least read access.
    
- **Run-centric view** – focused on execution history (succeeded, failed, in progress, canceled).
    
- **Navigation hub** – click on a failed item to open its detailed logs or error messages.
    

## When to use

- You need to quickly identify which pipeline or notebook failed across multiple workspaces.
    
- You want to review historic runs without opening each workspace individually.
    
- You are troubleshooting a failure and need to navigate to the item's detailed error logs.
    

---

## Capacity Metrics App (Capacity-level)

## What it monitors

**Capacity consumption** (compute utilization) across all item types within a Fabric capacity. It shows billable operations, throttling events, and CU (Capacity Unit) consumption over time.

## Supported items

**All Fabric items** that consume capacity – essentially everything (pipelines, dataflows, notebooks, semantic models, lakehouses, warehouses, etc.).

## Key characteristics

- **Power BI App** – you install it into your Fabric capacity as a pre-built Power BI report.
    
- **Capacity-level scope** – monitors all workspaces within a single capacity.
    
- **CU consumption metrics** – shows which items consume the most capacity units and when throttling occurs.
    

## When to use

- You need to analyze which workspaces or items are consuming the most capacity.
    
- You want to identify throttling events and optimize resource allocation.
    
- You are planning capacity scaling or investigating performance bottlenecks related to capacity limits.
    

## Important nuance

The Capacity Metrics App does **not** show individual run failures or error messages – it only tracks **resource consumption**. For failure investigation, use the Monitoring Hub instead.

---

## Workspace Monitoring (Workspace-level, preview)

## What it monitors

**Item-level logs** for specific workspace activities. When enabled, Fabric provisions an **Eventhouse** in your workspace to store granular logs.

## Supported items (as of preview)

- GraphQL operations
    
- Eventhouse
    
- Mirrored databases
    
- Semantic Models
    

## Key characteristics

- **Preview feature** – unlikely to appear in the DP-700 exam, but useful to know for future scenarios.
    
- **Eventhouse-backed** – logs are stored in an auto-provisioned Eventhouse, which you can query with KQL.
    
- **Workspace-scoped** – only tracks activities within the workspace where it is enabled.
    

## When to use

- You need granular logs for semantic model queries, eventhouse operations, or mirrored database sync activities.
    
- You want to perform custom KQL queries on workspace activity logs.
    
- You are building custom dashboards or alerts based on item-level logs.
    

---

## Comparison table: which tool for which scenario

|**Scenario**|**Tool to use**|
|---|---|
|Identify which pipeline failed across multiple workspaces|Monitoring Hub|
|Investigate capacity throttling and CU consumption|Capacity Metrics App|
|Review historic runs of a specific notebook|Monitoring Hub|
|Analyze which workspace consumes the most capacity|Capacity Metrics App|
|Query granular logs for semantic model refresh operations|Workspace Monitoring (preview)|
|Navigate to a failed dataflow's detailed error message|Monitoring Hub|

---

## Self-check / moderator questions

1. What is the primary difference between **Monitoring Hub** and **Capacity Metrics App**?
    
2. Which tool would you use to identify **capacity throttling** events?
    
3. Which Fabric items are **not supported** in the Monitoring Hub (e.g., eventhouse, warehouse)?
    
4. What happens when you enable **Workspace Monitoring** in a workspace?
    
5. Why is **Workspace Monitoring** unlikely to appear in the DP-700 exam?
    
6. If a pipeline fails, which tool provides the **run history and error messages**?
    
7. Can you use the **Capacity Metrics App** to see which user triggered a notebook run?
    
8. What is the scope of the **Monitoring Hub** – workspace, capacity, or tenant?
    

---

This structure gives you a clear framework for understanding when to use each monitoring tool. The next sections (9.1–9.4) will dive into **item-specific monitoring** for pipelines, dataflows, notebooks, and eventstreams.

---

# 9 Monitor / Optimize Processing

## 9.1 Data Pipeline Monitoring & Optimization – core idea

**Data Pipelines** are the primary low-code orchestration tool in Microsoft Fabric. Monitoring and optimizing them involves tracking run status through the **Monitoring Hub**, investigating failures via **activity-level error messages**, configuring **retry logic** for transient failures, and tuning **Copy Data settings** for performance and fault tolerance.

For the DP-700 exam, you need to understand where to find pipeline failures, how to debug activity-level errors, and how to implement error-handling patterns (retry, on-fail dependencies, custom alerting).

---

## Monitoring Hub – your first stop for pipeline failures

## What it does

The **Monitoring Hub** shows all pipeline runs across workspaces you have access to. For scheduled pipelines, this is where you check run status (succeeded, failed, in progress, canceled).

## How to use it

1. Navigate to **Monitoring Hub** (tenant-wide view).
    
2. Filter by **Data pipeline** to see all pipeline runs.
    
3. Click on a **failed pipeline run** to drill into details.
    

## Key exam point

If a question asks "where do you first look when a scheduled pipeline fails?", the answer is **Monitoring Hub** (unless custom alerting is already configured).

---

## Output pane in Data Pipeline Activities Status

## What it shows

When you open a specific pipeline run, you see the **activities graph** with color-coded status (green = success, red = failed). Click on a **failed activity** to view the **Error details** pane.

## Error details pane contains

- **Error message** – human-readable description of what went wrong.
    
- **Error code** – system error code (e.g., `UserErrorConfigurationIssue`).
    
- **Failure type** – transient vs. persistent error.
    
- **Activity ID** – unique identifier for the activity run.
    

## When to use

Always drill into the **error message** before troubleshooting. It tells you:

- Was it a connection failure (transient)?
    
- Was it a permission issue (RLS, item-level access)?
    
- Was it a data schema mismatch?
    

---

## Inputs and Outputs – debugging tool during development and failures

## What they show

For each pipeline activity, you can inspect:

- **Input** – the parameters and configuration passed to the activity (JSON format).
    
- **Output** – the result returned by the activity after execution.
    

## Use cases

- **Debugging** – verify that the correct values are being passed (e.g., table name, file path).
    
- **Development** – check intermediate results during pipeline authoring.
    
- **Validation** – confirm that dynamic parameters are resolved correctly.
    

## Exam tip

If a question mentions "how do you verify that a pipeline parameter is correctly passed to a Copy Data activity?", the answer is to inspect the **Input** of that activity.

---

## Copy Data activity – error-handling and optimization

## Retry activities

Many pipeline activities (Copy Data, Notebook, Web, etc.) support a **Retry** setting:

- **Retry count** – how many times to retry on failure (default: 0).
    
- **Retry interval** – delay (in seconds) between retry attempts (default: 30).
    

## When to use Retry

Use **Retry** for **transient failures**:

- Connection timeout to external API or database.
    
- Temporary network issue.
    
- Short-lived resource unavailability.
    

**Do not use Retry** for **persistent failures**:

- Incorrect credentials (will fail every time).
    
- Missing table or file (schema issue).
    
- Permission denied (access control issue).
    

---

## Copy Data Settings – performance tuning and logging

The **Settings** tab of a Copy Data activity has several optimization and logging options:

## Intelligent throughput optimization

- **What it does** – assigns CPU resources (4–256 units) to the Copy Data operation.
    
- **Higher value** = more parallelism and faster copy (but higher capacity consumption).
    
- **Lower value** = slower copy but less capacity impact.
    

## Degree of copy parallelism

- **Default** – 128 parallel threads.
    
- **Use case** – increase parallelism when copying large files or many files to reduce load time.
    
- **Trade-off** – higher parallelism consumes more capacity units.
    

## Fault tolerance

- **Skip incompatible rows** – if a row cannot be copied (e.g., schema mismatch), skip it and continue.
    
- **Skip incompatible files** – if a file cannot be copied, skip it and continue.
    
- **Use case** – useful when copying semi-structured data where some records may not conform to the target schema.
    

## Enable logging

- **What it does** – writes detailed log files to **Azure Blob Storage** (not OneLake).
    
- **Use case** – track which rows/files were skipped, which failed, and why.
    

## Enable staging

- **What it does** – uses an intermediate storage layer (Workspace staging or external Blob) before loading to the destination.
    
- **Use case** – improves performance for large data transfers and provides a recovery point if the final load fails.
    

---

## On Fail dependencies – control flow for error handling

## What it is

In the pipeline canvas, you can define **On Success**, **On Failure**, and **On Completion** dependencies between activities.

## Best practice for alerting

- Use **On Fail** dependency to send notifications **only when there's a failure**.
    
- Connect the failed activity to a **Web activity** or **Office 365 Outlook activity** to send an email or call an API.
    

## Parent-child pipeline pattern

In a **parent-child architecture**:

- The **child pipeline** executes the core logic.
    
- The **parent pipeline** orchestrates multiple child pipelines.
    
- Use **On Fail** in the parent to capture all child failures and send **one consolidated notification** instead of multiple alerts.
    

---

## Custom alerting and logging solutions

While Fabric provides **out-of-the-box monitoring** (Monitoring Hub, Capacity Metrics App), you can also build **custom logging solutions**:

## Approach 1: Log to Fabric SQL Database

- Create a **logging table** in a Fabric Warehouse or SQL Database.
    
- Use a **Script activity** or **Stored Procedure** to write pipeline run metadata (status, duration, error message) after each run.
    

## Approach 2: Log to KQL Database (Eventhouse)

- Create a **KQL table** for pipeline logs.
    
- Use a **Web activity** to POST run data to the KQL ingestion endpoint.
    
- Query logs with KQL for custom dashboards or real-time alerts.
    

## When to use custom logging

- You need **centralized logging** across multiple workspaces or capacities.
    
- You want to track **business-specific metrics** (e.g., number of rows processed, SLA compliance).
    
- You need to integrate pipeline monitoring with external systems (e.g., ServiceNow, PagerDuty).
    

---

## Self-check / moderator questions

1. Where do you first look when a scheduled Data Pipeline fails?
    
2. What information does the **Error details** pane provide when you click on a failed activity?
    
3. How do you verify that a pipeline parameter is correctly passed to a Copy Data activity?
    
4. What is the difference between **Retry** and **On Fail** dependency?
    
5. When should you use **Retry** for a Copy Data activity?
    
6. What does **Intelligent throughput optimization** control in Copy Data settings?
    
7. What is the default value for **Degree of copy parallelism** in Copy Data?
    
8. How does **Fault tolerance** help when copying data with schema mismatches?
    
9. What is the benefit of using a **parent-child pipeline architecture** for error handling?
    
10. Where can you write custom pipeline logs (two options)?
    
11. If you enable **Enable logging** in Copy Data settings, where are the logs written?
    
12. What is the purpose of **Enable staging** in Copy Data settings?
    

---

This gives you a complete framework for monitoring and optimizing Data Pipelines. Next sections (9.2–9.4) will cover **Dataflows**, **Spark Notebooks**, and **Eventstreams** in the same structured format.

---

## 9.2 Dataflow Monitoring & Optimization – core idea

**Dataflow Gen2** is the Power Query-based data transformation tool in Fabric. Monitoring involves checking the **workspace icon** for failures, reviewing **Refresh History** for detailed run logs, and troubleshooting errors at the query and transformation step level.

Optimization strategies include **Fast Copy** (bypassing Power Query for simple loads) and **Enable Staging** (offloading transformations to T-SQL or Spark engines for complex workloads). Understanding when to use each optimization is critical for the DP-700 exam.

---

## Monitoring Dataflow Gen2 – detecting failures

## Where to look first

Unlike Data Pipelines, Dataflow Gen2 failures are **not immediately visible** in the Monitoring Hub (Dataflows are included, but not as prominently as pipelines). Instead:

1. **Workspace view** – a **warning icon** appears next to the Dataflow if the last refresh failed.
    
2. **Power BI report** – end users or report owners may notice stale data or refresh errors in the semantic model.
    

## Why this matters for the exam

If a question asks "a business user reports stale data in a Power BI report powered by a Dataflow Gen2", your first troubleshooting step is to **check the Dataflow refresh status in the workspace view**.

---

## Refresh History – drill into failure details

## How to access

1. **Right-click** on the Dataflow Gen2 in the workspace view.
    
2. Select **Refresh History**.
    
3. You see a list of all previous refreshes with status (succeeded, failed, canceled).
    

## What you see in Refresh History

- **Start time** – when the refresh began.
    
- **Duration** – how long the refresh took.
    
- **Status** – succeeded or failed (with a red icon).
    
- **Type** – on-demand or scheduled refresh.
    

## Drilling into a failed run

Click on a **failed refresh run** to open the detailed view. This shows:

- **Tables** – which tables/queries in the Dataflow succeeded or failed.
    
- **Errors** – specific error messages for each failed query (e.g., "connection timeout", "column not found", "permission denied").
    
- **Activities** – step-by-step breakdown of the refresh process.
    

---

## Dataflow Gen2 optimization strategies

Dataflow Gen2 transformations are powered by the **Power Query (Mashup) engine** by default. While Mashup is great for ad-hoc transformations, it is **slower** than T-SQL or Spark engines for large datasets.

Fabric provides two optimization features to accelerate Dataflow performance: **Fast Copy** and **Enable Staging**.

---

## Fast Copy – bypass Power Query for simple loads

## What it does

**Fast Copy** uses the same backend as the **Data Pipeline Copy Data activity**. Instead of routing data through the Mashup engine, Fabric performs a **direct copy** from source to destination.

## When to use

- You are doing a **simple extract-and-load** (no complex transformations).
    
- Your source connector is supported by Fast Copy.
    

## Supported connectors (as of current Fabric release)

- ADLS Gen2
    
- Azure Blob Storage
    
- Azure SQL Database
    
- Fabric Lakehouse
    
- PostgreSQL
    
- On-premise SQL Server (via gateway)
    
- Fabric Warehouse
    
- Oracle
    
- Snowflake
    

## Limitations

- **No complex transformations** – Fast Copy works only for basic column mapping and filtering.
    
- **Connector-specific** – not all connectors support Fast Copy.
    

## Exam tip

If a question describes a scenario where "a Dataflow Gen2 is copying data from Azure SQL Database to a Lakehouse with minimal transformations and you want to optimize performance", the answer is **enable Fast Copy**.

---

## Enable Staging – offload transformations to T-SQL or Spark

## What it does

**Enable Staging** changes the Dataflow execution model to use an intermediate **staging layer** (Warehouse or Lakehouse). Instead of performing all transformations in the Mashup engine, Fabric:

1. Uses **Mashup engine** to extract data from the source.
    
2. Writes the raw data to a **Staging Warehouse or Lakehouse**.
    
3. Uses **T-SQL** or **Spark engine** (not Mashup) to perform transformations.
    
4. Mashup engine reads the transformed data and writes it to the final destination.
    

## Execution flow comparison

## Staging Disabled (default)

text

`Data Source → Mashup Engine (extract + transform + load) → Destination`

## Staging Enabled

text

`Data Source → Mashup Engine (extract) → Staging Lakehouse → T-SQL/Spark (transform) → Mashup Engine (load) → Destination`

## When to use Enable Staging

Use **Enable Staging** when:

- You have **large datasets** (millions of rows).
    
- You have **complex transformations** (multiple joins, aggregations, window functions).
    
- You want to leverage **T-SQL or Spark performance** instead of Mashup.
    

## When **NOT** to use Enable Staging

**Do not** use Enable Staging when:

- You have **small datasets** (< 100K rows).
    
- You have **simple transformations** (basic column mapping, filtering).
    
- The overhead of writing to/from staging exceeds the transformation time.
    

## Key exam point

If a question describes "a Dataflow Gen2 with complex aggregations and joins on a 10 million row dataset", the answer is **enable staging** to offload transformations to T-SQL or Spark.

---

## Optimization best practices

Beyond Fast Copy and Enable Staging, consider these Dataflow Gen2 optimization patterns:

## Query folding

- **What it is** – Power Query pushes transformations down to the source database instead of processing them in Fabric.
    
- **When it works** – when the source supports query folding (e.g., SQL databases, data warehouses).
    
- **How to verify** – right-click a query step in Power Query and check if "View Native Query" is available.
    

## Reduce query complexity

- **Minimize merges and joins** – each merge/join increases processing time.
    
- **Filter early** – apply filters at the source to reduce data volume.
    
- **Avoid unnecessary columns** – remove unused columns early in the transformation.
    

## Schedule refreshes during off-peak hours

- Dataflow Gen2 refreshes consume **capacity units**.
    
- Schedule large refreshes during **low-usage periods** to avoid throttling.
    

---

## Self-check / moderator questions

1. Where do you first look when a Dataflow Gen2 refresh fails?
    
2. How do you access **Refresh History** for a Dataflow Gen2?
    
3. What information is displayed in the **detailed refresh view** for a failed run?
    
4. What is the difference between **Fast Copy** and **Enable Staging**?
    
5. Which connectors are supported by **Fast Copy**?
    
6. When should you use **Fast Copy** instead of the default Mashup engine?
    
7. What is the default transformation engine for Dataflow Gen2?
    
8. Describe the execution flow when **Enable Staging** is enabled.
    
9. Why does **Enable Staging** add overhead, and when is this overhead justified?
    
10. What is **query folding** and how does it improve Dataflow performance?
    
11. If a Dataflow Gen2 has complex joins and aggregations on 10 million rows, which optimization should you enable?
    
12. If a Dataflow Gen2 is doing a simple copy from Azure SQL Database to a Lakehouse, which optimization should you enable?
    

---

This structured approach gives you a complete framework for monitoring and optimizing Dataflow Gen2. Next sections (9.3–9.4) will cover **Spark Notebooks** and **Eventstreams** in the same format.

---

## 9.3 Spark Notebook Monitoring & Optimization – core idea

**Spark Notebooks** and **Spark Job Definitions** are the code-first data processing tools in Fabric, powered by Apache Spark. Monitoring involves three layers: **Monitoring Hub** (high-level run status), **Monitor Run Series** (performance trends over time), and **Spark History Server** (deep-dive job analysis with DAG visualization, logs, and query plans).

For the DP-700 exam, you need to understand where to find Spark job details, how to interpret executor metrics, and when to use the History Server for optimization.

---

## Monitoring Hub – high-level Spark job status

## What it shows

When you click on a **Notebook** or **Spark Job Definition** in the Monitoring Hub, you see a list of **every Spark job executed** from a particular Spark session.

## Key information displayed

- **Job ID** – unique identifier for the Spark job.
    
- **Status** – succeeded, failed, running, canceled.
    
- **Start time** and **Duration** – when the job started and how long it ran.
    
- **Submitted by** – who triggered the notebook (user or pipeline).
    

## When to use

Use the **Monitoring Hub** when:

- You need to quickly identify **which notebook run failed**.
    
- You want to review **recent run history** across multiple workspaces.
    
- You are troubleshooting a scheduled notebook that didn't complete.
    

## Important exam distinction

The Monitoring Hub shows **session-level** information (entire notebook execution), not **individual Spark stages or tasks**. For that level of detail, use the **Spark History Server**.

---

## Monitor Run Series – performance trends over time

## What it does

**Monitor Run Series** provides **time-series statistics** for your Spark notebook or job definition. It shows performance metrics aggregated over multiple runs.

## Key metrics displayed

- **Execution duration** – how long each run took (trend analysis).
    
- **Peak memory usage** – maximum memory consumed by executors.
    
- **Data read/write volume** – how much data was processed.
    
- **Success rate** – percentage of successful runs over time.
    

## When to use

Use **Monitor Run Series** when:

- You want to **track performance degradation** (e.g., "why is this notebook taking longer each day?").
    
- You are validating the impact of **optimization changes** (e.g., after tuning partition sizes).
    
- You need to identify **resource consumption patterns** for capacity planning.
    

## Exam tip

If a question asks "how do you track whether a Spark notebook's performance is degrading over time?", the answer is **Monitor Run Series**.

---

## Spark History Server – deep-dive optimization tool

## What it is

The **Spark History Server** is a web-based UI (inherited from Apache Spark) that provides **granular visibility** into Spark job execution. It shows:

- **DAG (Directed Acyclic Graph)** – visual representation of Spark stages and dependencies.
    
- **Stage details** – task-level metrics (duration, data shuffle, spill, skew).
    
- **Executor logs** – stdout/stderr logs from Spark executors.
    
- **Query plans** – logical and physical plans for Spark SQL queries.
    
- **Event timeline** – task scheduling and execution timeline.
    

## How to access

1. From the **Monitoring Hub**, click on a specific **notebook run**.
    
2. Click on the **View Details** or **Spark UI** link (depends on Fabric version).
    
3. You are redirected to the **Spark History Server** for that job.
    

---

## Spark History Server – key sections

## Jobs tab

Shows all **Spark jobs** triggered by the notebook. Each notebook cell that executes a Spark action (e.g., `.count()`, `.write()`, `.show()`) creates a job.

## Stages tab

Each **job** is divided into **stages** (logical grouping of tasks). Key metrics:

- **Duration** – how long the stage took.
    
- **Tasks** – number of tasks (parallel units of work).
    
- **Shuffle read/write** – data exchanged between stages.
    
- **Spill (memory/disk)** – data that didn't fit in memory and was written to disk.
    

## Storage tab

Shows **cached DataFrames** or **RDDs** in memory. Useful for verifying that `.cache()` or `.persist()` is working as expected.

## Executors tab

Shows **executor-level metrics**:

- **Active tasks** – tasks currently running on each executor.
    
- **Failed tasks** – tasks that failed and were retried.
    
- **Memory usage** – heap memory, off-heap memory, and storage memory.
    

## SQL tab (for Spark SQL queries)

Shows **query execution plans**:

- **Logical plan** – high-level query structure (joins, filters, aggregations).
    
- **Physical plan** – low-level execution strategy (hash joins, broadcast joins, scans).
    

Use this to identify **query optimization opportunities** (e.g., missing broadcast joins, inefficient filters).

---

## Common Spark optimization patterns

## Partition tuning

**Problem**: Too few partitions → underutilized cluster. Too many partitions → excessive overhead.

**Solution**:

- Use `.repartition(N)` to increase partitions (for large datasets).
    
- Use `.coalesce(N)` to decrease partitions (for small datasets after filtering).
    

**Exam scenario**: "A Spark notebook processes 10GB of data but only uses 2 executors. How do you improve parallelism?" → Increase partitions.

## Data skew handling

**Problem**: One partition has significantly more data than others, causing a **straggler task** that delays the entire stage.

**Solution**:

- Use **salting** (add random key to distribute data).
    
- Use **adaptive query execution (AQE)** to automatically handle skew (enabled by default in Fabric).
    

**Exam scenario**: "One task in a Spark stage takes 10x longer than others." → Data skew issue.

## Broadcast joins

**Problem**: Joining two large tables triggers a **shuffle** (expensive operation).

**Solution**:

- If one table is small (< 10MB by default), use `.broadcast()` to send it to all executors.
    

python

`from pyspark.sql.functions import broadcast df_large.join(broadcast(df_small), "key")`

**Exam scenario**: "A Spark job spends 80% of time in shuffle. One of the joined tables is 5MB." → Use broadcast join.

## Caching/Persisting

**Problem**: Recomputing the same DataFrame multiple times (e.g., used in multiple actions).

**Solution**:

- Use `.cache()` (default: memory) or `.persist(StorageLevel.MEMORY_AND_DISK)` to store intermediate results.
    

python

`df = spark.read.parquet("path/to/data") df_filtered = df.filter(df.age > 30).cache() df_filtered.count()  # Computed and cached df_filtered.show()   # Read from cache`

**Exam scenario**: "A Spark notebook runs the same filter multiple times. How do you improve performance?" → Use `.cache()`.

---

## Self-check / moderator questions

1. Where do you first look when a Spark notebook fails?
    
2. What information does the **Monitoring Hub** show for Spark notebooks?
    
3. What is the difference between **Monitor Run Series** and **Spark History Server**?
    
4. How do you access the **Spark History Server** for a specific notebook run?
    
5. What is a **Spark stage** and how does it relate to a **Spark job**?
    
6. What does **shuffle read/write** indicate in the Stages tab?
    
7. What does **spill (memory/disk)** mean in Spark metrics?
    
8. How do you check if a DataFrame is successfully cached in memory?
    
9. What is **data skew** and how does it impact Spark job performance?
    
10. When should you use `.repartition()` vs. `.coalesce()`?
    
11. What is a **broadcast join** and when should you use it?
    
12. If a Spark notebook runs the same transformation multiple times, how do you optimize it?
    
13. What is the default storage level for `.cache()` in Spark?
    
14. How do you identify which Spark stage is the bottleneck in a job?
    

---

This gives you a complete framework for monitoring and optimizing Spark Notebooks in Fabric. The final section (9.4) will cover **Eventstream Monitoring & Optimization** to complete the data processing tools module.

---
## 9.4 Eventstream Monitoring & Optimization – core idea

**Eventstreams** are the low-code, real-time data ingestion and transformation tool in Fabric. Unlike batch processing tools (Data Pipelines, Dataflows, Notebooks), Eventstreams operate continuously, so monitoring focuses on **throughput metrics** (messages and bytes) and **runtime logs** (warnings, errors, information).

For the DP-700 exam, you need to understand the four key metrics in **Data Insights**, how to interpret **runtime logs**, and how to troubleshoot common Eventstream issues like throttling, backpressure, and destination failures.

---

## Where to monitor Eventstreams

Unlike Data Pipelines and Notebooks, Eventstreams are **not listed in the Monitoring Hub** in the same way. Instead, monitoring happens **within the Eventstream item itself**:

1. Open the **Eventstream** in your workspace.
    
2. Navigate to the **Data Insights** tab (metrics dashboard).
    
3. Navigate to the **Runtime logs** tab (error and warning logs).
    

## Key exam distinction

- **Data Pipeline / Notebook / Dataflow** → monitor in **Monitoring Hub** first, then drill into item-specific logs.
    
- **Eventstream** → monitor **directly in the Eventstream UI** (Data Insights and Runtime logs tabs).
    

---

## Data Insights – four key metrics

The **Data Insights** dashboard provides real-time visibility into Eventstream performance. It tracks **message throughput** and **data volume** over time.

## Four main metrics

## 1. IncomingMessages (Count)

**What it measures**: The number of events or messages **sent to** the Eventstream over a specified period.

**Use cases**:

- Verify that the **source** is actively sending data.
    
- Identify spikes or drops in incoming traffic.
    
- Validate that event ingestion is working as expected.
    

**Exam scenario**: "An Eventstream should be receiving data from an Azure Event Hub, but downstream reports show no data. Where do you check first?" → **IncomingMessages** in Data Insights.

## 2. OutgoingMessages (Count)

**What it measures**: The number of events or messages **flowing out** from the Eventstream to destinations over a specified period.

**Use cases**:

- Verify that the **destination** is receiving data.
    
- Detect backpressure (IncomingMessages > OutgoingMessages).
    
- Confirm that transformations are not filtering out all records.
    

**Exam scenario**: "IncomingMessages shows 10,000 events, but OutgoingMessages shows 0. What is the likely issue?" → Destination configuration error or transformation logic issue.

## 3. IncomingBytes (Bytes)

**What it measures**: The volume of data (in bytes) **ingested** by the Eventstream over a specified period.

**Use cases**:

- Monitor data volume trends (e.g., daily growth, seasonal spikes).
    
- Estimate capacity consumption (larger payloads consume more capacity).
    
- Identify unusually large message sizes.
    

## 4. OutgoingBytes (Bytes)

**What it measures**: The volume of data (in bytes) **sent** from the Eventstream to destinations over a specified period.

**Use cases**:

- Verify that data is being written to destinations.
    
- Compare with IncomingBytes to detect data loss or filtering.
    
- Monitor destination write performance.
    

---

## Interpreting Data Insights metrics – common patterns

## Healthy Eventstream

- **IncomingMessages** ≈ **OutgoingMessages** (steady flow).
    
- **IncomingBytes** ≈ **OutgoingBytes** (minimal transformation overhead).
    
- No spikes or drops in the time series.
    

## Backpressure (destination bottleneck)

- **IncomingMessages** > **OutgoingMessages** (data piling up).
    
- Possible causes:
    
    - Destination is **throttled** (e.g., Lakehouse write limits).
        
    - Destination is **slow** (e.g., external API with rate limits).
        
    - Transformation logic is **too complex** (blocking the pipeline).
        

## Data loss or filtering

- **IncomingMessages** > **OutgoingMessages** (but no errors in logs).
    
- Possible causes:
    
    - **Filter transformation** is removing most events.
        
    - **Schema mismatch** – events don't match expected format and are silently dropped.
        

## Source disconnection

- **IncomingMessages** drops to zero (but Eventstream is running).
    
- Possible causes:
    
    - **Source connection failed** (e.g., Event Hub SAS token expired).
        
    - **Source paused or stopped** (e.g., IoT devices offline).
        

---

## Runtime logs – troubleshooting abnormal behavior

## What are runtime logs?

**Runtime logs** are system-generated logs created by the **Eventstream engine** whenever something abnormal happens. They are not user-defined logs – they are automatically generated by Fabric.

## Three log levels

## 1. Information

- **Severity**: Low.
    
- **Purpose**: Normal operational messages (e.g., "Eventstream started", "transformation applied").
    
- **Action**: No action required – informational only.
    

## 2. Warning

- **Severity**: Medium.
    
- **Purpose**: Potential issues that don't stop the Eventstream but may impact performance or data quality.
    
- **Examples**:
    
    - "Destination write latency is high."
        
    - "Some events were retried due to transient errors."
        
- **Action**: Monitor closely – may need optimization.
    

## 3. Error

- **Severity**: High.
    
- **Purpose**: Critical issues that prevent data flow or cause failures.
    
- **Examples**:
    
    - "Failed to connect to destination."
        
    - "Schema validation error – event rejected."
        
    - "Authentication failure."
        
- **Action**: Immediate troubleshooting required.
    

## How to access runtime logs

1. Open the **Eventstream** item.
    
2. Click on the **Runtime logs** tab.
    
3. Filter by **log level** (information, warning, error).
    
4. Click on a specific log entry to view **detailed error message** and **timestamp**.
    

---

## Common Eventstream issues and troubleshooting

## Issue 1: IncomingMessages = 0 (no data from source)

**Possible causes**:

- Source connection failed (expired credentials, network issue).
    
- Source is not sending data (upstream system offline).
    
- Source configuration is incorrect (wrong Event Hub namespace, topic, or table).
    

**Troubleshooting**:

- Check **Runtime logs** for connection errors.
    
- Verify source credentials (SAS token, connection string, service principal).
    
- Test source connectivity outside of Fabric (e.g., Azure Portal for Event Hubs).
    

## Issue 2: OutgoingMessages = 0 (no data to destination)

**Possible causes**:

- Destination configuration error (wrong Lakehouse table, KQL database, or endpoint).
    
- Transformation logic filters out all events.
    
- Destination authentication failed (item-level permissions, workspace access).
    

**Troubleshooting**:

- Check **Runtime logs** for destination write errors.
    
- Review transformation logic – add a debug output to verify intermediate results.
    
- Verify destination permissions (Contributor or higher on target Lakehouse/KQL database).
    

## Issue 3: IncomingMessages > OutgoingMessages (backpressure)

**Possible causes**:

- Destination is throttled (capacity limits, write quotas).
    
- Transformation is too slow (complex aggregations, joins).
    
- Destination is unavailable (maintenance, outage).
    

**Troubleshooting**:

- Scale destination capacity (increase Lakehouse compute, add Event Hub partitions).
    
- Simplify transformation logic (move heavy processing downstream).
    
- Enable **buffering** or **partitioning** in Eventstream settings (if supported).
    

---

## Optimization best practices for Eventstreams

## 1. Minimize transformation complexity

- Eventstreams are designed for **simple, low-latency transformations** (filtering, column mapping, window aggregations).
    
- For **complex joins or aggregations**, consider using **Spark Structured Streaming** or **KQL Database** instead.
    

## 2. Use appropriate destination partitioning

- When writing to **Lakehouse**, ensure the target table is properly **partitioned** to avoid write contention.
    
- When writing to **KQL Database**, use **batching policies** to optimize ingestion performance.
    

## 3. Monitor capacity consumption

- Eventstreams consume **capacity units** continuously (unlike batch jobs).
    
- Use the **Capacity Metrics App** to track Eventstream capacity usage over time.
    
- Schedule high-volume ingestion during **off-peak hours** if possible.
    

## 4. Enable schema validation at the source

- Use **schema validation** in Eventstream transformations to catch malformed events early.
    
- Reject or route invalid events to a **dead-letter queue** (separate destination) for later analysis.
    

---

## Self-check / moderator questions

1. Where do you monitor Eventstream performance (which UI location)?
    
2. What are the four key metrics in the **Data Insights** dashboard?
    
3. What does **IncomingMessages** measure?
    
4. What does **OutgoingMessages** measure?
    
5. If **IncomingMessages = 10,000** but **OutgoingMessages = 0**, what are two possible causes?
    
6. What does **IncomingBytes** measure, and how does it differ from **IncomingMessages**?
    
7. What are **Runtime logs** and who creates them?
    
8. What are the three log levels in Eventstream runtime logs?
    
9. If an Eventstream shows **IncomingMessages = 0**, how do you troubleshoot the issue?
    
10. What is **backpressure** and how does it manifest in Data Insights metrics?
    
11. What is the difference between monitoring an **Eventstream** vs. monitoring a **Data Pipeline**?
    
12. Why should you avoid complex transformations in Eventstreams?
    
13. Where do you check Eventstream capacity consumption over time?
    

---

This completes **Module 9: Monitor/Optimize Data Processing Tools**. You now have a comprehensive framework for monitoring and optimizing **Data Pipelines**, **Dataflows**, **Spark Notebooks**, and **Eventstreams**. Next up is **Module 10: Monitor/Optimize Data Stores** (Lakehouse, Warehouse, Eventhouse, Semantic Models).

---
---
# 10 Monitor/ Optimize Stores

## 10.1 Warehouse Monitoring & Optimization – core idea

The **Fabric Data Warehouse** is a T-SQL-based relational data store optimized for analytical workloads. Monitoring focuses on **query performance** (execution time, resource consumption) using both UI-based tools (**Query Activity tab**) and T-SQL queries (**queryinsights schema**, **Dynamic Management Views**).

Optimization strategies include **VOrder** (read-optimized Parquet file format), **Query Plans** (analyze execution plans with SHOWPLAN), and **Caching** (automatic in-memory and SSD caching). For the DP-700 exam, you need to understand when to use each monitoring tool and when to disable VOrder.

---

## Two broad groups of monitoring tools

Fabric provides two categories of monitoring tools for the Data Warehouse:

## UI-based monitoring

- **Capacity Metrics App** – capacity consumption across all Warehouse operations.
    
- **Query Activity tab** – query execution history, long-running queries, frequently-run queries (with ability to cancel active queries).
    

## Query-based monitoring (T-SQL)

- **queryinsights schema** – historical query performance data (completed requests, sessions).
    
- **Dynamic Management Views (DMVs)** – live query lifecycle insights (active connections, sessions, requests).
    

---

## Capacity Metrics App – capacity utilization

## What it monitors

The **Capacity Metrics App** tracks **capacity unit (CU) consumption** for Warehouse operations. You can filter by **Warehouse activities** to see which queries or load operations consume the most capacity.

## How to use

1. Install the **Capacity Metrics App** in your Fabric capacity.
    
2. Filter by **item type = Warehouse** to see only Warehouse-related capacity consumption.
    
3. Analyze which operations (queries, loads, refreshes) consume the most CUs.
    

## When to use

- You are experiencing **capacity throttling** and need to identify high-consumption queries.
    
- You want to track **Warehouse capacity trends** over time.
    
- You are planning capacity scaling or optimizing query performance.
    

## Exam tip

If a question asks "how do you identify which Warehouse queries consume the most capacity?", the answer is **Capacity Metrics App** (not Query Activity tab, which focuses on execution time, not capacity consumption).

---

## Query Activity tab – UI-based query monitoring

The **Query Activity tab** is a **native UI** within the Fabric Data Warehouse that provides query execution visibility **without writing T-SQL**. It has three key views:

## 1. Query runs

**What it shows**: All queries that have been (and are currently being) executed against the Warehouse.

**Key features**:

- **Real-time status** – see queries that are currently running.
    
- **Cancel long-running queries** – you can manually cancel a query from this UI.
    
- **Query text** – view the exact SQL statement executed.
    
- **Execution time** – start time, duration, status (succeeded, failed, canceled).
    

**Use case**: You receive a report that "the Warehouse is slow", and you want to quickly identify if a long-running query is blocking other operations.

## 2. Long-running queries

**What it shows**: Queries ordered by their **Median Run Duration** (to expose queries that consistently take a long time).

**Key difference from Query runs**:

- **Query runs** shows individual executions.
    
- **Long-running queries** aggregates multiple executions of the same query and sorts by median duration.
    

**Use case**: You want to identify which queries are **consistently slow** (not just one-time outliers) for optimization.

## 3. Frequently-run queries

**What it shows**: Queries ordered by their **Run Count** (to expose queries that are executed most often).

**Use case**: You want to optimize queries that have the **highest impact** (even if they are fast individually, running them 10,000 times per day can consume significant capacity).

---

## queryinsights schema – T-SQL-based query analysis

The **queryinsights schema** exposes the same data as the **Query Activity tab**, but allows you to perform **custom T-SQL analysis** (joins, filters, aggregations).

## Four key views

## 1. exec_requests_history

**What it returns**: Information about each **completed SQL request/query**.

**Key columns**:

- `request_id` – unique identifier for the query.
    
- `session_id` – session that executed the query.
    
- `start_time`, `end_time`, `total_elapsed_time` – execution timing.
    
- `command` – SQL query text.
    
- `status` – succeeded, failed, canceled.
    

**Use case**: Custom analysis of query performance (e.g., "show all queries that took > 5 minutes in the last 24 hours").

## 2. exec_sessions_history

**What it returns**: Information about each **completed session** (a session can execute multiple queries).

**Use case**: Track which users or applications are querying the Warehouse most frequently.

## 3. frequently_run_queries

**What it returns**: Queries ordered by **Run Count** (similar to the UI view, but queryable with T-SQL).

**Use case**: Identify high-frequency queries for caching or pre-aggregation strategies.

## 4. long_running_queries

**What it returns**: Queries ordered by **query execution time** (similar to the UI view, but queryable with T-SQL).

**Use case**: Identify optimization candidates (queries with high median or max execution time).

---

## Dynamic Management Views (DMVs) – live query monitoring

## What are DMVs?

**Dynamic Management Views** provide **real-time visibility** into active connections, sessions, and requests. Unlike `queryinsights` (which stores historical data), DMVs show **what is happening right now**.

## Three key DMVs

## 1. sys.dm_exec_connections

**What it returns**: Information about each **connection** established between the Warehouse and the engine.

**Use case**: Identify how many active connections are open (useful for troubleshooting connection pool exhaustion).

## 2. sys.dm_exec_sessions

**What it returns**: Information about each **session** authenticated between the item and the engine.

**Use case**: Identify which users are currently connected to the Warehouse.

## 3. sys.dm_exec_requests

**What it returns**: Information about each **active request** in a session.

**Use case**: Identify queries that are **currently running** (not just completed queries).

## Relationship between DMVs

The three DMVs are related hierarchically:

text

`Connection (sys.dm_exec_connections)   ↓ Session (sys.dm_exec_sessions)   ↓ Request (sys.dm_exec_requests)`

- One **connection** can have multiple **sessions**.
    
- One **session** can have multiple **requests** (queries).
    

---

## Optimization tools

## VOrder – optimized Parquet format

## What is VOrder?

**VOrder** is a Fabric-specific optimization applied when writing Parquet files. It reorganizes data within the file to make **reads extremely fast** (at the cost of slightly slower writes).

## Default behavior

By default, the Fabric Data Warehouse **always writes VOrder'd files**.

## When to disable VOrder

You can disable VOrder at the **Warehouse level** (not per-table) with:

sql

`ALTER DATABASE CURRENT SET VORDER = OFF;`

**WARNING**: Disabling VOrder is **irreversible** (you cannot re-enable it).

## When to disable VOrder

Use **VOrder = OFF** for **write-heavy Warehouses**:

- **Raw Warehouse** – ingests data from sources (mostly writes, minimal reads).
    
- **Staging Warehouse** – temporary storage for ETL (high write volume, low read volume).
    

**Do not disable VOrder** for **read-heavy Warehouses**:

- **Analytics Warehouse** – used by Direct Lake semantic models (read-optimized is critical).
    

## Exam scenario

"A Warehouse is used as a staging layer for ETL pipelines and experiences slow write performance. Semantic models do not read from this Warehouse. What optimization should you apply?" → **Disable VOrder**.

---

## Query Plans (SHOWPLAN) – preview feature

## What it does

**SET SHOWPLAN_XML ON** generates a **query execution plan** in XML format, which can be visualized in **SQL Server Management Studio (SSMS)**.

## How to use

1. Connect to the Fabric Warehouse using **SSMS**.
    
2. Run:
    
    sql
    
    `SET SHOWPLAN_XML ON; SELECT * FROM FactSales WHERE Year = 2025;`
    
3. SSMS displays the **execution plan** (operators, costs, joins).
    

## Use case

Identify **query bottlenecks** (missing indexes, inefficient joins, table scans).

## Exam tip

If a question mentions "how do you analyze the execution plan of a T-SQL query in Fabric Warehouse?", the answer is **SET SHOWPLAN_XML ON** (and visualize in SSMS).

---

## Caching – automatic performance optimization

## What is caching?

Fabric Data Warehouse automatically caches query results in two layers:

- **In-memory cache** – fastest (RAM-based).
    
- **SSD cache** – fast (disk-based, larger capacity).
    

## Key characteristics

- **Automatic** – you cannot manually configure or disable caching.
    
- **Transparent** – queries automatically benefit from caching without code changes.
    
- **Invalidation** – cache is invalidated when underlying data changes.
    

## Use case

Repeated queries (e.g., dashboard refreshes) benefit from caching without additional tuning.
**How it works:**  https://learn.microsoft.com/en-us/fabric/data-warehouse/caching

---

## Self-check / moderator questions

1. What are the two broad groups of monitoring tools for Fabric Data Warehouse?
    
2. What is the difference between **Query Activity tab** and **queryinsights schema**?
    
3. Which tool shows **real-time active queries** (not historical)?
    
4. What is the purpose of the **Capacity Metrics App** for Warehouse monitoring?
    
5. What are the three views in the **Query Activity tab**?
    
6. What is the difference between **Long-running queries** and **Frequently-run queries**?
    
7. What does **exec_requests_history** in the `queryinsights` schema return?
    
8. What is the relationship between **sys.dm_exec_connections**, **sys.dm_exec_sessions**, and **sys.dm_exec_requests**?
    
9. What is **VOrder** and what does it optimize?
    
10. When should you **disable VOrder** in a Fabric Warehouse?
    
11. Can you disable VOrder for a specific table only?
    
12. What happens if you disable VOrder (is it reversible)?
    
13. How do you generate a query execution plan in Fabric Warehouse?
    
14. What tool do you use to visualize the execution plan?
    
15. Is Warehouse caching manual or automatic?
    

---

This gives you a complete framework for monitoring and optimizing Fabric Data Warehouse. The next sections will cover **Lakehouse** (10.2), **Eventhouse/KQL** (10.3), and **Semantic Model Refresh** (10.4).

---
## 10.2 Lakehouse Monitoring & Optimization – core idea

**Lakehouse** optimization focuses on **Delta Lake table maintenance** (OPTIMIZE, VACUUM, VOrder) and **partitioning strategies**. Unlike Warehouse (which monitors T-SQL queries), Lakehouse optimization is primarily about **file management** and **Spark performance tuning**.

Monitoring for Lakehouse uses the same **Spark Notebook monitoring tools** covered in section 9.3 (Monitoring Hub, Spark History Server). This section focuses on **optimization-only** techniques specific to Delta Lake tables.

For the DP-700 exam, you need to understand the three Table Maintenance operations, when to apply VOrder at different levels (session, table, cell), and partitioning best practices.

---

## Monitoring Lakehouse (reference to Spark Notebook monitoring)

Since Lakehouse tables are typically read/written using **Spark Notebooks** or **Spark Job Definitions**, monitoring follows the same patterns as **section 9.3: Spark Notebook Monitoring**:

- **Monitoring Hub** – track notebook runs that read/write Lakehouse tables.
    
- **Spark History Server** – analyze Spark job performance (stages, tasks, data shuffle).
    
- **Monitor Run Series** – track performance trends over time.
    

**Key exam point**: There is no separate "Lakehouse Monitoring Hub". You monitor the **Spark jobs that interact with the Lakehouse**, not the Lakehouse itself.

---

## Table Maintenance – UI-based ad-hoc optimization

**Table Maintenance** is a Fabric feature that provides a **UI-based** way to perform Delta Lake maintenance operations without writing code.

## How to access

1. Open your **Lakehouse** in the workspace.
    
2. **Right-click** on any Delta table.
    
3. Select **Maintenance**.
    
4. Choose from three operations: **Optimize**, **VOrder**, **Vacuum**.
    

---

## Three Table Maintenance operations

## 1. OPTIMIZE – file compaction

## What it does

**OPTIMIZE** compacts many small Parquet files into larger Parquet files (ideally **~1GB each**). This is also called **bin-packing**.

## Why it's needed

Over time, Delta tables accumulate **small files** (especially with frequent appends or updates). Small files hurt performance because:

- Spark must open/close many files (I/O overhead).
    
- Metadata operations (listing files) slow down.
    
- Query planning takes longer.
    

## When to use

- After many **incremental loads** (e.g., hourly appends).
    
- When you notice **slow query performance** on a table.
    
- Before running **large analytical queries** or **semantic model refreshes**.
    

## Exam scenario

"A Lakehouse table has 10,000 small Parquet files (average 5MB each) and query performance is degrading. What should you do?" → **Run OPTIMIZE**.

---

## 2. VOrder – read-optimized Parquet format

## What it does

**VOrder** applies Microsoft's proprietary algorithm to reorganize data within Parquet files for **super-fast read performance**. This is especially important for **Direct Lake semantic models** (Power BI reports reading directly from OneLake).

## When to use

- Tables used by **Direct Lake semantic models** (analytics, reporting).
    
- Tables with **read-heavy workloads** (dashboards, BI tools).
    

## When **NOT** to use VOrder (same as Warehouse)

- **Write-heavy tables** (raw ingestion, staging layers).
    
- Tables that are **rarely read** (archival data).
    

---

## 3. VACUUM – remove obsolete files

## What it does

**VACUUM** removes Parquet files that are **no longer part of the Delta log** (e.g., old versions from updates/deletes) after a retention threshold (e.g., 7 days).

## Benefits

- **Reduces OneLake storage costs** (fewer files stored).
    
- **Cleans up outdated files** that are no longer needed.
    

## Trade-off

- **Disables Delta Time Travel** beyond the vacuum retention period.
    
- You **cannot** query historical versions of the table older than the retention threshold.
    

## When to use

- When storage costs are a concern.
    
- When you don't need long-term time travel (e.g., staging tables, raw data).
    

## Exam scenario

"A Lakehouse table consumes 500GB of storage, but only 100GB is current data. The rest is from old versions. Time travel is not required. What should you do?" → **Run VACUUM**.

---

## Code-based optimizations – programmatic table maintenance

The **Table Maintenance UI** is great for ad-hoc operations, but you can also schedule these operations using **Spark SQL** or **PySpark** in a notebook.

## OPTIMIZE – Spark SQL

sql

`%%sql OPTIMIZE <table_name> VORDER;`

**Note**: Adding `VORDER` at the end applies VOrder **after** compaction.

## OPTIMIZE – PySpark

python

`from delta.tables import * deltaTable = DeltaTable.forPath(spark, "Tables/sales") deltaTable.optimize().executeCompaction()`

## VACUUM – Spark SQL

sql

`VACUUM your_delta_table;`

**Default retention**: 7 days (configurable).

---

## VOrder in Lakehouse – three configuration levels

Unlike Warehouse (where VOrder is set at the database level), **Lakehouse VOrder** can be configured at three levels:

## 1. Session-level (applies to all writes in the session)

sql

`%%sql SET spark.sql.parquet.vorder.enabled = TRUE;`

**Use case**: Enable VOrder for all tables written in a specific notebook session.

## 2. Table-level (persistent across all writes to that table)

## During table creation

sql

`%%sql CREATE TABLE person (id INT, name STRING, age INT) USING parquet TBLPROPERTIES("delta.parquet.vorder.enabled" = "true");`

## Alter existing table

sql

`%%sql ALTER TABLE person SET TBLPROPERTIES("delta.parquet.vorder.enabled" = "true");`

**Use case**: Permanently enable VOrder for a specific table (e.g., Gold layer analytics table).

## 3. Cell-level (dataframe writer – one-time write)

python

`df.write \   .format("delta") \  .option("delta.parquet.vorder.enabled", "true") \  .mode("overwrite") \  .saveAsTable("sales")`

**Use case**: Apply VOrder for a single write operation without changing session or table defaults.

---

## VOrder default values

|**Configuration**|**Default Value**|
|---|---|
|Session-level (`spark.sql.parquet.vorder.enabled`)|`true`|
|Table-level (`TBLPROPERTIES("delta.parquet.vorder.enabled")`)|`false`|
|Dataframe writer option (`parquet.vorder.enabled`)|`unset` (inherits session-level)|

**Key exam point**: By default, **session-level VOrder is ON**, but **table-level VOrder is OFF**. If you want a table to always write VOrdered files (regardless of session settings), set it at the **table level**.

---

## VOrder in a Medallion architecture

Similar to Warehouse optimization, you can apply different VOrder strategies across Lakehouse layers:

|**Layer**|**VOrder**|**Reason**|
|---|---|---|
|**BRONZE** (raw ingestion)|OFF|Write-heavy, minimal reads|
|**SILVER** (transformed)|OFF|Still write-heavy, intermediate processing|
|**GOLD** (analytics)|ON|Read-heavy, used by semantic models|

**Key exam point**: Only the **GOLD layer** (used for BI/analytics) should have VOrder enabled. Bronze/Silver layers benefit from faster writes by disabling VOrder.

---

## Partitioning – distributed processing optimization

## What is partitioning?

**Partitioning** splits a large table into smaller **physical subdirectories** based on column values (e.g., partition by `year`, `month`). Spark can then process each partition in parallel.

## Benefits

- **Parallel processing** – Spark reads multiple partitions simultaneously.
    
- **Data skipping** – Spark only reads relevant partitions (e.g., "WHERE year = 2025" skips other years).
    
- **Improved performance** – especially for large tables (>1GB).
    

## Implementing partitioning in PySpark

python

`df.write \   .mode("overwrite") \  .format("delta") \  .partitionBy("year", "month") \  .save("Tables/flights_partitioned")`

---

## Partitioning best practices

## 1. Don't over-optimize early

- **Wait** until you have **large datasets** (millions of rows) before partitioning.
    
- Premature partitioning causes the **small file problem** (many tiny partitions).
    

## 2. Choose partition columns carefully

- **High cardinality** = bad (e.g., `customer_id` with millions of values → millions of partitions).
    
- **Low cardinality** = good (e.g., `year`, `region`, `status` with a few distinct values).
    
- **Commonly filtered** = ideal (e.g., "WHERE year = 2025" benefits from year partitioning).
    

## 3. Aim for ~1GB partitions

- Too small (< 100MB) → small file problem.
    
- Too large (> 2GB) → limited parallelism.
    
- **Optimal** → ~1GB per partition.
    

---

## Self-check / moderator questions

1. What is the difference between **OPTIMIZE** and **VOrder**?
    
2. What does **VACUUM** do, and what is the trade-off?
    
3. How do you access **Table Maintenance** in the Lakehouse UI?
    
4. What is the Spark SQL command to run OPTIMIZE with VOrder?
    
5. At which three levels can you configure VOrder in Lakehouse?
    
6. What is the default value for **session-level VOrder**?
    
7. What is the default value for **table-level VOrder**?
    
8. Why should you **disable VOrder** in the Bronze and Silver layers of a Medallion architecture?
    
9. What is **partitioning** and how does it improve Spark performance?
    
10. What are the three best practices for partitioning Delta tables?
    
11. What is the **small file problem** and how does OPTIMIZE solve it?
    
12. Can you use Delta Time Travel after running VACUUM?
    
13. If a table has 10,000 small files (5MB each), which operation should you run?
    
14. If a table is used by a Direct Lake semantic model, should you enable VOrder?
    

---

This completes **10.2 Lakehouse Monitoring & Optimization**. The next sections will cover **Eventhouse/KQL** (10.3) and **Semantic Model Refresh** (10.4) to complete the data stores module.

---
## 10.3 Eventhouse/ KQL Monitoring & Optimization – core idea

**Eventhouse** is Fabric's real-time analytics engine powered by **Kusto Query Language (KQL)**. Monitoring focuses on **capacity consumption** (Real-Time Intelligence items consume CUs at a high rate) and **workspace-level monitoring** (auto-provisioned Monitoring Eventhouse with query logs, ingestion logs, metrics).

Optimization centers on **KQL best practices**: reducing data volume early in queries, using efficient string operators (`has` vs. `contains`), and applying case-sensitive operators when possible. For the DP-700 exam, you need to understand how to enable Workspace Monitoring and the key KQL optimization principles.

---

## Monitoring Eventhouse

## Capacity Metrics App – high-rate CU consumption

## Why it matters

**Real-Time Intelligence (RTI) items** (Eventstreams, Eventhouses, KQL databases) consume **capacity units at a very high rate** compared to batch processing tools (pipelines, notebooks).

## How to use

1. Install the **Capacity Metrics App** in your Fabric capacity.
    
2. Filter by **Eventhouse** or **KQL database** activities.
    
3. Analyze which queries or ingestion operations consume the most capacity.
    

## Key exam point

If a question mentions "your Real-Time Intelligence solution is experiencing throttling", the first step is to check **Capacity Metrics App** to identify high-consumption queries or ingestion streams.

---

## Workspace Monitoring – Eventhouse to monitor Eventhouses

## What is Workspace Monitoring?

**Workspace Monitoring** is a **preview feature** that auto-provisions a **Monitoring Eventhouse** when enabled at the workspace level. This Eventhouse stores detailed logs for all workspace items, including:

- **Eventhouses** (query logs, ingestion logs, metrics)
    
- **Semantic models**
    
- **Mirrored databases**
    
- **GraphQL operations**
    

## How to enable

1. Open **Workspace Settings**.
    
2. Navigate to **Workspace Monitoring (Preview)**.
    
3. Toggle **Enable Workspace Monitoring**.
    
4. Fabric creates a **Monitoring Eventhouse** in your workspace.
    

## Key distinction

- **Monitoring Hub** = does **not** include Eventhouse query logs.
    
- **Workspace Monitoring Eventhouse** = stores **detailed KQL query logs** and ingestion metrics.
    

---

## Eventhouse Monitoring Tables

When you enable Workspace Monitoring, the **Monitoring Eventhouse** contains five key tables:

## 1. EventhouseCommandLogs

**What it tracks**: List of **commands** run on an Eventhouse KQL database (e.g., `.create table`, `.alter policy`, `.show tables`).

**Use case**: Track administrative operations (schema changes, policy updates).

## 2. EventhouseDataOperationLogs

**What it tracks**: List of **data operations** (e.g., ingestion, exports, materialized view refreshes).

**Use case**: Monitor data movement into/out of the Eventhouse.

## 3. EventhouseIngestionResultLogs

**What it tracks**: Results from **data ingestion operations** (succeeded, failed, rows ingested).

**Use case**: Troubleshoot ingestion failures (missing data, schema mismatches).

## 4. EventhouseMetrics

**What it tracks**: Metrics for **ingestions**, **materialized views**, and **continuous exports** (throughput, latency, errors).

**Use case**: Monitor performance trends over time.

## 5. EventhouseQueryLogs

**What it tracks**: List of **KQL queries** executed on the Eventhouse (query text, execution time, user, status).

**Use case**: Identify slow queries, frequently-run queries, and query failures.

---

## Using Monitoring Eventhouse for troubleshooting

## Example: Identify slow queries

text

`EventhouseQueryLogs | where Duration > 5s  // Queries taking > 5 seconds | project Timestamp, User, QueryText, Duration | order by Duration desc`

## Example: Track ingestion failures

text

`EventhouseIngestionResultLogs | where Status == "Failed" | project Timestamp, Database, Table, ErrorMessage | order by Timestamp desc`

## Example: Monitor query frequency

text

`EventhouseQueryLogs | summarize QueryCount = count() by QueryText | order by QueryCount desc | take 10  // Top 10 most frequently run queries`

---

## KQL Optimization and Best Practices

**Reference**: [MICROSOFT 🔗 Best practices for Kusto Query Language queries](https://learn.microsoft.com/en-us/kusto/query/best-practices?view=microsoft-fabric)

KQL is intuitive for ad-hoc queries, but optimization is critical for production workloads (large datasets, frequent queries, capacity constraints).

---

## Key optimization principle: Reduce data volume early

## Core concept

**"A query's performance depends directly on the amount of data it needs to process. The less data is processed, the quicker the query (and the fewer resources it consumes)."**

KQL queries execute **top-to-bottom**. Apply filters and projections **as early as possible** to minimize the data passed to subsequent operations.

## Example: BAD (filter late)

text

`SensorReadings | join SensorMetadata on SensorID between ['1221' ... '1229'] | where SensorID between ['1221' ... '1229']`

**Problem**: The `join` processes **all** rows from `SensorReadings` before filtering.

## Example: GOOD (filter early)

text

`SensorReadings | where SensorID between ['1221' ... '1229']  // Filter FIRST | join SensorMetadata on SensorID`

**Benefit**: The `join` only processes the filtered subset of data.

---

## Example: Add time-based filtering

## BAD (no time filter)

text

`SensorReadings | where SensorID == "123" | join SensorMetadata on SensorID`

**Problem**: Scans the entire table history (potentially years of data).

## GOOD (time filter first)

text

`SensorReadings | where Timestamp > ago(24h)  // Filter to last 24 hours FIRST | where SensorID == "123" | join SensorMetadata on SensorID`

**Benefit**: KQL uses time-based indexing to skip irrelevant data shards.

---

## String operator optimization

## `has` vs. `contains`

|**Operator**|**Match Type**|**Performance**|**Use Case**|
|---|---|---|---|
|`has`|**Exact token match**|Fast (uses index)|Search for full words (e.g., "error", "warning")|
|`contains`|**Substring match**|Slower (full scan)|Search for partial strings (e.g., "err" matches "error", "terror")|

## Example

text

`// GOOD: Fast (indexed search) Logs | where Message has "error" // BAD: Slow (substring scan) Logs | where Message contains "err"`

**Exam tip**: If a question asks "how do you optimize a KQL query searching for the word 'error' in log messages?", the answer is **use `has` instead of `contains`**.

---

## Case-sensitive operator optimization

## `has` vs. `has_cs`

|**Operator**|**Case Sensitivity**|**Performance**|**Use Case**|
|---|---|---|---|
|`has`|Case-insensitive|Slower|When you don't know the exact case|
|`has_cs`|Case-sensitive|Faster (more selective)|When you know the exact case|

## Example

text

`// GOOD: Fast (exact case match) Logs | where Severity has_cs "ERROR" // BAD: Slower (case-insensitive) Logs | where Severity has "error"`

## Equality operators

|**Operator**|**Case Sensitivity**|**Performance**|
|---|---|---|
|`==`|Case-sensitive|Fast|
|`=~`|Case-insensitive|Slower|

---

## Additional KQL best practices (from Microsoft docs)

## 1. Use `datetime` columns for time filtering

- KQL has **efficient indexing** on `datetime` columns.
    
- Always filter by time **early** in the query.
    

text

`// GOOD Events | where Timestamp > ago(1h) | where EventType == "UserLogin"`

## 2. Avoid `*` (full-text search)

text

`// BAD: Searches all columns Events | where * has "error" // GOOD: Search specific column Events | where Message has "error"`

## 3. Use `materialize()` for reused expressions

text

`let FilteredData = materialize(     Events    | where Timestamp > ago(1h)    | where Severity == "Error" ); FilteredData | summarize count() by EventType; FilteredData | summarize avg(Duration) by User;`

**Benefit**: The filtered dataset is computed **once** and reused.

---

## Self-check / moderator questions

1. Why do **Real-Time Intelligence (RTI) items** consume capacity units at a high rate?
    
2. Where do you monitor **Eventhouse capacity consumption**?
    
3. What is **Workspace Monitoring** and how do you enable it?
    
4. What happens when you enable Workspace Monitoring in a workspace?
    
5. What are the five tables in the **Monitoring Eventhouse**?
    
6. Which table tracks **KQL query execution** in the Monitoring Eventhouse?
    
7. Which table tracks **ingestion failures** in the Monitoring Eventhouse?
    
8. What is the most important KQL optimization principle?
    
9. Why should you apply **time-based filters early** in a KQL query?
    
10. What is the difference between **`has`** and **`contains`**?
    
11. When should you use **`has_cs`** instead of **`has`**?
    
12. What is the difference between **`==`** and **`=~`**?
    
13. Why should you avoid using **`*`** (wildcard) in KQL queries?
    
14. What does **`materialize()`** do and when should you use it?
    
15. If a KQL query scans millions of rows but only needs data from the last 24 hours, what optimization should you apply?
    

---

This completes **10.3 Eventhouse/KQL Monitoring & Optimization**. The final section (10.4) will cover **Semantic Model Refresh Monitoring** to complete Module 10.

---
## 10.4 Semantic Model Refresh Monitoring – core idea

**Semantic Model refresh** is the process of updating Power BI datasets with the latest data from source systems. Monitoring depends on **how the refresh was triggered**: manual/scheduled refreshes and pipeline-triggered refreshes are monitored via **Monitoring Hub**, while **Semantic Link** (Python-based) provides programmatic monitoring with `fabric.list_refresh_requests()`.

For the DP-700 exam, you need to understand the four refresh trigger methods, where to monitor each type, and how to use Semantic Link for refresh orchestration and monitoring.

---

## Four ways to trigger Semantic Model refresh

As covered in the **Triggering section (Module 4.2)**, there are four methods to refresh a Semantic Model:

## 1. Direct Lake auto-refresh

**What it is**: Automatic refresh triggered when the underlying OneLake data changes (for Direct Lake semantic models only).

**How it works**: Fabric detects changes in the Lakehouse/Warehouse and automatically refreshes the semantic model without manual intervention.

**When to use**: When your semantic model uses **Direct Lake mode** and you want near-real-time data without scheduling.

## 2. Scheduled refresh

**What it is**: Pre-configured refresh schedule set in the **Semantic Model Settings**.

**How it works**: You define a refresh frequency (e.g., daily at 6 AM) and Fabric executes the refresh automatically.

**When to use**: For **Import mode** semantic models or when you need predictable, regular refresh cycles.

## 3. Data Pipeline: Semantic Model Refresh activity

**What it is**: A dedicated **Semantic Model Refresh activity** in a Data Pipeline that triggers the refresh as part of an orchestration flow.

**How it works**: The pipeline executes the refresh activity after upstream data processing (e.g., after a notebook loads data into a Lakehouse).

**When to use**: When you need **orchestrated refreshes** that depend on other pipeline activities completing first.

## 4. Semantic Link (sempy)

**What it is**: Python-based refresh using the **Semantic Link library** (`sempy.fabric`).

**How it works**: You call `fabric.refresh_dataset()` from a notebook to trigger the refresh programmatically.

**When to use**: When you need **dynamic, conditional refresh logic** (e.g., "refresh only if new data is available") or **partition-level refreshes**.

---

## Monitoring Hub – primary monitoring location

## What it monitors

The **Monitoring Hub** is the first place to check when you want to monitor Semantic Model refreshes. It tracks:

- **Manual refreshes** (triggered by clicking "Refresh now" in the UI).
    
- **Scheduled refreshes** (configured in Semantic Model Settings).
    
- **Pipeline-triggered refreshes** (via Semantic Model Refresh activity).
    

## How to use

1. Open the **Monitoring Hub**.
    
2. Filter by **Semantic model** to see all semantic model refresh runs.
    
3. Find the semantic model you care about and **right-click → Historical runs**.
    
4. You see the **full refresh history** (succeeded, failed, in progress, canceled).
    

## Drilling into refresh details

Click on a specific refresh run to view:

- **Start time** and **End time** – when the refresh began and completed.
    
- **Duration** – how long the refresh took.
    
- **Status** – succeeded, failed, or canceled.
    
- **Error details** (if failed) – specific error message and failure reason.
    
- **Refresh type** – full refresh or incremental refresh.
    
- **Tables refreshed** – which tables were updated (for partition-level refreshes).
    

## Key exam point

If a question asks "where do you check the status of a scheduled semantic model refresh?", the answer is **Monitoring Hub**.

---

## Semantic Link – programmatic refresh and monitoring

## What is Semantic Link?

**Semantic Link** (`sempy`) is a Python library for interacting with Power BI semantic models from Fabric notebooks. It supports:

- **Triggering refreshes** (`fabric.refresh_dataset()`).
    
- **Monitoring refresh status** (`fabric.list_refresh_requests()`).
    
- **Querying semantic model metadata** (tables, columns, relationships).
    

## Triggering a refresh with Semantic Link

python

`import sempy.fabric as fabric # Set workspace and semantic model names workspace_name = "Fabric D..." semantic_model_name = "sales_analytics" # Trigger a full refresh fabric.refresh_dataset(workspace=workspace_name, dataset=semantic_model_name)`

**Note**: This triggers a **full refresh** of the entire semantic model.

---

## Partition-level refresh with Semantic Link

## What is partition-level refresh?

Instead of refreshing the **entire semantic model**, you can refresh **specific tables or partitions** (e.g., only refresh the "Sales_2025" partition).

## How to implement

python

`import sempy.fabric as fabric # Trigger partition-level refresh fabric.refresh_dataset(     workspace="Fabric D...",    dataset="sales_analytics",    refresh_type="automatic",  # or "full", "dataOnly", etc.    objects=[        {"table": "Sales", "partition": "Sales_2025_Q1"}    ] )`

**Use case**: Large semantic models where refreshing the entire model takes hours. Partition-level refresh allows you to refresh only the changed data.

**Reference**: [Semantic Link documentation for partition-level refresh](https://learn.microsoft.com/en-us/python/api/semantic-link-sempy/sempy.fabric?view=semantic-link-python#sempy-fabric-refresh-dataset)

---

## Monitoring refreshes with Semantic Link

## Using `fabric.list_refresh_requests()`

After triggering a refresh, you can monitor its status programmatically:

python

`import sempy.fabric as fabric # Get refresh history for a semantic model df = fabric.list_refresh_requests(dataset="sales_analytics") # Display refresh history as a Pandas DataFrame display(df)`

## What the DataFrame contains

|**Column**|**Description**|
|---|---|
|`Request ID`|Unique identifier for the refresh request|
|`Refresh Type`|Full, incremental, or partition-level|
|`Start Time`|When the refresh started|
|`End Time`|When the refresh completed (or null if still running)|
|`Status`|Completed, Failed, In Progress, Cancelled|
|`Service Exception (JSON)`|Error details (if failed)|

## Use cases

- **Track refresh performance** – analyze refresh duration trends over time.
    
- **Automate failure alerts** – check if the last refresh failed and send a notification.
    
- **Debug refresh issues** – extract error messages from `Service Exception (JSON)`.
    

---

## Comparison: Monitoring Hub vs. Semantic Link

|**Feature**|**Monitoring Hub**|**Semantic Link**|
|---|---|---|
|**Monitoring scope**|All semantic model refreshes (manual, scheduled, pipeline)|Only refreshes triggered via Semantic Link or API|
|**UI vs. Code**|UI-based (point-and-click)|Code-based (Python notebook)|
|**Filtering**|Filter by workspace, item type, status|Query refresh history with pandas (custom filtering)|
|**Use case**|Quick troubleshooting, visual inspection|Automated monitoring, custom analytics, programmatic alerts|

---

## Self-check / moderator questions

1. What are the four ways to trigger a Semantic Model refresh?
    
2. What is **Direct Lake auto-refresh** and when should you use it?
    
3. Where do you monitor **scheduled semantic model refreshes**?
    
4. Where do you monitor **pipeline-triggered semantic model refreshes**?
    
5. How do you access the **Historical runs** for a semantic model in Monitoring Hub?
    
6. What information is displayed in the **refresh details** view?
    
7. What is **Semantic Link** and what library do you import to use it?
    
8. What is the Python function to **trigger a semantic model refresh**?
    
9. What is the Python function to **monitor semantic model refresh status**?
    
10. What is the difference between a **full refresh** and a **partition-level refresh**?
    
11. Why would you use a **partition-level refresh** instead of a full refresh?
    
12. What does `fabric.list_refresh_requests()` return?
    
13. Can you use **Monitoring Hub** to monitor refreshes triggered by Semantic Link?
    
14. When should you use **Semantic Link** instead of the **Monitoring Hub**?
    

---

## 🎉 Module 10 Complete: Monitor/Optimize Data Stores

You've now completed all four sections of **Module 10**:

- **10.1 Warehouse** – Query Activity tab, DMVs, queryinsights, VOrder, SHOWPLAN, caching
    
- **10.2 Lakehouse** – OPTIMIZE, VACUUM, VOrder (session/table/cell), partitioning
    
- **10.3 Eventhouse/KQL** – Workspace Monitoring Eventhouse, KQL best practices (`has` vs. `contains`, reduce data early)
    
- **10.4 Semantic Model** – Monitoring Hub, Semantic Link (refresh and monitor)
    

This completes the **entire monitoring and optimization section** of the DP-700 exam. You now have a complete end-to-end framework for monitoring and optimizing **data processing tools** (pipelines, dataflows, notebooks, eventstreams) and **data stores** (warehouse, lakehouse, eventhouse, semantic models).

---
---

