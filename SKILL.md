---
name: junco
description: Product requirement analysis and PRD writing methodology based on Junco's "make a good product" approach. Use when Codex needs to help product managers turn raw needs, stakeholder requests, operational pain points, platform/system ideas, or vague feature asks into high-quality full-depth PRDs through problem framing, user path analysis, concept definition, domain modeling, Mermaid concept relationship diagrams, system boundary diagrams, process flows, interaction rules, milestones, and acceptance criteria. Also use when reviewing or improving PRDs for clarity, model quality, diagrams, boundaries, permissions, risks, depth, and delivery readiness.
---

# Junco

## Overview

Use this skill to turn a raw demand into a rigorous PRD. Treat product work as: solving a real problem, matching the user's thinking path, abstracting a clean model, and making the solution tangible through rules, flows, pages, and delivery plans.

Default to Chinese output unless the user asks otherwise.

Use the expression priority: diagram before table, table before prose. Prefer Mermaid diagrams for relationships, flows, boundaries, states, and decisions; use tables for fields, permissions, rules, and acceptance criteria; use prose for rationale, tradeoffs, context, and exceptions.

Mermaid quality is part of PRD quality. Core diagrams should not be toy diagrams. They should expose enough domain structure to support review: actors, core objects, ownership, rules/control points, data/source-of-truth, lifecycle or exception handling where relevant. For `graph`, `flowchart`, and `stateDiagram` diagrams, use web-safe `classDef` and `class` statements from `references/diagram-patterns.md`; do not output default monochrome diagrams.

Default to full PRD mode for complex platform, system, workflow, governance, or operations products. Do not produce a lightweight outline unless the user explicitly asks for a brief. If source information is thin, proceed with explicit assumptions and open questions, but still design the model, rules, states, and acceptance path.

## Core Principle

Do not start from pages or features. Start from the problem.

Use this product definition as the anchor:

> A product is the tangible expression of a thinking path for solving a problem.

A good PRD should let business, product, design, engineering, QA, and operations share the same understanding of:

- What problem is being solved
- Who has the problem and why it matters
- What concepts and models the system is built on
- What users do in each scenario
- What rules, permissions, states, and exceptions govern the product
- What is in scope now, what is later, and how delivery is verified

## Interaction Rule Abstraction

When a concrete UX issue appears, do not stop at a negative rule such as "do not show X" or "X must not happen". First abstract the product logic behind it, then write the rule.

For every interaction rule, answer these questions before writing requirements:

- User information: What does the user need to know at this decision point? Is the information meaningful, timely, and proportional to the user's current intent?
- Action closure: After seeing the information, what can the user do next? Is there a clear path for success, fallback, correction, or exit?
- User friendliness: Does the solution reduce cognitive load, avoid premature pressure, and respect where the user is in the decision journey?
- Ambiguity risk: What could the user misunderstand? Are labels, statuses, locations, rankings, confidence cues, and warnings expressed in user language rather than internal implementation language?
- Data-to-action fit: Does the data shown support the action being offered? For example, a map marker used for navigation should represent an actual arrival point, entrance, parking lot, visitor center, or route start rather than an abstract area center.

Write quality gates as positive product standards with acceptance criteria and failure examples, not only as prohibitions. Examples:

- Instead of only "recommendation cards must not show preparation items", write "recommendation cards help users make the first decision of whether a place is worth opening; preparation items belong in the detail or pre-departure moment after intent is formed."
- Instead of only "map points must not fall in water", write "map locations must support navigation and arrival; coordinates must point to a reachable entrance, parking lot, visitor center, or route start, and large-area destinations need an explicit recommended entry point."
- Instead of only "do not expose internal logic", write "user-facing copy should express the value, state, or next action the user cares about, not implementation details, ranking mechanics, or product configuration."

## Feedback-to-Rule Method

Use this method when iterative product implementation reveals repeated UX, wording, data, or layout problems. The goal is to turn local feedback into reusable product standards without binding the skill to one project.

1. Extract the decision moment.
   - Identify what decision the user is making on this surface: open, compare, filter, trust, navigate, prepare, share, submit, or correct.
   - Name the stage in the journey. A recommendation card, detail page, form, map, and admin table should not carry the same information weight.

