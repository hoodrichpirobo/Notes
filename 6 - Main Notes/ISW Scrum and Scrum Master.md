2025-09-22 09:59

Status: #adult #reseach

Tags: [[Scrum]], [[Launchpad]]

# ISW Scrum and Scrum Master

# Scrum Agile Methodology: Basics and Scrum Master Role

> [!tldr] TL;DR
> **Scrum = Agile in action**: short, fixed-length **sprints**; clear **roles** (PO, Dev Team, **Scrum Master**); lightweight **artifacts** (Product/Sprint Backlog, **Increment**); recurring **events** (Planning, **Daily**, Review, Retro). You can learn the rules fast; mastery comes with practice.

---

## 1) Scrum Overview
Scrum is an Agile framework to deliver value iteratively by slicing work into small increments and adapting as you learn. Agile is the mindset; **Scrum is one concrete way to implement it** [Atlassian – Beginner’s Guide]. Created in the 1990s (Sutherland, Schwaber), it’s popular beyond software. **No certification needed** to start; the rules are simple, expertise takes time (the classic “poker” analogy) [Atlassian – Beginner’s Guide].

---

## 2) Roles (Who does what?)
- **Product Owner (PO)** → Owns **Product Backlog**, prioritizes for **value**, decides *what* to build next [Atlassian – Beginner’s Guide].
- **Development Team** → Cross-functional, self-organizing builders; decides *how* to deliver; small team (~3–9).
- **Scrum Master** → **Servant-leader** and coach of the process; facilitates events, removes impediments, protects focus, promotes continuous improvement [Atlassian – Beginner’s Guide; Atlassian – Scrum Master].

> [!tip] Mental model
> PO = *maximize value*, Dev Team = *build well*, Scrum Master = *make Scrum work smoothly*.

---

## 3) Artifacts (Lightweight tracking)

| Artifact | Purpose | Owner | Notes |
|---|---|---|---|
| **Product Backlog** | Ordered list of all desired work | **PO** | Dynamic; most valuable on top (e.g., “engine” before “paint”) [Atlassian – Beginner’s Guide]. |
| **Sprint Backlog** | Selected items + plan for current sprint | **Dev Team** | Fixed during sprint; visible task board; capacity-based selection [Atlassian – Ceremonies]. |
| **Increment** | Potentially shippable result of the sprint | Team | Meets “Definition of Done”; **100% done** by sprint end [Axosoft – Learn Scrum]. |

> Other helpers: **Burndown chart**, **Definition of Done** checklist [Axosoft – Learn Scrum].

---

## 4) Events (The sprint loop)

1. **Sprint Planning** – Decide **what** fits and **how** to do it; set a clear **Sprint Goal**. Time-box ≈ *2h per sprint week* [Atlassian – Ceremonies].  
2. **Daily Scrum (Stand-up)** – ~15 min: *Yesterday, Today, Blockers*. Team sync; not a manager status report [Atlassian – Ceremonies; Ayoka – Video Note].  
3. **Sprint Review** – Demo the **Increment**; inspect and get stakeholder feedback; update Product Backlog [Atlassian – Ceremonies].  
4. **Sprint Retrospective** – Team reflects on **process**, picks 1–3 concrete improvements for next sprint [Atlassian – Ceremonies].

> [!example] Daily stand-up prompts
> - What did I finish yesterday?  
> - What will I do today?  
> - What’s blocking me (and who can help)?

---

## 5) Scrum Values
**Commitment, Focus, Openness, Respect, Courage** → enable trust, transparency, and improvement. The Scrum Master models and nurtures these.

---

## 6) Scrum Master — Role & Responsibilities
- **Process Facilitator**: Ensure events happen, are time-boxed, and valuable; coach on estimation & sustainable pace [Atlassian – Scrum Master].  
- **Coach / Servant-Leader**: Teach Agile principles; enable self-organization; foster psychological safety and experimentation [Atlassian – Scrum Master].  
- **Impediment Remover**: Surface & clear blockers (enlist others as needed); shield from outside noise; improve flow [Atlassian – Scrum Master].  
- **Team Support & Ops**: Keep boards/tools tidy; visualize metrics (velocity, burndown) for insight, not control [Atlassian – Scrum Master].  
- **Org Liaison**: Educate stakeholders on engaging via PO and respecting sprint focus; advocate agile ways of working [Atlassian – Scrum Master].

> [!check] “Definition of Done” (starter checklist)
> - [ ] Coded & peer-reviewed  
> - [ ] Tested (unit/integration as appropriate)  
> - [ ] Integrated & passes CI  
> - [ ] Docs/notes updated  
> - [ ] Demo-ready

---

## 7) Quick Start (15-minute setup for a student team)
- **Create a Product Backlog**: 8–15 user stories, roughly ordered by value.  
- **Pick a sprint length**: Start with **2 weeks**; keep it consistent.  
- **Sprint Planning**: Select only what fits your capacity; write a **Sprint Goal** sentence.  
- **Daily**: 15-minute stand-up at a fixed time/place.  
- **End**: Demo to a friend/mentor (Review) + 20-minute Retro; choose 1 process improvement for next sprint.  
- **Track**: Simple board (To Do / In Progress / Done) and a one-line DoD like above.

---

## 8) Visual — Scrum cycle (Mermaid)
```mermaid
flowchart LR
  A[Product Backlog] --> B(Sprint Planning)
  B --> C[Sprint Backlog]
  C --> D(Development Work)
  D --> E[Daily Scrum]
  D --> F[Increment]
  F --> G[Sprint Review]
  G --> H[Sprint Retrospective]
  H --> B
````

---

## 9) Best 15-min Resources

* **Official *Scrum Guide*** (primary source, \~13 pages) — free PDF [Scrum Guide].
* **“Scrum in Under 10 Minutes”** (short animated explainer) — great primer [Axosoft – Learn Scrum].
* **Atlassian Agile Coach** (clear intros to roles & ceremonies) \[Atlassian – Beginner’s Guide; Atlassian – Ceremonies; Atlassian – Scrum Master].

---

## References (keep these links handy)

[Atlassian – Beginner’s Guide]: https://www.atlassian.com/blog/project-management/beginners-guide-scrum-and-agile-project-management
[Atlassian – Ceremonies]: https://www.atlassian.com/agile/scrum/ceremonies
[Atlassian – Scrum Master]: https://www.atlassian.com/agile/scrum/scrum-master
[Axosoft – Learn Scrum]: https://www.axosoft.com/scrum
[Ayoka – Video Note]: https://ayokasystems.com/opinion/scrum-in-under-10-minutes/
[Scrum Guide]: https://scrumguides.org/

## References

[[ISW Concepts]], [[ISW Lab Case]], [[ISW C1. Introduction to Software Engineering]]