2025-09-22 09:56

Status: #adult

Tags: [[Digitalización 2.0 Fabrica Jairo]], [[BDA]], [[ISW]]

# ISW Lab Case

The main information that needs to be known about an incident is: incident number, employee who reported it, ~~hospital service~~ where it took place, creation date, description, priority and cost of the repairment parts used.


# Universal System Development Manual (Beginner-Friendly)

> Build **one reusable system** that works for *any* organization: shops, clinics, factories, schools, a textile plant—without naming any specific industry.

---

## 0) From Specific Case → General System

Use neutral words so the design fits everywhere:

| Specific term                 | General, reusable term                             |
| ----------------------------- | -------------------------------------------------- |
| Incident                      | **Request** (problem, task, ticket, order)         |
| Area/Department               | **Functional Unit** (team, cell, line)             |
| Work order                    | **Job** (assignment to do work)                    |
| Parts                         | **Resources** (materials, tools, assets, services) |
| Service head                  | **Coordinator** (triage/priority owner)            |
| Area master                   | **Team Lead** (assigns and supervises)             |
| Operator                      | **Agent** (does the work)                          |
| External provider             | **Vendor**                                         |
| Requester (employee/customer) | **Requester**                                      |

---

## 1) Goal & Scope (keep it small first)

**Goal:** Track every **request** from creation → triage → assignment → execution → completion, with optional **resources**, **costs**, and **reports**.

**MVP scope (first version):**

1. Create a request.
2. Triage (set priority + functional unit).
3. Assign to a job (one or more agents, one shift/time window).
4. Mark resources used (optional).
5. Complete the job (result, date, notes).
6. Basic lists and filters by status.
7. Simple role-based access.

> If you’re brand-new: you can prototype all of this in a spreadsheet first (one tab per table below), then move to a database/app.

---

## 2) Core Concepts (what the system manages)

* **Requester:** Person who opens a request.
* **Request:** What needs doing (title, description, priority, status, unit).
* **Functional Unit:** Where it belongs (team/line/department).
* **Job:** Concrete assignment to agents to fulfill a request.
* **Agent:** Person who executes jobs; may have **shift** or availability.
* **Resource:** Anything consumed or used (stocked item, tool, outside service).
* **Vendor:** External supplier of resources/services.
* **User & Role:** Who can do what (Coordinator, Team Lead, Agent, Requester, Admin).

---

## 3) Lifecycle (status model you can reuse)

**Request.Status:**
`created → triaged → assigned → in_progress → pending_resources → completed | rejected`

Rules:

* Only Coordinators can **triage** (set priority + functional unit).
* Team Leads create **jobs** and assign **agents**.
* If resources are missing, move job to **pending\_resources** until available.
* Once done, **completed** with outcome notes & timestamps.
* If invalid, **rejected** with reason.
* **No deletion** of requests until completed or rejected (audit trail).

**Job.Status:**
`open → in_progress → blocked (waiting_resources) → done`

---

## 4) Roles & Permissions (starter matrix)

| Action                         | Requester | Agent | Team Lead | Coordinator | Admin |
| ------------------------------ | :-------: | :---: | :-------: | :---------: | :---: |
| Create Request                 |     ✅     |   ✅   |     ✅     |      ✅      |   ✅   |
| Triage Request (priority/unit) |     ❌     |   ❌   |     ❌     |      ✅      |   ✅   |
| Create Job / Assign Agents     |     ❌     |   ❌   |     ✅     |      ✅      |   ✅   |
| Update Job Progress            |     ❌     |   ✅   |     ✅     |      ✅      |   ✅   |
| Manage Resources/Stock         |     ❌     |  ✅\*  |     ✅     |      ✅      |   ✅   |
| Close/Complete Job             |     ❌     |   ✅   |     ✅     |      ✅      |   ✅   |
| Reject Request                 |     ❌     |   ❌   |     ❌     |      ✅      |   ✅   |
| User Management                |     ❌     |   ❌   |     ❌     |      ❌      |   ✅   |

\* Let agents record what they actually used.

---

## 5) Data Model (tables you can start with)

**Users**(id, login, password\_hash, first\_name, last\_name, role, phone, city, region, postal\_code)
**FunctionalUnits**(id, name, description)
**Agents**(user\_id, unit\_id, shift ENUM\[morning, afternoon, night])
**Requests**(id, created\_at, requester\_user\_id, title, description, priority ENUM\[high, medium, low], unit\_id, status ENUM\[created, triaged, assigned, in\_progress, pending\_resources, completed, rejected], rejection\_reason, cost\_total)
**Jobs**(id, request\_id, start\_at, end\_at, status ENUM\[open,in\_progress,blocked,done], lead\_user\_id, outcome\_notes, cause\_notes)
**JobAssignments**(job\_id, agent\_user\_id)
**Resources**(id, code, description, unit\_of\_measure, vendor\_id, unit\_price, qty\_on\_hand, min\_qty)
**JobResourceUses**(job\_id, resource\_id, quantity\_used)
**Vendors**(id, name, contact\_phone, contact\_email, notes)
**StockMovements**(id, resource\_id, delta\_qty, reason, created\_at, reference)

**Key constraints (beginner-safe rules):**

* A Request can’t be **deleted** unless `status in (completed, rejected)`.
* Triage can only be done by roles `Coordinator/Admin`.
* A Job must link to exactly **one** Request.
* All Agents in a Job should share a compatible shift (validate in code).
* When a Job uses resources, **decrease stock**; if stock < requested, set Job to `blocked` and mark shortage.

---

## 6) Workflows (what the app should let users do)

### A) Intake & Triage

1. **Create Request:** requester fills title, description (auto-id, timestamp).
2. **Coordinator triages:** sets priority + functional unit → status becomes `triaged`.

