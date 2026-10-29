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

#### 1. Slide Transcripts (As-Is)

##### Part 1: Overview & Project Requirements
> **Wiki for Documentation**  
> *Cheat sheets, Practice Exams and Flash cards 👉 www.exampro.co/az-400*
>
> **Wiki offers a collaborative space for team members to compile and share crucial details about a DevOps project.**
>
> **Start with an Overview Page:**  
> Begin by setting up an **overview page**. This should introduce the **project, its goals, and the team working** on it.  
> Mention the **technologies, tools, and methods your project** employs, keeping it broad but informative.
>
> *(UI Callout: Example 'Project Overview' containing Welcome message, Team Members list [Alex Johnson - Project Manager, Jamie Doe - Lead Developer, Chris Smith - QA Engineer, Jordan Lee - UI/UX Designer], and Technologies & Tools [Frontend: React.js/Redux, Backend: Node.js/Express, Database: MongoDB, CI/CD: Jenkins/Azure Pipelines, Version Control: Git/Azure Repos]).*
>
> **Detail Project Requirements:**  
> Dedicate pages to outline the **project's requirements**.  
> Break down what the project **needs to do (functional requirements)** and how it should perform **(non-functional requirements)**, using clear and achievable language.  
> Add **user stories**, what needs to be true for the project to be considered complete **(acceptance criteria)**, and any other elements that rely on each other **(dependencies)**.
>
> *(UI Callout: Example 'Project Requirements' containing Functional Requirements [create account, edit profile], Non-Functional Requirements [load within 3 seconds, data protection compliance], User Stories, Acceptance Criteria, and Dependencies).*

##### Part 2: Architecture & Collaborative Input
> **Wiki for Documentation**  
> *Cheat sheets, Practice Exams and Flash cards 👉 www.exampro.co/az-400*
>
> **Architecture and Design Documentation:**  
> Use the wiki to detail the **project's structure and design**. Make a separate page for each part, whether it's **a component, a larger section, or a service**.  
> To help visualize how these parts interact, include diagrams like **UML (Unified Modeling Language)** or system architecture sketches.
>
> *(UI Callout: Example 'Architecture and Design' containing Overview of microservices architecture, User Service breakdown [responsibilities, Node.js/JWT], Email Service breakdown [SendGrid, Azure Functions]).*
>
> **Encourage Team Input:**  
> Get your team involved in the documentation process.  
> Allowing everyone to **edit and update wiki pages** not only promotes teamwork but also helps keep the information **current**.  
> Make sure to use the wiki's version tracking to monitor changes and roll back if needed.
>
> *(UI Callout: Example 'Collaborative Content Creation' covering editing instructions, commit messages, and Version Tracking to view change history and revert).*

##### Part 3: Live Markdown Editor Interface
> **Azure DevOps Services Portal — Wiki Editor Walkthrough**  
> **Path**: `Overview -> Wiki -> Example Wiki Markdown` (`dev.azure.com/exampro1/examprotest`)  
> - **Dual-Pane View**: Split editor with Raw Markdown on the left and Live Rendered HTML Preview on the right.  
> - **Formatting Toolbar**: Bold, Italics, Strikethrough, Headings (H1/H2/H3), Bulleted/Numbered Lists, Checklists, Blockquotes, Code blocks, Tables, Links, and Image uploads.  
> - **Version Tracking & Actions**: Page revisions, Clone wiki, Print, and Link to work items.

---

#### 2. Visual References

![Wiki for Documentation Overview & Requirements](../images/04-wikis-for-documentation-part1.png)

![Wiki Architecture and Collaborative Editing](../images/04-wikis-for-documentation-part2.png)

![Azure DevOps Live Wiki Markdown Editor](../images/04-wikis-markdown-editor-live-preview.png)

---

#### 3. Expert-Level Deep Dive & Practical Notes

