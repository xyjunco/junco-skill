# Junco Demand-to-PRD Methodology

## Core Mental Model

Product work starts from a problem, not from a requested feature. A product is the tangible expression of a thinking path for solving a problem.

Use this chain:

`Problem -> User thinking path -> Concept definition -> Domain model -> User stories -> Product architecture -> Interaction rules -> Delivery plan -> PRD`

For medium or complex platform requirements, diagram before writing long prose:

`Concept relationship -> System boundary -> Data / responsibility flow -> User / system sequence -> State machine`

Before drafting, calibrate depth:

- Full PRD: default for complex platform, system, workflow, governance, and operations products.
- Outline: only when the user explicitly asks for a brief.
- Review: lead with gaps, risks, and concrete fixes.

If context is incomplete, do not shrink the PRD into generic bullets. Write assumptions, open questions, and TODOs, then still complete the model, flow, rules, and acceptance criteria with the best defensible design.

## 1. Reframe Demand As Problem

Ask:

- Who raised the demand?
- What scenario triggered it?
- What does the user want on the surface?
- What problem is hidden behind that request?
- What is the current workaround?
- Why is the current solution not enough?
- What happens if this is not solved?
- What measurable impact exists: frequency, cost, duration, failure rate, incident level, affected users?

Problem statement template:

```markdown
In [scenario], [role] needs to [goal], but because [root cause], [negative impact] happens. This PRD solves [core problem], and does not solve [non-goal].
```

Good problem statements separate:

- Symptom: what users complain about
- Root cause: why it happens
- Impact: why it matters
- Scope: what this iteration will solve

## 2. Capture User Thinking Paths

Thinking path means how a user naturally understands and solves the problem.

Analyze:

- What object does the user start from?
- What hierarchy, filter, or entry do they expect?
- What information is needed before action?
- What action feels natural after each state?
- What actions are high-frequency and must be prominent?
- What actions are risky and must be slowed down?
- Which existing mental models should be preserved?

For platform tools, existing operational paths often matter more than visual novelty. Preserve valuable paths, but remove accidental complexity.

## 3. Define Concepts

Do concept work before page work.

For every important noun, define:

| Concept | Definition | Example | Boundary / Distinction |
| --- | --- | --- | --- |
|  |  |  |  |

Definition rules:

- Do not be too terse.
- Distinguish similar terms explicitly.
- Name source-of-truth systems.
- Explain whether the concept is generic core, scenario extension, metadata, runtime data, or view-only data.
- Avoid overloaded terms if they conflict with existing domain vocabulary.

## 4. Build Domain Model

Model the system before designing screens.

Cover:

- Entities and unique identifiers
- Entity fields, types, requiredness, defaults, validation
- Relationships: ownership, dependency, mapping, reference, binding
- Lifecycle and status machine
- Data source and write owner
- Permissions and responsibility
- Audit and traceability
- Runtime vs management-side data

Model smells:

- Users request bulk edit for many rows with the same value. This may mean those rows should share a logical entity.
- A generic system contains fields belonging to one business scenario.
- Conflict is solved by priority instead of validation and deterministic matching.
- Multiple systems own the same data without source-of-truth clarity.
- A high-frequency runtime path depends on a management system that cannot meet availability or performance expectations.

After the model is identified, draw at least one concept relationship diagram. The diagram should answer:

- What are the core nouns?
- Who owns or operates each noun?
- Which concept contains, maps to, depends on, or triggers another?
- Which system is the source of truth?
- Which parts are management-side concepts and which are runtime concepts?

Use `references/diagram-patterns.md` for Mermaid templates.

For complex platform or multi-system products, also use `references/platform-patterns.md` for common modeling patterns.

## 5. Derive User Stories With Role x Model

Use roles and models to derive user stories.

| Role / Model | Entity A | Entity B | Rule / Policy | Audit / History |
| --- | --- | --- | --- | --- |
| User | View / submit / edit | Select / bind | Trigger | View |
| Manager | Create / maintain | Configure | Enable / approve | Trace |
| Platform owner | Define / initialize | Sync | Guardrail / fallback | Global audit |

