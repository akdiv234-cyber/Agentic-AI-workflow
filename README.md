# Azure DevOps Multi-Agent Workflow (Planner & Analyser)

An automated, event-driven multi-agent orchestration pipeline built with **n8n** that integrates with **Azure DevOps (ADO)**. The system ingests incoming work items or pull requests, delegates work breakdown to a **Planner Agent**, and uses an **Analyser Agent** to evaluate structural dependencies before updating the ADO backlog.

---

## 🏗 System Architecture

```text
               +-----------------------+
               |  Azure DevOps (ADO)   |
               |  (Webhook / Work Item)|
               +-----------+-----------+
                           |
                           v
               +-----------------------+
               |    n8n Orchestration  |
               |       Pipeline        |
               +-----------+-----------+
                           |
            +--------------+--------------+
            |                             |
            v                             v
  +------------------+          +-------------------+
  |  Planner Agent   |          |  Analyser Agent   |
  |  (Task Breakdown |          |  (Dependency &    |
  |   & Sub-tasks)   |          |   Impact Graph)   |
  +--------+---------+          +---------+---------+
           |                              |
           +--------------+---------------+
                          |
                          v
               +-----------------------+
               |  ADO Backlog Update   |
               |  (Comments / Tasks)   |
               +-----------------------+
