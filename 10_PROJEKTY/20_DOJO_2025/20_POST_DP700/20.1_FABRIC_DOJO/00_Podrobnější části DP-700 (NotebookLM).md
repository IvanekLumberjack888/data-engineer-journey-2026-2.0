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