- **Project Wiki vs. Publish Code as Wiki (AZ-400 Core Knowledge)**:
  - In Azure DevOps, there are **two distinct types** of Wikis. Understanding the architectural differences between them is one of the most frequently tested concepts on the AZ-400 exam:

  | Architectural Capability | **Project Wiki** (Built-in Provisioned Wiki) | **Publish Code as Wiki** (Git Repository Wiki) |
  | :--- | :--- | :--- |
  | **Storage Mechanism** | Hidden backend Git repo managed internally by Azure DevOps | Standard Git repository (or subfolder, e.g. `/docs`) inside Azure Repos |
  | **Branch Policies & PR Workflow** | ❌ No PRs; changes committed directly to main wiki branch | ✅ Full PR support, branch protection, peer code review policies |
  | **Multi-Version / Branching Documentation** | ❌ Single version only | ✅ Multi-version (publish separate docs per release branch e.g. `v1.0`, `v2.0`) |
  | **Local IDE Offline Editing** | Cloned via special hidden Git URL | Standard Git clone (`git clone`) with VS Code / Markdown editors |
  | **Max Page Limit & Hierarchy** | Up to 1 GB repo size; sub-pages reordered via drag-and-drop | Defined by folder structure and `.order` metadata files |
  | **Auditing & History** | Revision history visible in portal | Full `git log`, blame, and commit SHAs |

```mermaid
flowchart TD
    subgraph Options ["Azure DevOps Wiki Deployment Options"]
        PW["1. Create Project Wiki<br/>(Ad-hoc, team collaboration, quick notes)"]
        CW["2. Publish Code as Wiki<br/>(Docs-as-Code, PR-gated, versioned docs)"]
    end

    PW --> PWHidden["Hidden Git Repo<br/>No Branch Policies<br/>Direct Online Editing"]
    CW --> CWGit["Standard Azure Repo (/docs)<br/>Enforce Branch Policies & PRs<br/>Versioned per Git Release Branch"]
```

---

- **Publishing Code as Wiki (Docs-as-Code Workflow)**:
  1. Store markdown documentation directly in your application codebase under a `/docs` directory.
  2. In Azure DevOps, navigate to **Overview $\rightarrow$ Wiki**.
  3. Click the dropdown next to the wiki name $\rightarrow$ select **Publish code as wiki**.
  4. Select the **Repository**, the target **Branch** (e.g. `main`), and the **Folder** (`/docs`).
  5. Provide a Wiki name $\rightarrow$ click **Publish**.
  6. *Benefit*: Developers update documentation in the same Pull Request that modifies source code, ensuring docs never drift out of sync with code releases.

---

- **Ordering Pages via `.order` Files**:
  - In a Code Wiki, pages are ordered alphabetically by default.
  - To specify custom ordering, create a text file named `.order` inside the folder and list the file names (without `.md` extension) in desired display order:
    ```
    Project-Overview
    Architecture-and-Design
    API-Contracts
    Deployment-Guide
    ```

---

- **Advanced Markdown Features in Azure DevOps Wiki**:
  - **Work Item Referencing**: Typing `#<ID>` (e.g., `#105`) embeds a live interactive chip showing the work item title, type, and current state.
  - **Mentioning Users**: Typing `@<User>` sends an automated notification to that team member.
  - **Mermaid Diagrams**: Native rendering inside fenced code blocks:
    ````markdown
    ```mermaid
    sequenceDiagram
        Client->>AuthService: POST /oauth/token
        AuthService-->>Client: JWT Bearer Token
    ```
    ````
  - **Table of Contents Generation**: Adding `[[_TOC_]]` at the top of a page automatically builds an interactive TOC based on markdown headings.
  - **Active Work Item Query Results**: Embed dynamic query results using the query syntax:
    ```markdown
    ::: query-table <Query-GUID>
    :::
    ```

> [!TIP]
> **AZ-400 Exam Tip**:
> - If an exam scenario requires **peer review, branch policies, or versioning documentation alongside release branches (e.g. v1 vs v2 docs)**, the correct answer is always **"Publish code as wiki"** pointing to an Azure Repos Git branch.
> - To enforce custom page order in a published code wiki, use a **`.order`** file.
> - `[[_TOC_]]` generates a table of contents automatically.

### Process Diagrams for Documentation

#### 1. Slide Transcripts (As-Is)

##### Part 1: Introduction
> **Azure DevOps Engineer Expert**  
> **Collaboration and Communication**  
> **Process Diagrams for Documentation**

