# PRD Depth And Readiness Rubric

Use this for drafting a full PRD or assessing readiness. Full means domain-specific, understandable, and verifiable; it is not a heading or word-count target.

## Scope Before Depth

- A new full PRD includes the applicable problem, roles/stories, model, rules, modules, permissions, dependencies/recovery, milestones, and acceptance.
- An existing document or section-only request preserves the useful current outline. Complete the affected rules and dependencies without rebuilding unrelated chapters.
- An explicitly requested brief stays brief while retaining material scope, ownership, dependency, and uncertainty.
- A review identifies concrete gaps and effects, rather than restating a generic template.

A summary that replaces a requested full PRD is incomplete. A detailed scoped revision does not become incomplete because it has fewer than a fixed number of chapters.

Depth is different from published volume. Readers need the relevant behavior and outcome; internal reasoning, field inventories, and verification matrices do not all belong in the body. A milestone summary can stay short while the page solution carries the necessary detailed rules. A separate acceptance chapter depends on the requested purpose, rather than the word "full".

## Depth Dimensions

| Dimension | Thin Output | Reviewable Output |
|---|---|---|
| Problem | Feature wishes | Work, context, pain, cause, scale, impact, constraints, and chosen path |
| Role needs | Persona or UI preference list | Actual responsibility, cadence, volume, decisions, desired outcome, and evidence |
| Concepts | Nouns without relationships | Meaning, ownership, cardinality, source, lifecycle, and distinctions |
| Rules | Support CRUD or automate | Deterministic inputs, scope, validation, action effect, conflicts, permissions, and recovery |
| Data | Numbers and symbols | Decision served, source, population, units, time/version, readable formula, precision, and reconciled examples |
| Modules | Columns and buttons | Purpose, carried context, information groups, complete actions, states, return path, and acceptance |
| Permissions | Checkmarks | Role x action/state x object/data scope x approval x feedback x audit |
| Batch | Many single forms | Actual workload, input throughput, whole-batch validation, correction, execution scope, idempotency, and result |
| Delivery | Vague phase labels or a copied field/exception inventory | Iteration functions and user outcomes; grounded schedule, dependencies, parallel work and exit conditions when requested |
| Expression | Prompt rules or dense paragraphs | Business-readable responsibility/action/result, consistent terms, semantic emphasis, and appropriate figures/tables |
| Evidence | Claims of completion | Actual written artifact, readback, rendered checks where needed, and precise verification level |

## Readiness Questions

1. Which work problem is solved, for whom, how often, and at what scale?
2. Which constraints are confirmed, which are inherited habits, and which decisions remain open?
3. Are role needs distinguished from design review, writing instructions, and assistant inference?
4. Are the core objects, their relationships, and the source of truth clear?
5. Are save/preview, request/approval, execution/acknowledgment, and current-state effects distinguished where they exist?
6. Can engineering determine validation, permission, conflict, lifecycle, and audit behavior?
7. Can a business reader understand metrics without decoding engineering symbols? Do units, time/version, population, and precision agree?
8. Are comparison population, displayed subset, and modified/executed set explicit?
9. Do normal examples contain complete coherent data, with source/illustrative status clear? Are real exceptions designed separately?
10. Does every page support a useful decision, with a next action and return/recovery path?
11. Does the batch mechanism fit the cadence and workload, including full-batch constraints across pages?
12. Are action guidance, static evidence, comparison, and history organized by meaning?
13. Does each iteration state the main functions and what users can do afterward, without repeating every page rule? Does a requested execution schedule use actual dependencies, estimates and parallel work?
14. Are canonical prose, figures, prototypes, permissions, examples, and acceptance synchronized after changes?
15. Do delivery claims match the evidence, with proposed dates and unverified runtime behavior distinguished?

## Artifacts As Needed

For a complex PRD, choose artifacts that answer actual review questions:

- Role/work/evidence and scenario/story tables.
- Concept relationship and system boundary diagrams.
- Entity/field tables, decision rules, and lifecycle views.
- Core flow or sequence for ordering and asynchronous results.
- Metric dictionary and data/interface contracts.
- Relevant module/action specifications and permission matrix.
- Batch input/validation/submission contract.
- Audit, notification, exception, and recovery rules.
- Capability milestone and acceptance tables.

Prefer a target-native editable diagram where supported; use styled Mermaid when appropriate. The diagram must exist and be readable, rather than a placeholder. Avoid adding nodes, states, warnings, or tables merely to reach a count.

## Final Review Gates

| Gate | Evidence | Repair If Missing |
|---|---|---|
| Requested scope preserved | Current decisions and withdrawn scope checked | Reconcile latest context before editing |
| Real work modeled | Role, cadence/scale, pain, outcome, source | Separate actual needs from review instructions |
| Objects and effects coherent | Model, ownership, stages, state truth | Fix affected fields and actions across surfaces |
| Data traceable | Population, unit, time/version, source, formula, arithmetic | Define canonical metrics and complete representative data |
| Modules usable | Decision, groups, closed action, permission, return/recovery | Fill behavior gaps rather than adding decorative pages |
| Batch throughput fits | Full-batch validation and exact execution set | Redesign from workload instead of multiplying single forms |
| Delivery concrete | Iteration scope and user outcome; supported schedule detail when needed | Replace vague labels with usable increments, or condense an over-detailed task inventory |
| Expression readable | Positive product semantics, stable terms and formatting | Rewrite long clauses and prompt-like rules |
| Outcomes testable | Observable scenario results and data consistency; separate acceptance table when useful | Clarify behavior, adding a dedicated check plan only where needed |
| Artifact verified | Readback and rendered evidence for visual changes | Verify target and report limitations accurately |
