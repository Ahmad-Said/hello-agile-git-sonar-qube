# Practical Project Example: Building "TaskFlow"

To make Agile concrete, let's follow a small team building **TaskFlow**, a
simple team to-do / task-management web app. We'll watch it grow across **five
2-week sprints** (10 weeks total).

## The team

| Person | Role |
|--------|------|
| Maya | Product Owner |
| Sam | Scrum Master |
| Priya, Leo, Dan | Developers (full-stack) |

**Sprint length:** 2 weeks · **Team velocity (after warm-up):** ~24 points/sprint

## Step 1 — The Product Vision

> *For busy teams who lose track of work, TaskFlow is a web app that keeps
> tasks, owners, and due dates in one shared board — so nothing slips through
> the cracks.*

## Step 2 — The initial Product Backlog (epics → stories)

```mermaid
flowchart TD
    V[Vision: shared task board] --> E1[Epic: Accounts]
    V --> E2[Epic: Tasks]
    V --> E3[Epic: Collaboration]
    V --> E4[Epic: Notifications]

    E1 --> S1[Sign up / log in]
    E1 --> S2[Reset password]
    E2 --> S3[Create a task]
    E2 --> S4[Edit / delete a task]
    E2 --> S5[Mark task complete]
    E3 --> S6[Assign a task to a teammate]
    E3 --> S7[Comment on a task]
    E4 --> S8[Email when assigned]
    E4 --> S9[Daily digest]
```

## Step 3 — The release roadmap

```mermaid
timeline
    title TaskFlow 10-Week Roadmap
    Sprint 1 (Wk 1-2)  : Walking skeleton : Auth + create task
    Sprint 2 (Wk 3-4)  : Core CRUD : Edit, delete, complete tasks
    Sprint 3 (Wk 5-6)  : Collaboration : Assign + comments
    Sprint 4 (Wk 7-8)  : Notifications : Email on assign + digest
    Sprint 5 (Wk 9-10) : Polish + v1.0 : Bug fixes, perf, launch
```

---

## Sprint 1 (Weeks 1–2) — The "Walking Skeleton"

**Sprint Goal:** *A user can sign up, log in, and create a single task that
persists.*

The first sprint deliberately delivers a thin, end-to-end slice — auth + one
task — so the whole architecture is proven early rather than at the end.

| Story | Points | Outcome |
|-------|--------|---------|
| Sign up / log in | 8 | ✅ Done |
| Create a task | 5 | ✅ Done |
| Project scaffolding & CI | 5 | ✅ Done |
| Reset password | 5 | ⛔ Pulled — ran out of time |

**What week 1 looked like:** scaffolding, database schema, CI pipeline, auth API.
**What week 2 looked like:** login UI, "create task" form, wiring it together,
demo prep.

**Review:** Maya demos signing up and adding a task. Stakeholders love it but
ask that tasks show a due date — added to the backlog.

**Retro action item:** "We underestimated auth. Let's split big stories before
planning." → leads to better refinement next time.

---

## Sprint 2 (Weeks 3–4) — Core Task Management

**Sprint Goal:** *A user can fully manage their own tasks (edit, delete,
complete, set due dates).*

```mermaid
stateDiagram-v2
    [*] --> Open: Task created
    Open --> InProgress: User starts work
    InProgress --> Done: Mark complete
    Open --> Done: Quick complete
    Done --> Open: Reopen
    Open --> [*]: Delete
    InProgress --> [*]: Delete
```

| Story | Points | Outcome |
|-------|--------|---------|
| Edit / delete a task | 5 | ✅ Done |
| Mark task complete | 3 | ✅ Done |
| Add due dates | 5 | ✅ Done |
| Reset password (carried over) | 5 | ✅ Done |
| Task list filtering | 8 | ⛔ Carried to Sprint 3 |

**Velocity emerging:** ~24 points completed → the team now plans around that.

---

## Sprint 3 (Weeks 5–6) — Collaboration

**Sprint Goal:** *Teammates can be assigned tasks and discuss them via comments.*

This sprint a **mid-sprint scope change** arrives: a key customer asks for
@mentions in comments. Instead of jamming it in, Maya adds it to the backlog and
the team agrees to consider it for Sprint 4 — protecting the Sprint Goal.

| Story | Points | Outcome |
|-------|--------|---------|
| Assign a task to a teammate | 5 | ✅ Done |
| Comment on a task | 8 | ✅ Done |
| Task list filtering (carried) | 8 | ✅ Done |
| @mentions in comments | 5 | 🔜 Moved to backlog |

---

## Sprint 4 (Weeks 7–8) — Notifications

**Sprint Goal:** *Users are notified by email when assigned a task, and can opt
into a daily digest.*

```mermaid
sequenceDiagram
    actor User
    participant App as TaskFlow
    participant Q as Job Queue
    participant Mail as Email Service

    User->>App: Assign task to teammate
    App->>Q: Enqueue "assignment" notification
    Q->>Mail: Send email
    Mail-->>User: "You've been assigned a task"
    Note over Q,Mail: Daily at 8am, digest job runs
    Q->>Mail: Send digest of open tasks
```

| Story | Points | Outcome |
|-------|--------|---------|
| Email when assigned | 8 | ✅ Done |
| Daily digest | 8 | ✅ Done |
| @mentions in comments | 5 | ✅ Done |

---

## Sprint 5 (Weeks 9–10) — Polish & v1.0 Launch

**Sprint Goal:** *Ship a stable v1.0 — fix known bugs, harden performance,
launch to production.*

| Story | Points | Outcome |
|-------|--------|---------|
| Fix top 10 bugs | 8 | ✅ Done |
| Performance: paginate task lists | 5 | ✅ Done |
| Accessibility pass | 5 | ✅ Done |
| Production deploy + monitoring | 5 | ✅ Done |

**Review:** TaskFlow v1.0 ships 🎉. See
[../Semver/Semver.md](../Semver/Semver.md) for how that `1.0.0` version number
is chosen.

**Retro across the whole release:** velocity stabilized, refinement habit paid
off, and slicing thin in Sprint 1 meant zero late-stage architecture surprises.

---

## Velocity across the release

```mermaid
xychart-beta
    title "Story points completed per sprint"
    x-axis [Sprint1, Sprint2, Sprint3, Sprint4, Sprint5]
    y-axis "Points" 0 --> 30
    bar [18, 24, 21, 21, 23]
```

## Lessons from TaskFlow

1. **Deliver a thin end-to-end slice first.** The walking skeleton de-risks everything.
2. **Let velocity be discovered, not decreed.** Plan Sprint *n+1* with the real average.
3. **Protect the Sprint Goal.** New requests go to the backlog, not into the current sprint.
4. **Refinement is continuous.** Grooming next sprint's stories *this* sprint keeps planning short.
5. **Retros compound.** One small improvement per sprint adds up over a release.