##### Part 2: Essential Processes, Flowcharts, BPMN & Diagramming Tools
> **Process Diagrams for Documentation**  
> *Cheat sheets, Practice Exams and Flash cards 👉 www.exampro.co/az-400*
>
> **Process diagrams are visual guides that show the steps in a process, making it easier to see how everything connects, especially in DevOps projects.**
>
> **Pinpoint Essential Processes:**  
> First, identify the main processes in your DevOps project, such as **managing source code, integrating changes continuously, testing automatically, deploying, and monitoring**.  
> Break down these processes into smaller parts.
>
> **Make Flowcharts or BPMN Diagrams:**  
> Use software like **Microsoft Visio, draw.io, or lucidchart**, to create diagrams that map out the process.  
> These diagrams should clearly show where the process starts and ends, include **decision-making points**, and outline the steps in order.
>
> *(UI Callout: Icons for Microsoft Visio, draw.io, and Lucidchart; Example Flowchart showing: Ticket/Email Submitted by Customer $\rightarrow$ Support Case Created & Assigned $\rightarrow$ Decision: During STD Business Hours? [Yes: Alerts sent to Support team to respond; No: Alerts sent to on-call Technician to respond] $\rightarrow$ Decision: Is ticket assigned? $\rightarrow$ Ticket reviewed based on priority $\rightarrow$ Decision: Was issue resolved? $\rightarrow$ Ticket closed & system sends follow-up email $\rightarrow$ End).*

##### Part 3: Inputs, Outputs & Responsibility
> **Process Diagrams for Documentation**  
> *Cheat sheets, Practice Exams and Flash cards 👉 www.exampro.co/az-400*
>
> **Detail What Goes In and Comes Out:**  
> For every step in your process, note down what you need to **start (inputs)** and what you expect to get **out of it (outputs)**.  
> This might be **code, test results, deployment packages**, or anything else relevant. It's important to show how each step is linked to the next.
>
> *(UI Callout: Example Flowchart: Email or phone call from customer $\rightarrow$ Check FAQ $\rightarrow$ Info available? [Yes: Reply according to FAQ $\rightarrow$ Answer customer; No: Contact manager $\rightarrow$ Manager provides answer $\rightarrow$ Add answer to FAQ $\rightarrow$ Reply according to FAQ]).*
>
> **Clarify Who Does What:**  
> Make sure your diagrams indicate **who is responsible for each step**.  
> This removes confusion and makes sure everyone knows their responsibilities.

---

#### 2. Visual References

![Process Diagrams Title](../images/04-process-diagrams-title.png)

![Process Diagrams Flowcharts & Tools](../images/04-process-diagrams-flowcharts-tools.png)

![Process Diagrams Inputs, Outputs & Roles](../images/04-process-diagrams-inputs-outputs-roles.png)

---

#### 3. Expert-Level Deep Dive & Practical Notes

- **Diagramming Paradigms in Enterprise DevOps**:
  - **BPMN (Business Process Model and Notation)**: Focuses on business-level flows, approvals, SLAs, and handoffs between departments.
  - **UML Activity & Sequence Diagrams**: Focuses on runtime service-to-service communication, API invocation contracts, and exception flows.
  - **Diagrams-as-Code (Mermaid / PlantUML)**: Preferred in modern DevOps repositories because diagrams live in Markdown, versioned in Git alongside source code, and reviewed via Pull Requests.

```mermaid
flowchart TD
    subgraph Inputs ["1. Inputs"]
        Code[Git Commit / PR]
        Config[App Config / Secrets]
    end

    subgraph ProcessFlow ["2. Automated CI/CD Pipeline (Process)"]
        Build[Compile & Lint]
        Test{Unit Tests & SAST Pass?}
        Package[Package Container / Artifact]
        Deploy[Deploy to Staging Slot]
        Gate{Automated Smoke Tests & Approval?}
        Prod[Swap to Production Slot]
    end

    subgraph Outputs ["3. Outputs & Responsible Roles"]
        Artifact[Drop Artifact / Container Image]
        Telemetry[Application Insights Metrics]
        Roles["Responsible: DevOps Engineers & Platform Team"]
    end

    Code --> Build
    Config --> Build
    Build --> Test
    Test -- Yes --> Package
    Test -- No --> Fail[Fail Pipeline & Alert Author]
    Package --> Deploy
    Deploy --> Gate
    Gate -- Approved --> Prod
    Gate -- Rejected --> Rollback[Abort & Revert]
    Package --> Artifact
    Prod --> Telemetry
```

