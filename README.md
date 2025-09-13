
# 🌱 Zettelkasten Notes — CSE & Beyond

I really like taking notes, so this repository is my experiment in applying the **Zettelkasten** method to my studies and projects.  
Goal: capture ideas, **connect** them, and grow them into durable knowledge.

---

## 🔎 What this repo is
A Markdown-first, plain-text knowledge garden. It’s organized to make it easy to:
- **Capture** quick thoughts and references
- **Distill** them into permanent, atomic notes
- **Link** related ideas so new insights emerge over time

Any Markdown editor works. No lock-in, just text files.

---

## 🗂️ Structure (folders)
```

/1 - Rough Notes/          # Fleeting notes & quick captures (to be processed)
/2 - Source Material/     # Reading notes: papers, books, articles
/3 - Tags/      # Common themes among groups of notes
/4 - Indexed/       # Tags that have been totally explored
So on...

````

> Tip: Don’t over-engineer the structure. The links between notes matter most.

---

## 🧩 Note types
- **Fleeting**: quick, messy capture. One idea per note if possible.
- **Literature**: what source X actually says, with citation.
- **Permanent**: your own distilled idea in your own words; small, self-contained.
- **MOC (Map of Content)**: an index/hub that curates links for a topic (e.g., `Algorithms`, `Databases`).

---

## 🔖 Conventions
**File name / ID**
- `YYYY-MM-DD-hhmm-descriptive-slug.md`  
  Example: `2025-09-13-1710-union-vs-join-relational-algebra.md`

**Frontmatter (YAML)**
```yaml
---
id: 2025-09-13-1710
title: Union vs Join in Relational Algebra
created: 2025-09-13 17:10
updated:
tags: [cs, databases, relational-algebra]
links:
  - [[2025-09-10-1400-basic-set-operations]]
  - [[2025-09-11-0930-inner-vs-outer-joins]]
source:
  - title: Course notes DB-101
    url:
summary: One-paragraph gist of the idea in your own words.
---
````

**Linking**

* Prefer **explicit links** between notes (the lifeblood of Zettelkasten).
* Add a `See also` section at the bottom with related links.
* Create MOCs when a topic starts to sprawl.

**One idea per note**

* Keep permanent notes small and focused. Split if a note grows too wide.

---

## 🛠️ Workflow (simple)

1. **Capture** in `/0-inbox/` (fleeting note).
2. **Process**: turn good captures into **Literature** (if from a source) or **Permanent** notes (in your words).
3. **Link** each new permanent note to 2–3 related notes.
4. **Curate**: when a cluster emerges, create/update a **MOC** in `/_mocs/`.

> Bias for execution: link first, tidy later.

---

## ✍️ Templates

**Permanent Note**

```markdown
---
id: {{date:YYYY-MM-DD-hhmm}}
title: {{title}}
created: {{date:YYYY-MM-DD}} {{time:HH:mm}}
updated:
tags: []
links: []
summary:
---
# {{title}}

**Claim / Idea:** …

**Why it matters:** …

**Details:** …

**See also:**  
- [[<related-note-id-1>]]  
- [[<related-note-id-2>]]
```

**Literature Note**

```markdown
---
id: {{date:YYYY-MM-DD-hhmm}}
title: {{source-title}} — Notes
created: {{date:YYYY-MM-DD}} {{time:HH:mm}}
tags: [literature]
source:
  - title: {{source-title}}
    author: {{author}}
    year: {{year}}
    url: {{url}}
---
# {{source-title}} — Notes

**Key points (verbatim or close):**  
- …

**My takeaways (own words):**  
- …

**Links / relates to:**  
- [[<permanent-note-id>]]
```

**MOC (Map of Content)**

```markdown
---
title: {{Topic}} — MOC
tags: [moc]
---
# {{Topic}} — Map of Content

## Core ideas
- [[…]]

## Techniques / Examples
- [[…]]

## References
- [[…]]
```

---

## 🧪 Focus areas (current semester)

Likely tags & hubs I’ll be building out:

* `algorithms`, `data-structures`, `complexity`, `graphs`
* `databases`, `sql`, `relational-algebra`
* `systems`, `os`, `networks`
* `math`, `discrete-math`, `probability`, `linear-algebra`

---

## 🔄 Optional: autosave commits

If you want a steady trail of progress, you can set up a small script or CI to commit daily.

**Local script (example)**

```bash
#!/usr/bin/env bash
set -euo pipefail
cd "$(dirname "$0")"
git add -A
msg="chore(notes): auto-commit $(date -u +'%Y-%m-%d %H:%M:%S UTC')"
git commit -m "$msg" || echo "Nothing to commit."
git push
```

**GitHub Actions (daily at 23:55 UTC)**

```yaml
name: daily-commit
on:
  schedule:
    - cron: "55 23 * * *"
  workflow_dispatch:
jobs:
  commit:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          persist-credentials: true
      - name: Commit changes
        run: |
          git config user.name "auto-commit"
          git config user.email "actions@users.noreply.github.com"
          git add -A
          git commit -m "chore(notes): daily sync" || echo "Nothing to commit."
          git push
```

---

## 📌 Principles

* **Small notes, strong links.**
* **Write in your own words.**
* **Connect before you collect more.**
* **Return to improve; don’t chase perfection on day one.**

---

## 📜 License & contributions

These are personal notes. Feel free to read, learn, and open issues.
PRs are closed unless explicitly invited.

```

If you want, tell me your exact folder names or any preferences (emoji level, colors in headings, templates you already use), and I’ll tailor this to match your repo 1:1.
```