2. Separate user language from internal language.
   - User-facing labels should describe the benefit, state, or next action the user cares about.
   - Keep implementation mechanics, ranking internals, confidence codes, default states, and workaround language out of the UI unless the user needs them to act.
   - If a label can be read as "why would I choose the opposite?", reframe it. For example, a ranking dimension based on evidence quality may be shown as "information complete" rather than "trustworthy".

3. Check option orthogonality.
   - A filter group should contain options at the same conceptual level.
   - Do not mix a parent category with its children in one multi-select group, such as a broad transport category beside specific modes.
   - If users need both levels, split them into separate controls or choose the level that directly supports the decision.

4. Match information timing to intent.
   - Early surfaces should help users decide whether to continue.
   - Later surfaces should support commitment, preparation, risk review, and execution.
   - Move heavy, anxiety-producing, or operational details later unless they are hard blockers for the current decision.

5. Align visual semantics with product semantics.
   - Colors, grouping, spacing, and placement are part of the product contract, not decoration.
   - Positive actions should not use danger colors. Pending, unknown, or unverified states should not use success colors.
   - Controls that belong to one decision should remain visually grouped; orphaned chips, isolated buttons, or accidental line breaks create false hierarchy.

6. Verify data-to-action fit.
   - Every action must be backed by data precise enough to complete it.
   - A navigation action needs reachable coordinates. A location badge needs a real place name. A warning needs a source or a confidence state. A filter needs data that can actually distinguish results.
   - If the data is uncertain, provide a fallback and correction path rather than pretending it is confirmed.

7. Keep product documents and implementation rules in sync.
   - When feedback changes interaction logic, update the PRD, acceptance criteria, and project agent rules together.
   - Write the rule as a positive standard with a failure example so future changes can be checked without relying on memory.
   - The PRD should describe the user-facing principle; implementation rules can add concrete checks for files, fields, and UI states.

## Workflow

Follow this sequence when helping with requirements or PRDs.

0. Calibrate output depth and context.
   - Decide whether the user needs a full PRD, review, outline, or brainstorming answer. If they ask for a PRD, assume full PRD.
   - Identify missing context early. Ask only when the gap blocks safe modeling; otherwise state assumptions and open questions in the PRD.
   - Use `references/prd-depth-rubric.md` before drafting or reviewing a shareable PRD.

1. Reframe the request as a problem.
   - Identify the requester, context, current workaround, pain, impact, and root cause.
   - Treat the user's requested feature as a possible solution, not the requirement itself.
   - Write explicit goals and non-goals.

2. Capture user thinking paths.
   - Identify roles, daily behavior, responsibilities, anxieties, incentives, and decision points.
   - Preserve existing user mental models when they are valuable.
   - Call out where current paths are confusing, risky, slow, or over-coupled.

3. Define concepts before functions.
   - Create a glossary for every core noun.
   - Distinguish similar concepts and name source-of-truth systems.
   - Avoid vague shorthand; clear definitions reduce downstream communication cost.

4. Build the domain model.
   - Identify entities, fields, relationships, states, ownership, data sources, and lifecycle.
   - Separate generic kernel concepts from scenario-specific extensions.
   - Watch for model smells: bulk editing as a workaround, business-only fields in a generic core, unclear source of truth, over-reliance on priority to resolve conflicts.
   - Draw concept relationship diagrams before detailed module design when the requirement has multiple concepts, systems, or ownership boundaries.
   - For complex platform or multi-system products, use `references/platform-patterns.md` for common modeling patterns before writing modules.

5. Derive user stories from role x model.
   - Use roles and entities to enumerate concrete paths.
   - Keep each story valuable, small enough to estimate, and testable.
   - Tie each story to user value and acceptance criteria.

6. Plan the product architecture.
   - Define product positioning, system boundaries, upstream/downstream dependencies, reused capabilities, and new capabilities.
   - Prefer layered designs for complex platforms: kernel, scenario layer, control plane, delivery/runtime layer.
   - State solution tradeoffs and the chosen conclusion when multiple options exist.
   - Use Mermaid diagrams to express system boundaries, layered architecture, data flow, and core sequence flows.
   - Before writing a diagram, decide its question and ensure it includes enough nodes and relationships to answer that question without becoming a generic placeholder.

