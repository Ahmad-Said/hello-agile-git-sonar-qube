# Kanban Workflow

Kanban is a **flow-based** Agile method. Unlike Scrum, there are no fixed-length
sprints — work flows continuously, and the focus is on **limiting work in
progress (WIP)** so things actually get *finished* instead of all starting at once.

## When to choose Kanban over Scrum

| Use Kanban when… | Use Scrum when… |
|------------------|-----------------|
| Work arrives unpredictably (support, ops, maintenance) | You can plan a goal for a fixed period |
| Priorities change frequently within a day | You want a regular delivery cadence |
| You want continuous delivery | You want time-boxed commitments |
| The team is interrupt-driven | The team can protect focus for a sprint |

## A basic Kanban board

```mermaid
flowchart LR
    subgraph Backlog
        A1[Story A]
        A2[Story B]
        A3[Story C]
    end
    subgraph "To Do (WIP 3)"
        B1[Task 1]
    end
    subgraph "In Progress (WIP 2)"
        C1[Task 2]
        C2[Task 3]
    end
    subgraph "Review (WIP 2)"
        D1[Task 4]
    end
    subgraph Done
        E1[Task 5]
        E2[Task 6]
    end
    Backlog --> B1 --> C1 --> D1 --> E1
```

The numbers in parentheses are **WIP limits** — the maximum number of items
allowed in that column at once.

## Why WIP limits matter

When everything is "in progress," nothing is done. Limiting WIP forces the team
to **finish before they start** and exposes bottlenecks.

```mermaid
flowchart TD
    A[New work pulled in] --> B{Is the next<br/>column at its<br/>WIP limit?}
    B -- No --> C[Pull the item forward]
    B -- Yes --> D[STOP — swarm to clear<br/>the bottleneck first]
    D --> C
    C --> E[Item moves toward Done]
```

> **Pull, don't push.** Work is *pulled* into a column only when there's
> capacity, rather than *pushed* onto whoever is next.

## Flow as a state machine

```mermaid
stateDiagram-v2
    [*] --> Backlog
    Backlog --> ToDo: Prioritized
    ToDo --> InProgress: Capacity available
    InProgress --> Blocked: Impediment found
    Blocked --> InProgress: Unblocked
    InProgress --> Review: Work complete
    Review --> InProgress: Changes requested
    Review --> Done: Approved
    Done --> [*]
```

## Key Kanban metrics

| Metric | What it measures | Why you care |
|--------|------------------|--------------|
| **Lead time** | From request to delivery | What the customer experiences |
| **Cycle time** | From "started" to "done" | Team's actual working speed |
| **Throughput** | Items finished per week | Capacity / forecasting |
| **WIP** | Items in progress now | Early warning of overload |

### Cumulative Flow — a healthy board

Bands should stay roughly parallel. A widening band means a column is becoming a
bottleneck (work entering faster than it leaves).

```mermaid
xychart-beta
    title "Throughput: items completed per week"
    x-axis [Wk1, Wk2, Wk3, Wk4, Wk5, Wk6]
    y-axis "Items done" 0 --> 15
    bar [6, 8, 7, 9, 11, 10]
```

## Scrum vs Kanban side by side

```mermaid
flowchart TB
    subgraph Scrum
        S1[Fixed-length sprints] --> S2[Commit to a Sprint Goal]
        S2 --> S3[Review + Retro each sprint]
    end
    subgraph Kanban
        K1[Continuous flow] --> K2[Limit WIP per column]
        K2 --> K3[Optimize cycle time]
    end
```

Many teams blend the two ("**Scrumban**"): sprint cadence and retros from Scrum,
plus WIP limits and pull-based flow from Kanban.
