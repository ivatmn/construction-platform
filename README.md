# construction-platform

**Enterprise construction management platform with AI agents, MCP interface, and RAG-based document search.**

Built for real construction workflows: WBS hierarchy, CBS (Cost Breakdown Structure) with BOQ line items, MDR documents, and Gantt scheduling — not a generic CRUD.

---

## What's inside

### 🔐 Auth & RBAC
- Cookie-based authentication (JWT in `access_token`, HttpOnly)
- Roles: `admin`, `owner`, `user`, `contractor`
- Access groups by level: `region`, `program`, `mega_project`, `project`
- API keys for MCP agents + call audit (`user_api_key_logs`)
- Account lockout after failed logins, Telegram OTP binding

### 📁 Project management
- Project hierarchy: `Project → WBS → Operation`
- Dictionaries: regions, statuses, phases, units of measure
- Project files: upload (50MB, type whitelist), folders, tags, move/rename/delete
- Soft delete, SHA-256 checksums

### 🏗️ Project phases
- **Core & Shell** — foundation, structure, envelope
- **Fit-out** — interior finishing, MEP, low-voltage
- **Commissioning (PNR)** — testing, start-up, acceptance
- **Handover** — as-built documentation, final acceptance

### 📅 Gantt scheduling
- Baseline vs Current (plan/fact)
- Milestones with deviation tracking
- Report generation: Gantt → PPTX, Excel
- Data export for visualization

### 🧮 CBS & BOQ
- **Cost Breakdown Structure (CBS)** with 3 levels: `level 3 → level 4 → level 5 (unit rates)`
- CBS linked to disciplines (`discipline_l1`, `discipline_l2`)
- **BOQ (Bill of Quantities)** management: create, version, link to operations and CBS, export to Excel
- BOQ line items derived from CBS and WBS
- **Resource catalog with regional pricing** (analogous to RSMeans/BCIS data model): resource → unit rate → BOQ line item

### 📄 MDR & documents
- MDR documents: WBS, codes, weights, BIM status, progress
- Document steps (plan/fact/forecast)
- Companies and roles in a document (curator, chief engineer, BIM manager)
- MDR export to Excel

### 🔍 Commissioning & Construction Supervision
- **Commissioning (PNR)**: separate work type with own BOQ, CBS, and schedules
- **Construction supervision**: inspections, QA/QC checklists, acceptance acts
- Link to MDR documents and project files

### 🤖 AI & MCP
- MCP server for LLM agents: `whoami` → domain navigation
- Role-based tool registry (projects, tasks, CBS, BOQ, resource catalog, documents)
- Prompt versioning (draft → publish → versions)
- Agent chats, message history, `tool_calls`
- RAG: `document_chunks` + `pgvector` (HNSW, cosine) for instruction search

### 🔄 Background processes
- `sync_gantt`, `sync_mdr` — async tasks with status polling
- Progress, cancellation, result

---

## Architecture
TODO