- **Tooling Comparison**:
  | Tool | Type | Integration with Azure DevOps |
  | :--- | :--- | :--- |
  | **Mermaid.js** | Diagram-as-Code | Native zero-install rendering in Azure DevOps Wikis and GitHub Markdown files. |
  | **draw.io (diagrams.net)** | Visual Drag & Drop | Azure DevOps Marketplace extension allows editing `.drawio` files directly in repos. |
  | **Microsoft Visio** | Enterprise Visual Tooling | Deep Microsoft 365 / SharePoint integration; exportable as SVG/PNG for Wiki embedding. |
  | **Lucidchart** | Cloud Collaborative Canvas | Embeddable interactive canvas widgets in Azure DevOps dashboards and wikis. |

> [!TIP]
> **AZ-400 Exam Tip**: Prefer **Diagrams-as-Code (Mermaid/Markdown)** for architectural and pipeline process diagrams because they avoid binary blob merge conflicts in Git and ensure documentation evolves with the code via Pull Requests.

---

### Configure Release Documentation

#### 1. Slide Transcripts (As-Is)

##### Part 1: Introduction
> **Azure DevOps Engineer Expert**  
> **Collaboration and Communication**  
> **Configure release documentation**

##### Part 2: Key Elements of Release Documentation
> **Configure release documentation**  
> *Cheat sheets, Practice Exams and Flash cards 👉 www.exampro.co/az-400*
>
> **Release documentation is a cornerstone for the successful deployment of software releases within Azure DevOps, focusing on the non-code aspects that define the scope, quality, and functionality of the release.**
>
> **Key Elements of Release Documentation:**
> 1. **Release Notes**: These should highlight what's **new**, what **issues have been resolved**, and any **enhancements made**, as well as outline any **modifications to settings** and their effects on existing features.
> 2. **Installation Guides**: Provide clear, detailed instructions for the **setup process**, including a list of required **software and system prerequisites**, and post-installation actions.
> 3. **Configuration Changes**: Document updates to **configuration settings**, clarifying any default settings and essential changes.
> 4. **Change Log**: Keep an accurate record of **commits or work items** in the release, using a consistent tracking method.
> 5. **Rollback Plan**: Have a clear, predefined plan for **reverting to an earlier software version** if necessary.

##### Part 3: Creating Release Documentation in Azure DevOps
> **Configure release documentation**  
> *Cheat sheets, Practice Exams and Flash cards 👉 www.exampro.co/az-400*
>
> **Creating Release Documentation in Azure DevOps:**
> - **Azure Repos**:
>   - Store your **markdown or text files** alongside your code.
>   - **Version control** your documentation for consistency and traceability.
> - **Azure Pipelines**:
>   - Automate the generation of **changelogs** and other documentation during the build and release processes.
> - **Artifacts**:
>   - Attach generated documentation to specific **builds or releases as downloadable artifacts**.
> - **Wiki**:
>   - Utilize the built-in **Wiki** to share detailed guides and notes with the team and stakeholders.
>
> *(UI Callout: Code snippet of markdown release notes showing `# Release Notes - Version 2.1.0`, `## New Features`, `## Enhancements`, `## Configuration Changes`, `## Known Issues`, `## Rollback Plan`, and `For installation guidance, please refer to the [Installation Guide](link-to-guide)`).*

---

#### 2. Visual References

![Configure Release Documentation Title](../images/04-configure-release-documentation-title.png)

![Key Elements of Release Documentation](../images/04-configure-release-documentation-key-elements.png)

![Creating Release Documentation in Azure DevOps](../images/04-configure-release-documentation-azure-devops-tools.png)

---

#### 3. Expert-Level Deep Dive & Practical Notes

- **The 5 Pillars of Release Documentation**:
  ```mermaid
  graph TD
      ReleaseDoc[Release Documentation Package] --> RN[1. Release Notes: New Features, Bugfixes & Breaking Changes]
      ReleaseDoc --> IG[2. Installation & Upgrade Guides: Prerequisites & Post-deploy verification]
      ReleaseDoc --> CC[3. Configuration Changes: Env vars, Feature Flags & DB Migrations]
      ReleaseDoc --> CL[4. Changelog: Git commit SHAs & linked Azure Boards Work Items]
      ReleaseDoc --> RB[5. Rollback Plan: Deployment slot swap-back, DB restore & fallback steps]
  ```