7. Design tangible functions and interactions.
   - For each module, define page purpose, entry, fields, operations, states, validation, permissions, feedback, and audit.
   - For every P0 module, include list/detail/form fields, operation rules, disabled states, empty/error/no-permission states, audit, and acceptance.
   - Convert concrete UI issues into interaction principles before writing gates: clarify user information, action closure, user friendliness, ambiguity risk, and data-to-action fit.
   - Apply "diagram > table > prose": use diagrams where relationships or flows matter, tables where attributes or rule rows matter, and prose only to explain conclusions.
   - Keep Mermaid diagrams concise, visually tidy, and styled with the web-safe palette in `references/diagram-patterns.md`; for `graph`, `flowchart`, and `stateDiagram`, styling is required.
   - Text should explain logic and rules, not repeat screenshots.

8. Complete rules and delivery.
   - Add permissions, audit, notification, rollback, gray release, migration, exception handling, and high-risk confirmation rules where relevant.
   - Split P0/P1/P2 by closure, risk, dependency, and cost.
   - Define milestones and acceptance criteria.

## Reference Files

Load these files only when needed:

- `references/methodology.md`: detailed demand-to-PRD method and analysis questions.
- `references/diagram-patterns.md`: Mermaid diagram selection rules and reusable templates for concept relationships, architecture, flows, and state machines.
- `references/prd-depth-rubric.md`: full-depth PRD gates, thin-PRD anti-patterns, and final self-review rules.
- `references/platform-patterns.md`: common modeling patterns for complex platform products, including kernel/extension separation, layered architecture, lifecycle governance, views, and ownership.
- `references/prd-template.md`: reusable PRD structure and table templates.
- `references/review-checklist.md`: PRD quality review checklist and common anti-patterns.

## Output Expectations

When drafting a PRD, produce a structured document with these sections unless the user asks for a lighter output:

1. Background and problem definition
2. Goals and non-goals
3. Concepts and glossary
4. User roles and scenarios
5. Product positioning and system boundaries
6. Domain model and key rules
7. Product solution overview
8. Detailed module design
9. Permissions, audit, data, and dependencies
10. Milestones, priorities, risks, and acceptance criteria

For a shareable PRD, each section must contain domain-specific content, not generic placeholder language. Do not leave a diagram section as "shown below" without an actual diagram. If a section is not applicable, write why it is not applicable.

For medium or complex platform PRDs, include Mermaid diagrams in the PRD:

- Concept relationship diagram
- System boundary / layered architecture diagram
- Core flow or sequence diagram
- State machine diagram when lifecycle exists
- Data ownership / source-of-truth diagram when multiple systems exchange data

Keep diagrams compact but meaningful: one diagram answers one question, labels are short and business-readable, arrows are labeled with verbs, and overloaded diagrams should be split. For core concept, boundary, layered, and decision diagrams, a useful diagram usually has 8-14 meaningful nodes; fewer nodes are acceptable only when the domain is genuinely simple.

Before finalizing a PRD, run the depth gates in `references/prd-depth-rubric.md`. A PRD is not ready if it only lists background, goals, a few concepts, CRUD modules, a simple permission table, and phases.

When reviewing an existing PRD, lead with gaps and risks:

- Problem clarity gaps
- Concept/model ambiguity
- Boundary or ownership issues
- Missing user paths
- Missing state, permission, audit, validation, or exception rules
- Delivery, dependency, and acceptance gaps

## Quality Bar

A strong PRD should create four kinds of certainty:

- Business certainty: why this problem matters and what value is expected.
- User certainty: what each role does in each scenario.
- Engineering certainty: model, states, rules, interfaces, permissions, and boundaries are implementable.
- Delivery certainty: scope, phases, risks, and acceptance criteria are explicit.

It should also have high information density: use diagrams instead of tables when relationships matter, tables instead of prose when rows and columns communicate faster, and concise prose only where judgment is needed.

For product experience, a strong PRD should also create interaction certainty: each UI surface should make clear what information the user receives, what decision it supports, what action can close the loop, what fallback exists when data is missing or uncertain, and what ambiguity has been removed through wording, timing, and data choice.
