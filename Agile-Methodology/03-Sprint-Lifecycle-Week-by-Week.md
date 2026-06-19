# Sprint Lifecycle: Week by Week

This walks through a typical **2-week sprint** (the most common length) so you
can see *when* each event happens and *what* the team is actually doing on each
day.

## The sprint at a glance

```mermaid
gantt
    title Two-Week Sprint Timeline
    dateFormat  YYYY-MM-DD
    axisFormat  %a %d

    section Week 1
    Sprint Planning        :done,   p1, 2026-06-01, 1d
    Build & Daily Stand-up :active, b1, 2026-06-02, 4d
    Backlog Refinement     :        r1, 2026-06-04, 1d

    section Week 2
    Build & Daily Stand-up :active, b2, 2026-06-08, 3d
    Code Freeze / Stabilize:        cf, 2026-06-11, 1d
    Sprint Review          :crit,   rv, 2026-06-12, 1d
    Retrospective          :crit,   rt, 2026-06-12, 1d
```

## Day-by-day

### Week 1

| Day | Focus | What happens |
|-----|-------|--------------|
| **Mon** | Sprint Planning | Team agrees the Sprint Goal, pulls stories into the Sprint Backlog, breaks them into tasks. |
| **Tue** | Build | First stand-up of the sprint. Developers pick up the highest-priority tasks. |
| **Wed** | Build | Stand-up. Early integration; raise blockers fast. |
| **Thu** | Build + Refinement | Mid-sprint **Backlog Refinement**: PO and team groom upcoming stories so *next* sprint's planning is smooth. |
| **Fri** | Build | Stand-up. Aim to have something demo-able starting to take shape. |

### Week 2

| Day | Focus | What happens |
|-----|-------|--------------|
| **Mon** | Build | Stand-up. Burndown check — are we on track for the Sprint Goal? |
| **Tue** | Build | Stand-up. Start wrapping up; resist adding new scope. |
| **Wed** | Stabilize | Code freeze for the increment. Final testing, bug-fixing, polish. |
| **Thu** | **Review + Retro** | Demo the increment to stakeholders. Then the team reflects and picks improvements. |
| **Fri** | Buffer / next planning prep | Slack day, deployment, or roll straight into the next sprint. |

## Tracking progress: the burndown chart

A **burndown** shows remaining work (in story points or hours) against time.
The ideal line is a straight slope to zero.

```mermaid
xychart-beta
    title "Sprint Burndown (story points remaining)"
    x-axis [Mon1, Tue1, Wed1, Thu1, Fri1, Mon2, Tue2, Wed2, Thu2]
    y-axis "Points remaining" 0 --> 40
    line [40, 38, 33, 30, 24, 18, 12, 5, 0]
    line [40, 35, 30, 25, 20, 15, 10, 5, 0]
```

- The **first line** is actual remaining work.
- The **second line** is the ideal trajectory.
- Above the ideal line → behind schedule. Below → ahead.

## The decision flow during a sprint

```mermaid
flowchart TD
    Start([Daily Stand-up]) --> Q1{On track for<br/>the Sprint Goal?}
    Q1 -- Yes --> Cont[Continue as planned]
    Q1 -- No --> Q2{Can a blocker<br/>be removed?}
    Q2 -- Yes --> SM[Scrum Master clears it]
    Q2 -- No --> Q3{Scope vs Goal?}
    Q3 -->|Drop lowest-priority story| Replan[Adjust Sprint Backlog<br/>with PO]
    Q3 -->|Goal still reachable| Cont
    SM --> Cont
    Replan --> Cont
    Cont --> End([Keep building])
```

## Common anti-patterns to avoid

- **Scope creep mid-sprint** — new "urgent" work shoved in without dropping anything.
- **Stand-ups that become status reports to a manager** — they're for the team.
- **Skipping the retro** — the one event that makes the team better over time.
- **A "mini-waterfall" sprint** — design all week 1, test all week 2. Slice
  vertically instead so something is *done* early.

Next: see this applied end-to-end in
[Practical-Project-Example.md](./04-Practical-Project-Example.md).
