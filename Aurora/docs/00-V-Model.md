# Aurora — V-Model Overview

A small, illustrated map of the artifacts that describe the Aurora website. The V opens on the left with intent and closes on the right with verification; implementation sits at the bottom of the V.

```
   Concept / Flow ─────────────────────────────────────► Acceptance Test
   docs/01-Flow.md                                       docs/06-Test.md §A
        │                                                     ▲
        ▼                                                     │
        Requirements ───────────────────────────────► System Test
        docs/02-Requirements.md                       docs/06-Test.md §S
              │                                             ▲
              ▼                                             │
              Design ───────────────────────► Integration Test
              docs/03-Design.md                docs/06-Test.md §I
                    │                              ▲
                    ▼                              │
                    Detailed Design ──► Unit Test
                    docs/03-Design.md §6  docs/06-Test.md §U
                            │              ▲
                            ▼              │
                            Implementation
                            docs/05-Implementation.md
                            (Aurora.html · styles.css · ...)
```

## Reading order

| # | Artifact                                                | Phase           |
|---|---------------------------------------------------------|-----------------|
| 1 | [Flow](./01-Flow.md)                                    | Concept         |
| 2 | [Requirements](./02-Requirements.md)                    | Specification   |
| 3 | [Design](./03-Design.md)                                | Architecture    |
| 4 | [Test Cases](./04-Test-Cases.md)                        | Verification    |
| 5 | [Implementation](./05-Implementation.md)                | Build           |
| 6 | [Test execution & results](./06-Test.md)                | Validation      |

## Traceability

Every requirement in `02-Requirements.md` has an ID (`R-001…`). Every test in `04-Test-Cases.md` carries one or more `R-NNN` tags and a `TC-NNN` id. Every implementation reference in `05-Implementation.md` cites the requirement(s) it satisfies.

## Status

| Phase           | Owner   | Status       |
|-----------------|---------|--------------|
| Flow            | Design  | Approved     |
| Requirements    | Design  | Approved     |
| Design          | Design  | Approved     |
| Implementation  | Build   | Complete v1  |
| Test            | QA      | In progress  |
