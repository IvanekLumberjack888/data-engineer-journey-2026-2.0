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