User story template:

| Role | Scenario | I want to | So that | Function | Acceptance |
| --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  |

Keep stories:

- Independent
- Negotiable
- Valuable
- Estimable
- Small enough for one iteration when possible
- Testable

## 6. Plan Product Architecture

Before detailed UI, define:

- Product positioning in the wider system
- Upstream and downstream systems
- What this product owns
- What it reuses
- What it only references
- What is newly built
- What is current scope vs future scope

Draw system diagrams here instead of relying only on text:

- System boundary diagram: users, product, upstream systems, downstream systems.
- Layered architecture diagram: metadata, control plane, runtime / delivery layer.
- Data flow or sequence diagram: write path, read path, approval path, task submission path.
- State machine diagram: core object or workflow lifecycle.

Useful architecture patterns:

- Minimal kernel + scenario plugins: for generic task/workflow platforms.
- Metadata layer + management/control layer + runtime delivery layer: for high-read or high-risk systems.
- Business view + architecture/resource view: for CMDB and resource management systems.
- First manage, then govern: for risk, quota, storage, audit, or lifecycle platforms.
- Control plane above baseline capability: for gray release, emergency block, rollback, or high-risk governance.

When multiple solutions exist, compare:

| Solution | Description | Pros | Cons | Risks | Conclusion |
| --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  |

## 7. Detail Product Modules

For each module, specify:

- Module positioning
- Entry and context
- Core data displayed
- Fields and source
- Operations and state constraints
- Validation and error handling
- Permission and visibility
- Audit and notification
- Empty, loading, disabled, failure, and no-permission states

For every P0 module, do not stop at a capability bullet such as "support CRUD". Expand it into:

- Entry: where the user starts and what context is carried.
- List/detail/form fields: visible fields, source, default, validation, permission, and sorting/filtering.
- Operations: create, edit, delete, copy, enable, disable, submit, approve, publish, rollback, retry, export, or other domain actions.
- State constraints: when operations are hidden, disabled, blocked, or require confirmation.
- Error and exception handling: conflict, dependency unavailable, partial success, no permission, stale data, and validation failure.
- Audit and notification: what is recorded, who receives it, and where users can trace it.

Field template:

| Field | Meaning | Type | Source | Required | Default | Validation | Permission / State | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  |  |  |  |

Operation template:

| Operation | Entry | Preconditions | Flow | Success Feedback | Failure Feedback | Audit | Permission |
| --- | --- | --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  |  |  |

State machine template:

| Current State | Action | Next State | Actor | Validation | User Feedback |
| --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  |

## 8. Complete Rules, Risks, And Delivery

Rules to check:

- Permission matrix
- Status machine
- Required fields and validation
- High-risk action confirmation
- Diff, preview, version, rollback, and release notes when changes are high risk
- Audit trail: who, when, why, before, after
- Notifications: trigger, audience, frequency, content, action links
- Exception paths: empty, conflict, unavailable dependency, no permission, partial failure
- Migration: existing data, ownership, cleanup, fallback

Final self-review:

- If the PRD has only background, goals, concept definitions, CRUD bullets, a simple permission table, and phase list, it is an outline, not a full PRD.
- If a concept relationship section says "as follows" but no diagram is present, the PRD is incomplete.
- If a product with complex rules lacks precedence, conflict handling, lifecycle state, audit, and downstream consistency rules, the model is incomplete.
- If a P0 module has no fields, operations, state constraints, and acceptance criteria, the implementation contract is incomplete.

Priority guidance:

- P0: core path cannot close without it, or risk is unacceptable.
- P1: meaningful efficiency, experience, observability, or governance improvement.
- P2: extension, lower-frequency scenario, or future capability.

Milestone guidance:

- M1: concepts, model, boundary, base chain.
- M2: list/detail, basic operations, audit.
- M3: new data onboarding, permission, admission, system integration.
- M4: automation, alerting, governance.
- M5: operational loop, forecasting, optimization.