### B) Assignment

3. **Team Lead sees triaged list** for their unit, creates **Job**, picks agents (all same shift or compatible schedule) → Request becomes `assigned`, Job `open`.

### C) Execution & Resources

4. Agents start → Job `in_progress`.
5. Agents mark **resources needed**:

   * If available: reserve & decrement stock; continue.
   * If not: Job `blocked`; system records shortages (for purchasing).

### D) Completion

6. Do the work, record **outcome** and **cause**; set Job `done`.
7. System rolls up **cost\_total** to the Request; Request `completed`.

### E) Purchasing Loop (optional module)

* Coordinators/Leads review **shortages**, place orders with **Vendors**, increase stock via **StockMovements**, then unblock Jobs.

---

## 7) Screens/Pages (minimum set)

* **Login**
* **Create Request**
* **Requests List** (filters by status, priority, unit)
* **Triage View** (only for Coordinators)
* **Unit Queue** (Team Lead view)
* **Job Detail** (assignments, time, resources, notes)
* **Resources/Inventory** (CRUD, min qty alerts, stock movements)
* **Vendors** (basic contact list)
* **Reports/Dashboard** (see §10)

---

## 8) Validation & Business Rules (starter set)

* **Priority must be set** during triage; **Unit** must be set before assignment.
* **Reject** requires a **rejection\_reason**.
* **No extra resources** can be added **after** a Request is `completed`.
* **Returns**: allow agents to reduce `quantity_used` before completion (puts stock back).
* **Stock alert**: if `qty_on_hand < min_qty`, show alert and list in “Replenish” report.

---

## 9) Security & Audit (keep it simple, but real)

* Store **password hashes** (never plain text).
* **Role-based access control** as per matrix.
* **Audit fields:** `created_at`, `created_by`, `updated_at`, `updated_by` on all core tables.
* Prevent destructive actions without eligibility (e.g., can’t delete active Requests/Jobs).

---

## 10) Metrics & Reports (what leaders care about)

* **Throughput:** Requests completed per week.
* **SLA:** Avg time from creation → triage, triage → assignment, assignment → completion.
* **Backlog by Status/Unit/Priority.**
* **Resource usage & cost** by Unit, by Request, by time period.
* **Stock below minimum** (action list).
* **Top recurring request types/causes** (prevention focus).

---

## 11) Beginner-Friendly Implementation Path

**Phase 0 (Spreadsheet Prototype, Day 1–2)**

* Create tabs for tables in §5.
* Use data validation for enums.
* Create a simple dashboard (COUNTIFs, pivot tables).

**Phase 1 (MVP App, Week 1)**

* Pick any stack you know (even no-code/low-code is fine).
* Build: Login → Create Request → Triage → Unit Queue → Create Job → Job Detail (resources, notes) → Complete.
* Add list filters and basic role checks.

**Phase 2 (Week 2)**

* Add Inventory: resources, stock movements, min stock alerts.
* Add “blocked by resources” logic and a simple **Shortages** report.
* Add baseline **metrics**.

**Phase 3 (Week 3+)**

* Vendors & purchasing flow.
* Email/notification for status changes.
* Exports (CSV) and simple access logs.

---

## 12) Example API (optional, if you build REST)

```
POST   /requests
GET    /requests?status=triaged&unit=...
PATCH  /requests/{id}/triage           (role: Coordinator/Admin)
POST   /jobs                           (body: request_id, agent_ids[], start_at)
PATCH  /jobs/{id}/start
POST   /jobs/{id}/resources            (resource_id, qty)
PATCH  /jobs/{id}/block                (reason)
PATCH  /jobs/{id}/complete             (outcome_notes, cause_notes)
GET    /resources/shortages
POST   /stock-movements                (resource_id, delta_qty, reason)
```

---

## 13) Common Pitfalls (and fixes)

* **Too many statuses:** Keep to the lifecycle above; add later if truly needed.
* **Hidden rules in people’s heads:** Write them as validation messages/tooltips.
* **No audit trail:** Add `created_by/updated_by` now; you’ll thank yourself later.
* **Inventory chaos:** Treat every change as a **StockMovement**; never edit `qty_on_hand` directly.

---

## 14) Glossary (neutral terms)

* **Request:** The thing that needs doing.
* **Triage:** Setting priority and routing to the right functional unit.
* **Job:** Concrete assignment to execute a Request.
* **Agent:** The person doing the Job.
* **Resource:** Anything used or consumed.
* **Vendor:** Who supplies external resources/services.

**This universal request→job system is a concrete, end-to-end anchor for a Databases & Information Systems course.** The relational basics map to tables and keys for users, functional units, requests, jobs, assignments, resources, vendors and stock movements. Interpreting a database becomes writing SQL to answer operational questions (backlog, cycle times, shortages, costs). SQL DML drives the lifecycle (create, triage, assign, complete), while SQL DDL defines schemas and constraints that enforce statuses, priorities and foreign keys.

DBMS topics appear naturally: ANSI/SPARC is visible as role-specific external views, a conceptual ER model, and an internal physical layer. Transactions keep multi-step updates (finish a job, consume resources, roll up costs) atomic; integrity comes from PK/FK/CHECK rules; concurrency is handled with isolation levels or row locks when reserving scarce resources; recovery relies on backups/WAL; security maps app roles to DB roles and, if needed, row-level security.

In design, you move from conceptual ER modeling to a normalized logical schema. Practice 1 can deliver DDL, seed data and core DML/queries; Practice 2 can deliver the full case: ER → schema → sample data → representative reports → a transaction script for shortages and role-based views.

## References
[[ISW Concepts]], [[ISW C1. Introduction to Software Engineering]], [[ISW Scrum and Scrum Master]], [[BDA Concepts.]], [[BDA 1.1. Relational Databases.]]