---

- **Automating Changelog and Release Notes Generation in Azure Pipelines**:
  - In modern CI/CD, manual release note authoring causes human error and missed commits.
  - Azure Pipelines can automatically harvest work items and commits linked to a release:

  ```yaml
  # Sample Azure Pipeline stage generating and publishing Release Notes
  stages:
  - stage: BuildAndDocument
    jobs:
    - job: BuildJob
      pool:
        vmImage: 'ubuntu-latest'
      steps:
      - checkout: self
        fetchDepth: 0

      # 1. Generate release notes from Git commits & Conventional Commits
      - script: |
          echo "## Release Notes - $(Build.BuildNumber)" > $(Build.ArtifactStagingDirectory)/RELEASE_NOTES.md
          echo "Generated on: $(date)" >> $(Build.ArtifactStagingDirectory)/RELEASE_NOTES.md
          echo "" >> $(Build.ArtifactStagingDirectory)/RELEASE_NOTES.md
          echo "### Commits in this Release:" >> $(Build.ArtifactStagingDirectory)/RELEASE_NOTES.md
          git log $(git describe --tags --abbrev=0 2>/dev/null || git rev-list --max-parents=0 HEAD)..HEAD --oneline >> $(Build.ArtifactStagingDirectory)/RELEASE_NOTES.md
        displayName: 'Generate Changelog'

      # 2. Publish documentation as pipeline artifact
      - task: PublishBuildArtifacts@1
        inputs:
          PathtoPublish: '$(Build.ArtifactStagingDirectory)/RELEASE_NOTES.md'
          ArtifactName: 'release-documentation'
          publishLocation: 'Container'
  ```

- **Automated Work Item Release Annotations (Azure DevOps Native Release Notes)**:
  - In Classic & YAML Multi-Stage Pipelines, checking **"Report deployment status to Boards"** on deployment jobs automatically links the deployed release pipeline run ID and commit SHA directly to all associated work items.
  - Third-party extensions such as **XplatGenerateReleaseNotes** or **GitReleaseManager** extract all linked `AB#` work items, issues, and PR descriptions to dynamically construct markdown release notes.

> [!TIP]
> **AZ-400 Exam Tip**:
> - A comprehensive release package must contain a **Rollback Plan** and **Configuration Changes / DB Migration instructions**, not just feature descriptions.
> - Attaching documentation as a **Pipeline Build Artifact** guarantees that release notes are immutably tied to the exact compiled binaries and commit SHA that were deployed.

### API Documentation

#### 1. Slide Transcripts (As-Is)

##### Part 1: Introduction
> **Azure DevOps Engineer Expert**  
> **Collaboration and Communication**  
> **API documentation**

##### Part 2: Steps to Generate API Documentation
> **API documentation**  
> *Cheat sheets, Practice Exams and Flash cards 👉 www.exampro.co/az-400*
>
> **Steps to Generate API Documentation:**
> - **Generate Documentation:**
>   - Utilize **Visual Studio** to generate **API documentation**. Access this feature via the **Build** menu.
>   - Use tools like **Swagger, Azure API Management, or OpenAPI** for automatic documentation generation from your codebase.
> - **Documenting Endpoints:**
>   - Clearly define and describe each **API endpoint**, detailing the purpose and functionality.
>   - Include information on request and response formats, as well as any **authentication** requirements.
> - **Selecting Formats and Styles:**
>   - Decide on your **output** format and style, ensuring it's readable and accessible for your target audience.
> - **Integration and Automation:**
>   - Integrate documentation generation into your **continuous integration and deployment pipelines** within Azure DevOps.
>
> *(UI Callout: Sample API Documentation in Markdown/JSON for Version 1.2.3: POST /api/login endpoint with request body username/password and 200 OK response with JWT token; GET /api/users endpoint retrieving list of users).*

##### Part 3: Best Practices for API Documentation
> **API documentation**  
> *Cheat sheets, Practice Exams and Flash cards 👉 www.exampro.co/az-400*
>
> **Best Practices for API Documentation:**
> - **Consistency:** Use a consistent format for all **API endpoints** to make the documentation easy to follow.
> - **Clarity:** Ensure that descriptions are clear and concise, avoiding ambiguity.
> - **Version Control:** Manage your API documentation within **Azure Repos** for versioning and historical tracking.
> - **Regular Updates:** Keep the documentation current with every release, deprecating outdated information promptly.
> - **Feedback Mechanisms:** Include a process for developers and users to provide **feedback** on the documentation for continuous improvement.
>
> *By focusing on these elements, your API documentation will be an invaluable resource for your team and stakeholders, supporting the effective use and integration of your software's API.*

