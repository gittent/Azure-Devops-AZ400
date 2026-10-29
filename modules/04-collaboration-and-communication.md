# Module 04: Collaboration & Communication

> **Course:** AZ-400 — Designing and Implementing Microsoft DevOps Solutions  
> **Instructor:** Andrew Brown (ExamPro)  
> ⬅️ [Previous: 03. Azure Boards Deep Dive](03-azure-boards-deep-dive.md) | [Main Index](../README.md) | ➡️ [Next: 05. GitHub Fundamentals & Architecture](05-github-fundamentals.md)

---

## 📑 Module Overview

- [Custom Azure Boards Dashboards](#custom-azure-boards-dashboards)
- [Wikis for Documentation](#wikis-for-documentation) *(Coming next)*
- [Process Diagrams for Documentation](#process-diagrams-for-documentation) *(Coming next)*
- [Configure Release Documentation](#configure-release-documentation) *(Coming next)*
- [API Documentation](#api-documentation) *(Coming next)*
- [Automate Git History Documentation](#automate-git-history-documentation) *(Coming next)*
- [What are Webhooks](#what-are-webhooks) *(Coming next)*
- [Configure Notifications with Webhooks](#configure-notifications-with-webhooks) *(Coming next)*

---

### Custom Azure Boards Dashboards

#### 1. Slide Transcripts (As-Is)

##### Part 1: Overview, Widgets & Query Widgets
> **Custom Azure Boards dashboards**  
> *Cheat sheets, Practice Exams and Flash cards 👉 www.exampro.co/az-400*
>
> **Centralize with Custom Dashboards**  
> **Custom dashboards in Azure Boards** are crucial for presenting a comprehensive **overview of your project's status and key metrics**.
> - By tailoring these dashboards to highlight crucial data, your team can streamline workflows and improve decision-making.
>
> **Customize with Widgets**  
> **Widgets** are the heart of Azure Boards dashboards, presenting diverse data from **progress charts to work item queries**. Select and tailor widgets that best display the team's critical information, ensuring essential insights are readily accessible.
>
> **Monitor Backlogs with Query Widgets**  
> Incorporate **query widgets** to **filter and display work items based on defined criteria**, like outstanding tasks per team member.  
> This enables efficient task management and helps in setting clear priorities.
>
> *(UI Callouts: Overview -> Dashboards in navigation; Add Widget dialog showing 'Velocity' by Microsoft; 'Query Results' widget displaying results from a query; 'Query Tile' widget displaying total number of results for a query).*

##### Part 2: Burndown, Performance Charts & Team Engagement
> **Custom Azure Boards dashboards**  
> *Cheat sheets, Practice Exams and Flash cards 👉 www.exampro.co/az-400*
>
> **Track Progress with Burndown Charts**  
> Use **burndown chart** widgets to graphically **track project progress**, helping to identify any delays. Regular review of these charts keeps the team's progress aligned with project goals.
>
> **Visualize Performance with Charts**  
> Enrich your dashboard with charts that **convey performance metrics**, such as **bug trends or team velocity**, providing a clear picture of the team's dynamics and highlighting areas for improvement.
>
> **Enhance Team Engagement**  
> Share dashboards with your **team and stakeholders** to offer a **live view of the project's status**, fostering a culture of transparency and collective accountability.
>
> *(UI Callouts: 'Burndown' widget displaying burndown across multiple teams and sprints; 'Chart for Build History' widget showing build history of a selected build definition; Example Dashboard showing tiles for Completed Work [50], Active Work [10], Planned Work [76], Unplanned Work [27], Work Moved Out [34], Backlog and tags [220], Team Velocity bar charts, and Sprint Burndown area chart).*

---

#### 2. Visual References

![Custom Azure Boards Dashboards Part 1](../images/04-custom-azure-boards-dashboards-part1.png)

![Custom Azure Boards Dashboards Part 2](../images/04-custom-azure-boards-dashboards-part2.png)

---

#### 3. Expert-Level Deep Dive & Practical Notes

- **Dashboard Architecture: Team vs Project Dashboards**:
  - In Azure DevOps, dashboards can be configured at two levels:
    1. **Team Dashboards**: Owned by a specific team (e.g., *Frontend Team*, *Core API Team*). Each team can have multiple dashboards.
    2. **Project Dashboards**: Visible to everyone across all teams in the project, ideal for executive roll-up views and cross-team alignment.
  - Dashboards are accessed via **Overview -> Dashboards** in the left sidebar navigation.

```mermaid
graph TD
    Project[Azure DevOps Project] --> TeamA[Team A: Mobile App]
    Project --> TeamB[Team B: Backend Services]
    TeamA --> DashA1[Sprint 12 Operational Dashboard]
    TeamA --> DashA2[Bug Quality & Defect Density]
    TeamB --> DashB1[CI/CD Build & Deployment Health]
    Project --> ExecDash[Executive Roll-up: Cross-Team Velocity & Epics]
```

---

- **Core Widget Taxonomy & Capabilities**:

  | Category | Key Widgets | Purpose & What It Measures |
  | :--- | :--- | :--- |
  | **Work Item Tracking** | **Query Tile** | Single large metric showing count of matching work items (e.g., *Active P1 Bugs: 4*). Supports conditional color rules. |
  | | **Query Results** | Paginated tabular list of work items from a shared query with sortable columns. |
  | | **Assigned to Me** | Filtered personal view for the logged-in user. |
  | **Flow & Agile Metrics** | **Velocity** | Compares planned work vs. delivered work in Story Points/Effort across previous sprints. |
  | | **Burndown / Burnup** | Remaining work hours or work item count versus ideal trend line over time. |
  | | **Cumulative Flow Diagram (CFD)** | Work in Progress (WIP), Cycle Time, and bottleneck identification across Kanban columns. |
  | | **Lead Time & Cycle Time** | Time elapsed from creation/active state to completion. |
  | **Build & Pipeline Health** | **Build History** | Visual bar chart of recent runs (success/failure) for a specific CI/CD pipeline. |
  | | **Deployment Status** | Tracks stage-by-stage deployment across environments (Dev -> QA -> Prod). |
  | **Extensibility & Analytics** | **Markdown / Embedded Webpage** | Custom instructions, team mission, external runbooks, or PowerBI reports. |

---

- **Configuring Query-Based Widgets (Step-by-Step)**:
  1. **Step 1: Create a Shared Query**:
     - Navigate to **Boards -> Queries -> + New query**.
     - Specify query criteria, e.g.:
       - `Work Item Type = Bug`
       - `State = Active`
       - `Priority <= 2`
     - Save query under **Shared Queries** (Widgets *cannot* read queries saved under *My Queries* when shared with team members).
  2. **Step 2: Add Widget to Dashboard**:
     - Go to **Overview -> Dashboards**.
     - Click **Edit** (pencil icon at top right) -> search for **Query Tile** or **Chart for Work Items** -> click **Add**.
  3. **Step 3: Configure Widget Properties**:
     - Click the widget gear icon -> select the Shared Query created in Step 1.
     - For **Query Tile**: Define color thresholds (e.g., turn green if count is 0, yellow if 1-3, red if >= 4).
     - For **Chart for Work Items**: Select chart type (Pie, Bar, Pivot table), grouping field (e.g., `Assigned To`), and value (`Count of Work Items`).

---

- **Executive & Stakeholder Dashboards (AZ-400 Best Practice)**:
  - Non-developers (managers, clients, stakeholders) holding free **Stakeholder Access** licenses can view dashboards and interact with charts.
  - Best practice dashboard layout:
    - **Top Row**: High-level status tiles (Active Blockers, Sprint Days Remaining, Critical Vulnerabilities).
    - **Middle Row**: Progress & flow widgets (Sprint Burndown, Team Velocity).
    - **Bottom Row**: Deployment & quality status (Build History, Code Quality / SonarQube scorecards).

> [!TIP]
> **AZ-400 Exam Tip**:
> - For a dashboard widget to display work items to other team members, the underlying query **MUST be saved in the `Shared Queries` folder**, not `My Queries`. If saved in `My Queries`, other users will see an access error on the dashboard.
> - **Stakeholder** license holders can view dashboards, run shared queries, and view charts at no additional licensing cost.

---

### Wikis for Documentation
*Awaiting slide content / screenshot...*

### Process Diagrams for Documentation
*Awaiting slide content / screenshot...*

### Configure Release Documentation
*Awaiting slide content / screenshot...*

### API Documentation
*Awaiting slide content / screenshot...*

### Automate Git History Documentation
*Awaiting slide content / screenshot...*

### What are Webhooks
*Awaiting slide content / screenshot...*

### Configure Notifications with Webhooks
*Awaiting slide content / screenshot...*
