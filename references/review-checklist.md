# PRD Review Checklist

Use this checklist to review or improve PRDs.

## Problem Clarity

- The PRD reframes the request as a real problem.
- It separates symptom, root cause, impact, and proposed solution.
- It includes demand reflection: user request, surface symptom, first-principles problem, challenged assumptions, alternatives, and chosen conclusion.
- It treats the stakeholder's implementation path as a hypothesis, not as the requirement itself.
- It identifies whether the actual fix should be feature-level, model-level, data-level, rule-level, process-level, or operational.
- It explains why current process or system is insufficient.
- It states goals and non-goals.
- It includes evidence or examples when available.

## User Thinking Path

- User roles are specific, not just "user".
- Each role has responsibilities, daily behavior, needs, and concerns.
- The PRD explains the user's natural thinking path, not only the product's page flow.
- The solution aligns with user cognition enough to feel natural without excessive training.
- Human motivations behind behavior are considered: certainty, control, trust, safety, efficiency, anxiety, recognition, or curiosity where relevant.
- Existing mental models are preserved where useful.
- High-frequency paths are prominent.
- Risky paths are slowed down with confirmation, preview, or permissions.

## Concepts And Model

- Core nouns are defined clearly.
- Similar concepts are distinguished.
- Concepts are defined as shared language for product, engineering, design, operations, and users.
- Source-of-truth systems are named.
- Entities, relationships, states, ownership, and lifecycle are explicit.
- Complex products have explicit object, relationship, lifecycle, version/history, and ownership models.
- Decision, priority, conflict, publish, rollback, and downstream consistency rules are defined when relevant.
- Concept relationships are shown with a diagram when there are multiple nouns or ownership boundaries.
- Relationship arrows are labeled with verbs such as owns, maps to, depends on, writes, reads, triggers, or audits.
- Generic kernel concepts are separated from scenario-specific extensions.
- The model can support foreseeable future scenarios without changing the skeleton.

## Rules And Boundaries

- Product/system boundaries are explicit.
- System boundary or layered architecture is diagrammed when multiple systems collaborate.
- Upstream and downstream responsibilities are clear.
- Boundary conditions and exceptions are designed as product "game rules", not left as implementation details.
- Permission matrix exists for key actions.
- Status machine exists where lifecycle matters.
- Core write/read/approval/submission paths are represented with sequence diagrams or flowcharts when order matters.
- Validation rules, defaults, required fields, and uniqueness constraints are defined.
- Every P0 module has fields, operations, preconditions, disabled states, errors, audit, and acceptance criteria.
- High-risk actions have confirmation and audit.
- Exceptions, empty states, no-permission states, and dependency failures are covered.

## Delivery Readiness

- P0/P1/P2 are based on closure, risk, dependency, and cost.
- The chosen solution is the minimum sufficient path after comparing simpler or more universal alternatives.
- Milestones describe capability maturity, not just dates.
- Dependencies and risks have owners.
- Acceptance criteria are testable.
- Data, interfaces, migration, and fallback are considered.

## Expression Quality

- The PRD follows "diagram > table > prose": diagrams for relationships/flows/boundaries/states, tables for repeated attributes/rules, prose for rationale and conclusions.
- The PRD uses diagrams, tables, matrices, and state machines where they communicate better than prose.
- For complex PRDs, diagrams include concept relationship, system boundary, core flow, and state machine views.
- Diagram sections contain actual Mermaid diagrams, not placeholder text such as "shown below".
- Mermaid diagrams are concise, visually tidy, and split when one diagram tries to answer multiple questions.
- Core Mermaid diagrams are not toy diagrams; they show enough actors, objects, rules, data, audit, runtime, and exception nodes to support review.
- `graph`, `flowchart`, and `stateDiagram` diagrams use `classDef` and `class` statements from a consistent web-safe color palette.
- Text explains logic and rules instead of repeating prototypes.
- A reader from product, engineering, design, QA, or operations can understand what they need to do.

## Common Anti-Patterns

- Starting with pages and buttons before defining the problem.
- Treating a stakeholder's solution as the requirement itself.
- Following the user's requested path literally without first-principles reflection.
- Mistaking a visible workaround for the underlying requirement.
- Adding a feature when a concept, data ownership, default rule, permission boundary, or process agreement would solve the problem more simply.
- Producing INVEST-compliant user stories that still follow the wrong path or preserve a bad existing structure.
- Delivering a four-page outline when the user asked for a full PRD.
- Skipping concept definitions and letting teams argue over words during review.
- Defining many concepts in tables but not showing their relationships.
- Stopping at "support CRUD" without fields, rules, states, edge cases, and acceptance criteria.
- Describing key actions or decision logic without lifecycle, precedence, conflict, and audit rules.
- Showing a permission table with checkmarks but no data scope, ownership, disabled states, or audit implications.
- Replacing clear diagrams with long tables or prose when a relationship or flow is the real point.
- Creating Mermaid diagrams that are either too shallow, such as `User -> Product -> System`, or too dense with crossing arrows, unlabeled edges, or inconsistent colors.
- Outputting default monochrome `graph`, `flowchart`, or `stateDiagram` diagrams without web-safe classes.
- Designing only by feature scenes without a domain model.
- Putting business-specific fields into a generic platform core.
- Using bulk edit to hide poor model abstraction.
- Covering only happy paths.
- Missing permissions, audit, status, validation, or exception rules.
- No non-goals, leading to uncontrolled scope expansion.
- A long PRD with low information density and no clear structure.
