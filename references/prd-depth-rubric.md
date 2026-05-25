# PRD Depth Rubric

Use this before drafting or reviewing a shareable PRD. The goal is to prevent a full PRD from collapsing into a short capability outline.

## Full PRD vs Outline

A short outline may be acceptable for early brainstorming only. A full PRD is expected when the user asks for a PRD, product proposal, product design, or can-share document for engineering/design/QA review.

Summary-only output is a failure mode. A response that lists section headings, a few decisions, delivery features, and next steps is not a full PRD, even if it mentions diagrams or claims the content is complete.

A full PRD must not merge away user stories, usage scenarios, permissions, audit, dependency recovery, or QA verification. These sections are required because they make the design reviewable by design, engineering, QA, and operations.

| Dimension | Outline | Full PRD |
| --- | --- | --- |
| Problem | Lists pain points | Separates user request, surface symptom, first-principles problem, current process, root cause, impact, scope, evidence |
| Concepts | Defines a few nouns | Defines nouns, boundaries, source of truth, lifecycle, relationships |
| Model | Light entity list | Entity IDs, fields, ownership, states, cardinality, data source |
| Rules | General statements | Deterministic decisions, validation, conflicts, permissions, audit, exceptions |
| Modules | CRUD bullets | Entry, layout, fields, operations, states, errors, audit, acceptance |
| Permissions | Mentions roles | Role x operation x data scope x approval x disabled state x audit matrix |
| Delivery | Phase list | Priority rationale, dependencies, risks, rollout, acceptance |

## Depth Gates

A platform/system PRD is not ready unless it answers these questions:

1. What did the user ask for on the surface, and what first-principles problem is hidden behind it?
2. Which assumptions in the requested path are real constraints, and which are inherited habits or workarounds?
3. What simpler, more universal, or more model-level solutions were considered before choosing the final path?
4. What are the core nouns, and how do they relate?
5. Which system owns each noun and field?
6. What is the source of truth for read and write paths?
7. What lifecycle states exist, and what operations are allowed in each state?
8. What decision, priority, validation, and conflict rules produce deterministic outcomes?
9. What happens when upstream/downstream dependencies fail?
10. What does each role see, change, approve, or audit?
11. What exact fields appear on the key list/detail/form surfaces?
12. What audit, notification, rollback, and recovery path exists for risky operations?
13. How will QA verify main paths, permission paths, exception paths, and data consistency?

## Required Artifacts For Complex PRDs

Include these unless clearly not applicable:

- Demand reflection table: user request, surface symptom, first-principles problem, challenged assumptions, alternatives, chosen conclusion.
- User role table with responsibility, decision moment, authority, and success signal.
- Usage scenarios and user stories for happy path, exception path, permission-limited path, and recovery path.
- Concept relationship diagram.
- System boundary or layered architecture diagram.
- Core decision flow or sequence diagram.
- State machine for lifecycle objects.
- Entity table with unique ID, owner, and source of truth.
- Field table for core entities and P0 surfaces.
- Operation table for P0 modules.
- Permission matrix with data scope and notes.
- Audit and notification rules.
- Data/interface dependency table with consistency and fallback.
- Acceptance criteria covering success, permission, validation, dependency failure, and audit.

## Thin PRD Anti-Patterns

These are signals that the output is still too shallow:

- It says "main entities and relationships are as follows" but no diagram follows.
- It defines concepts but never shows cardinality, source of truth, or lifecycle.
- It lists modules as generic capability names without fields and operation rules.
- It skips user stories or reduces scenarios to a short role list.
- It uses checkmarks for permissions but does not define data scope, ownership, disabled states, and audit.
- It skips the permission matrix entirely or hides permissions inside module prose.
- It explains a key switch or high-risk action but lacks state machine, execution path, conflict behavior, and rollback.
- It has phases but no acceptance criteria.
- It has generic prose that could apply to many products after replacing nouns.
- It ends with a short "delivery features", "next steps", or "summary" block without the detailed PRD sections.
- It claims a PRD has been created but the actual response or target document only contains condensed decisions and high-level bullets.

## Final Self-Review

Before finalizing, scan the PRD and mark each item as pass/fail:

| Gate | Pass / Fail | Fix If Failed |
| --- | --- | --- |
| Demand is reflected from first principles |  | Add user request, surface symptom, root problem, challenged assumptions, alternatives, chosen conclusion |
| Problem is reframed with root cause and impact |  | Add current process, root cause, impact, scope |
| Concepts and relationships are diagrammed |  | Add concept relationship diagram and entity table |
| User stories and usage scenarios are explicit |  | Add role-action-value-acceptance stories and happy/exception/permission/recovery scenarios |
| Core rules are deterministic |  | Add decision, validation, conflict, and fallback rules |
| P0 modules are implementable |  | Add fields, operations, state constraints, errors, audit |
| Permissions are implementable |  | Add role x operation x data scope x approval x disabled state x audit matrix |
| Dependencies are explicit |  | Add system boundary and interface table |
| Acceptance is testable |  | Add scenario-based acceptance rows |