---

#### 2. Visual References

![API Documentation Title](../images/04-api-documentation-title.png)

![API Documentation Generation Steps](../images/04-api-documentation-generation-steps.png)

![API Documentation Best Practices](../images/04-api-documentation-best-practices.png)

---

#### 3. Expert-Level Deep Dive & Practical Notes

- **The OpenAPI (Swagger) Specification Standard**:
  - In modern RESTful systems, API documentation is generated directly from code annotations/attributes (**Code-First**) or drafted before coding (**API-First / Contract-First**).
  - Framework integrations:
    - **ASP.NET Core**: `Swashbuckle.AspNetCore` or `NSwag` extracts XML doc comments and controller attributes (`[ProducesResponseType]`, `[HttpPost]`) to generate a runtime `swagger.json`.
    - **Node.js/Express**: `tsoa` or `swagger-jsdoc` with JSDoc annotations.
    - **FastAPI / Python**: Auto-generates interactive Swagger UI (`/docs`) and ReDoc (`/redoc`) at runtime via Pydantic models.

```mermaid
flowchart LR
    Code["API Source Code<br/>(C# / Node.js / Python)"] --> Build["CI Pipeline Build<br/>(az pipelines)"]
    Build --> GenSpec["Generate openapi.json<br/>(Swashbuckle / CLI)"]
    GenSpec --> APIM["Deploy to Azure API Management<br/>(Developer Portal)"]
    GenSpec --> StaticDocs["Static HTML/Markdown Docs<br/>(Redoc / Swagger UI / Wiki)"]
    StaticDocs --> Devs["Internal & External Consumers"]
```

---

- **Automated API Documentation in Azure Pipelines**:
  - To prevent documentation drift, generating OpenAPI definitions must be part of CI validation:

  ```yaml
  # Sample CI Pipeline task generating OpenAPI spec during build
  - stage: BuildAndDoc
    jobs:
    - job: GenerateAPIDocs
      steps:
      - task: DotNetCoreCLI@2
        displayName: 'Build Solution'
        inputs:
          command: 'build'
          projects: '**/*.csproj'
          arguments: '--configuration Release'

      # Generate OpenAPI specification file using dotnet swagger CLI
      - script: |
          dotnet tool install --global Swashbuckle.AspNetCore.Cli
          swagger tofile --output $(Build.ArtifactStagingDirectory)/swagger.json $(Build.BinariesDirectory)/MyApi.dll v1
        displayName: 'Extract OpenAPI Specification'

      # Publish generated OpenAPI spec as build artifact
      - task: PublishBuildArtifacts@1
        inputs:
          PathtoPublish: '$(Build.ArtifactStagingDirectory)/swagger.json'
          ArtifactName: 'api-specification'
  ```

---

- **Azure API Management (APIM) Developer Portal (AZ-400 Architecture)**:
  - Enterprise systems publish APIs to **Azure API Management**.
  - **Features**:
    - **Automated Ingestion**: APIM can automatically import OpenAPI/Swagger specifications via CI/CD pipelines (`az apim api import`).
    - **Developer Portal**: Provides a customizable, self-service web portal where developers can read API reference docs, obtain API subscription keys, and test live calls directly in the browser via an interactive console.
    - **Versioning & Revisions**: Manages non-breaking revisions and breaking versions (`v1`, `v2`) with deprecation alerts.

> [!TIP]
> **AZ-400 Exam Tip**:
> - Always automate API specification extraction within the **CI Build Pipeline** to avoid "doc drift".
> - When asked how to provide a secure, interactive documentation catalog with subscription key management and rate-limiting policies for external or partner developers, select **Azure API Management (APIM) Developer Portal**.

### Automate Git History Documentation
*Awaiting slide content / screenshot...*

### What are Webhooks
*Awaiting slide content / screenshot...*

### Configure Notifications with Webhooks
*Awaiting slide content / screenshot...*
