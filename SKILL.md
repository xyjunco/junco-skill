---
name: junco
description: Product design methodology based on Junco's "make a good product" approach. Use when an AI assistant or product practitioner needs to turn raw needs, stakeholder requests, operational pain points, platform/system ideas, or vague feature asks into high-quality product design through first-principles demand reflection, problem framing, user path analysis, concept definition, domain modeling, Mermaid concept relationship diagrams, system boundary diagrams, process flows, interaction rules, milestones, and acceptance criteria. The final delivery artifact is usually a reviewable PRD, but the skill's purpose is product design quality rather than template completion. Also use when reviewing or improving product plans and PRDs for clarity, model quality, diagrams, boundaries, permissions, risks, depth, and delivery readiness.
---

# Junco

## Overview

Use this skill to turn a raw demand into rigorous product design. Treat product work as: solving a real problem with minimal necessary cost, matching the user's thinking path, abstracting a clean model, defining the operating rules of the product world, and making the solution tangible through rules, flows, pages, and delivery plans. The final artifact may be a PRD, but the work is product design, not template completion.

When receiving a user demand, do not assume the user's stated path is the right path. Treat it as a surface signal. First ask what first-principles problem, invariant constraint, user motivation, or system model issue is hidden behind it, then decide whether the requested implementation is still the simplest sufficient answer.

Default to the user's language unless the user asks otherwise.

Use the expression priority: diagram before table, table before prose. Prefer Mermaid diagrams for relationships, flows, boundaries, states, and decisions; use tables for fields, permissions, rules, and acceptance criteria; use prose for rationale, tradeoffs, context, and exceptions.

Mermaid quality is part of PRD quality. Core diagrams should not be toy diagrams. They should expose enough domain structure to support review: actors, core objects, ownership, rules/control points, data/source-of-truth, lifecycle or exception handling where relevant. For `graph`, `flowchart`, and `stateDiagram` diagrams, use web-safe `classDef` and `class` statements from `references/diagram-patterns.md`; do not output default monochrome diagrams.

Rendering compatibility is also part of PRD quality. Some host tools show Mermaid source code without rendering a preview. Never claim that a rendered preview exists unless the current tool actually renders or embeds one. When the target tool may not render Mermaid, still output a valid fenced `mermaid` code block, then add a short `Diagram Quick Read` after each non-trivial diagram: what the diagram answers, the main path, key branches or exceptions, and ownership/source-of-truth boundaries. If image or file-rendering tools are available and the user asks for a visual preview, generate and attach a rendered SVG/PNG while keeping the Mermaid source.

Default to full product-design mode for complex platform, system, workflow, governance, or operations products. Do not produce a lightweight outline unless the user explicitly asks for a brief. If source information is thin, proceed with explicit assumptions and open questions, but still design the model, rules, states, and acceptance path, then deliver it in PRD form when a document is needed.

## Core Principle

Do not start from pages or features. Start from the problem.

Do not start from the user's proposed implementation path either. A stakeholder may ask for a button, workflow, dashboard, approval step, bulk edit, alert, or automation because that is the visible workaround available to them. The product job is to recover the underlying problem and find the simplest general solution that makes the workaround unnecessary when possible.

Use this product definition as the anchor:

> A product is the tangible expression of a thinking path for solving a problem.

A good product should meet three standards:

- It solves a real problem with the minimum sufficient cost.
- Its thinking path is universal enough that users can act naturally without excessive explanation.
- Its solution is perceptible or touchable: rules, interactions, objects, and feedback can be experienced by users and understood by teams.

A good PRD should let business, product, design, engineering, QA, and operations share the same understanding of:

- What problem is being solved
- Who has the problem and why it matters
- What concepts and models the system is built on
- What users do in each scenario
- What rules, permissions, states, and exceptions govern the product
- What is in scope now, what is later, and how delivery is verified

## Methodology Summary

Use the full method from "make a good product", not a narrow keyword checklist.

1. Solve the actual problem.
   - The product's root purpose is problem solving. Do not confuse slogans, technologies, AI concepts, or stakeholder wishes with a solved user problem.
   - "Minimum cost" is not "fewest features"; it is the smallest solution that fully closes the real problem without unnecessary complexity.

2. Recover the user's thinking path.
   - A good product feels natural because its path overlaps with how the user already understands and solves the problem.
   - Different users may choose different paths under different information, constraints, and contexts. Preserve valuable mental models and remove accidental complexity.
   - Distinguish the core path from surprise, polish, or secondary delight. Delight cannot replace the core path.

3. Look through behavior to human motivation.
   - Empathy means capturing the user's thinking path from the inside, not merely listing user roles.
   - Surface functional requests often hide psychological, emotional, responsibility, trust, control, efficiency, or safety needs.
   - When demand is vague or contradictory, infer the human driver before designing the feature.

4. Abstract models before stitching functions.
   - Simple tools can follow a linear path, but complex systems need concepts, entities, relationships, ownership, states, and boundaries.
   - Feature-by-feature stitching creates products that feel fragmented, coupled, and hard to understand.
   - Concepts are the shared language for product, engineering, design, operations, and users. Do not make teams pay coordination cost because nouns are vague.

5. Derive user stories from role x model.
   - User stories are concrete thinking paths produced from roles acting on domain objects.
   - They must remain independent, negotiable, valuable, estimable, small enough when possible, and testable.
   - Validate stories with interviews, prototype tests, A/B tests, data, or operational review where relevant.

6. Apply first principles.
   - Return to the most basic conditions, decompose the problem, and rebuild the solution from what must be true.
   - Challenge inherited assumptions such as existing entry points, process steps, physical controls, org habits, default states, and old system constraints.
   - Sometimes the solution is outside the current path or even the current dimension of the problem; broaden the search with cross-domain mental models.

7. Define the product's game rules.
   - The more complex the product, the more boundary conditions, exceptions, protections, and state rules it needs.
   - Rules are not decoration. They determine whether users know what to do, whether systems behave predictably, and whether risk is controlled.

8. Express logic efficiently.
   - Product work is not "drawing screens". A prototype, diagram, table, or prose is only good if it lets each role know what should happen in each situation.
   - Use diagram > table > prose. Avoid dumping unprocessed information or writing long text when a relationship diagram or rule table carries the logic more clearly.

## First-Principles Demand Reflection

Run this reflection before designing a solution, delivering a PRD, or writing a review conclusion.

1. Separate signal from essence.
   - Surface request: What did the user explicitly ask to build or change?
   - Symptom: What pain, complaint, inefficiency, risk, or confusion is visible?
   - Root problem: What basic condition causes the symptom to exist?
   - Impact: Who pays the cost, how often, and how severely?

2. Return to first principles.
   - What is the most basic user goal in this scenario?
   - What must be true for the problem to disappear?
   - Which constraints are real constraints: law, security, physics, organizational responsibility, data availability, cost, latency, or user cognition?
   - Which constraints are only inherited assumptions from the current process, old system, org habit, or implementation history?
   - What human motivation or fear drives the current behavior?

3. Challenge the requested path.
   - If the requested feature could not be built, how else could the problem be solved?
   - Is the request automating an accidental workaround rather than fixing the model?
   - Is the current path too local, while a more universal capability would solve multiple scenarios?
   - Can the solution be made smaller by changing concept definitions, data ownership, defaults, rules, or feedback timing instead of adding UI and process?
   - Is the simplest answer a product feature, a rule change, a data correction, a governance mechanism, an integration, an operational playbook, or doing nothing?

4. Seek the simplest general solution.
   - Prefer the solution that closes the core problem with the fewest concepts, states, permissions, and user steps.
   - Avoid overfitting to a single stakeholder's workflow when a more universal model can serve the same need.
   - Do not pursue cleverness for its own sake. The result should feel natural, obvious, and low-friction after the root problem is understood.
   - Use radical simplicity as a design pressure: reduce accidental complexity, but keep essential rules, boundaries, and risk controls explicit.

5. Record the reflection.
   - For PRDs, include a short demand reflection before goals: user request, surface symptom, first-principles problem, challenged assumptions, alternative solution paths, and chosen conclusion.
   - For reviews, call out when the PRD follows the user's requested path too literally and misses a simpler or more general solution.
   - If the user's path is still correct, explain why it is the simplest sufficient path after reflection.

## Interaction Rule Abstraction

When a concrete UX issue appears, do not stop at a negative rule such as "do not show X" or "X must not happen". First abstract the product logic behind it, then write the rule.

For every interaction rule, answer these questions before writing requirements:

- User information: What does the user need to know at this decision point? Is the information meaningful, timely, and proportional to the user's current intent?
- Action closure: After seeing the information, what can the user do next? Is there a clear path for success, fallback, correction, or exit?
- User friendliness: Does the solution reduce cognitive load, avoid premature pressure, and respect where the user is in the decision journey?
- Ambiguity risk: What could the user misunderstand? Are labels, statuses, locations, rankings, confidence cues, and warnings expressed in user language rather than internal implementation language?
- Data-to-action fit: Does the data shown support the action being offered? For example, a risky submit action should expose the target object, current state, expected consequence, permission basis, and recovery path rather than only showing a generic confirmation.

Write quality gates as positive product standards with acceptance criteria and failure examples, not only as prohibitions. Examples:

- Instead of only "the summary card must not show too many fields", write "summary cards support the first decision of whether an item is worth opening; operational details belong in the detail view after intent is formed."
- Instead of only "the confirmation dialog must not be vague", write "high-risk confirmations must expose object identity, change impact, rollback availability, and the exact user decision being requested."
- Instead of only "do not expose internal logic", write "user-facing copy should express the value, state, or next action the user cares about, not implementation details, ranking mechanics, or product configuration."

## Feedback-to-Rule Method

Use this method when iterative product implementation reveals repeated UX, wording, data, or layout problems. The goal is to turn local feedback into reusable product standards without binding the skill to one project.

1. Extract the decision moment.
   - Identify what decision the user is making on this surface: open, compare, filter, trust, navigate, prepare, share, submit, or correct.
   - Name the stage in the journey. A summary surface, detail page, form, dashboard, and admin table should not carry the same information weight.

2. Separate user language from internal language.
   - User-facing labels should describe the benefit, state, or next action the user cares about.
   - Keep implementation mechanics, ranking internals, confidence codes, default states, and workaround language out of the UI unless the user needs them to act.
   - If a label can be read as "why would I choose the opposite?", reframe it. For example, a ranking dimension based on evidence quality may be shown as "information complete" rather than "trustworthy".

3. Check option orthogonality.
   - A filter group should contain options at the same conceptual level.
   - Do not mix a parent category with its children in one multi-select group, such as a broad resource type beside specific subtypes.
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
   - An execution action needs a stable target object and version. A status badge needs a defined state source. A warning needs a source or confidence state. A filter needs data that can actually distinguish results.
   - If the data is uncertain, provide a fallback and correction path rather than pretending it is confirmed.

7. Keep product documents and implementation rules in sync.
   - When feedback changes interaction logic, update the PRD, acceptance criteria, and implementation guidance together.
   - Write the rule as a positive standard with a failure example so future changes can be checked without relying on memory.
   - The PRD should describe the user-facing principle; implementation rules can add concrete checks for files, fields, and UI states.

## Workflow

Follow this sequence when helping with requirements or PRDs.

0. Calibrate output depth and context.
   - Decide whether the user needs full product design, review, outline, or brainstorming. If they ask for a PRD, assume the PRD should contain full product design unless they explicitly ask for a brief.
   - Identify missing context early. Ask only when the gap blocks safe modeling; otherwise state assumptions and open questions in the PRD.
   - Use `references/prd-depth-rubric.md` before drafting or reviewing a shareable PRD.
   - Treat "product design", "product proposal", "solution", "PRD", and "design this requirement" as full-product-design requests by default. Do not downgrade them into a short answer, executive summary, or phase outline unless the user explicitly asks for a brief.

1. Reframe the request as a problem.
   - Identify the requester, context, current workaround, pain, impact, and root cause.
   - Treat the user's requested feature as a possible solution, not the requirement itself.
   - Apply first-principles reflection: distinguish visible symptom, real constraint, inherited assumption, and the smallest condition that must change.
   - Challenge whether the user's proposed implementation path is necessary, or whether a simpler general rule, model, data, or process change solves the same problem.
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
   - Compare at least one simpler or more universal alternative when the user proposes a concrete implementation path.
   - Use Mermaid diagrams to express system boundaries, layered architecture, data flow, and core sequence flows.
   - Before writing a diagram, decide its question and ensure it includes enough nodes and relationships to answer that question without becoming a generic placeholder.

7. Design tangible functions and interactions.
   - For each module, define page purpose, entry, fields, operations, states, validation, permissions, feedback, and audit.
   - For every P0 module, include list/detail/form fields, operation rules, disabled states, empty/error/no-permission states, audit, and acceptance.
   - Convert concrete UI issues into interaction principles before writing gates: clarify user information, action closure, user friendliness, ambiguity risk, and data-to-action fit.
   - Apply "diagram > table > prose": use diagrams where relationships or flows matter, tables where attributes or rule rows matter, and prose only to explain conclusions.
   - Keep Mermaid diagrams concise, visually tidy, and styled with the web-safe palette in `references/diagram-patterns.md`; for `graph`, `flowchart`, and `stateDiagram`, styling is required.
   - If Mermaid preview support is unknown or absent, pair each important Mermaid diagram with `Diagram Quick Read` so reviewers can understand the diagram without relying on renderer support.
   - Text should explain logic and rules, not repeat screenshots.

8. Complete rules and delivery.
   - Add permissions, audit, notification, rollback, gray release, migration, exception handling, and high-risk confirmation rules where relevant.
   - Split P0/P1/P2 by closure, risk, dependency, and cost.
   - Define milestones and acceptance criteria.

## Reference Files

Load these files only when needed:

- `references/methodology.md`: detailed demand-to-product-design method and analysis questions.
- `references/diagram-patterns.md`: Mermaid diagram selection rules and reusable templates for concept relationships, architecture, flows, and state machines.
- `references/prd-depth-rubric.md`: full-depth PRD gates, thin-PRD anti-patterns, and final self-review rules.
- `references/platform-patterns.md`: common modeling patterns for complex platform products, including kernel/extension separation, layered architecture, lifecycle governance, views, and ownership.
- `references/prd-template.md`: reusable PRD structure and table templates.
- `references/review-checklist.md`: PRD quality review checklist and common anti-patterns.

## Output Expectations

### Delivery Contract

The default deliverable is the full PRD body, not a summary of the PRD. Do not end with only "delivery features", "next steps", or a condensed overview when the user asked for product design, a product proposal, or a PRD.

If no external document target is explicitly requested, write the complete PRD inline in the current response. If the response would be long, continue with the complete structure instead of compressing it into a summary; split only if the host tool forces a hard length limit, and then say exactly which sections are included in this part and which section should continue next.

If an external document target is requested, write the full PRD to that target and then return only a short completion note with the document link and a validation summary. Do not claim the full PRD was written unless the document actually contains the full PRD body.

Never substitute a short table, bullet summary, or "key decisions" section for the detailed PRD body. Summary sections may appear at the top, but they are additive and must be followed by the complete sections.

Some host models compress by default. Counter that explicitly: for a full PRD, use the required section set below, keep the section headings visible, and do not merge required sections into each other. If a required section seems not applicable, keep the heading and explain why it is not applicable.

When delivering the product design as a PRD, produce a structured document with these sections unless the user asks for a lighter output:

1. Demand Reflection And First-Principles Interpretation
2. Background, Current Process, And Problem Definition
3. Goals, Non-Goals, And Success Metrics
4. User Roles And Stakeholders
5. Usage Scenarios And User Stories
6. Concepts And Glossary
7. Domain Model, Entities, Fields, And Lifecycle
8. Product Positioning And System Boundaries
9. Product Solution And Architecture
10. Key Interaction Rules And Decision Logic
11. Detailed Module Design
12. Permissions, Data Scope, And Role Matrix
13. Audit, Notification, Dependencies, And Recovery
14. Milestones, Scope, Risks, And Rollout
15. Acceptance Criteria And QA Verification

Do not omit sections 5, 11, 12, 13, or 15. These are common failure points in short outputs. User stories, usage scenarios, detailed module design, permissions, audit/dependency/recovery, and acceptance criteria must be explicit sections, not brief bullets hidden inside other sections.

### Minimum Depth Contract

For full product-design mode, each required section must contain domain-specific substance:

- Demand reflection: include user request, visible symptom, first-principles problem, challenged assumptions, at least one alternative path, and the chosen conclusion.
- Problem definition: include current process, root cause, affected roles, frequency or impact, and scope boundary.
- Goals and non-goals: include measurable outcomes where possible and explain why non-goals are excluded.
- Concepts and glossary: define every core noun, owner, boundary, source of truth, and lifecycle relevance.
- User roles and stakeholders: define each role's responsibility, motivation, authority, data scope, operational pressure, and success signal.
- Usage scenarios and user stories: include concrete scenarios for the happy path, exception path, permission-limited path, and operational recovery path. Add user stories in the form role -> action -> value -> acceptance signal. Do not replace this with a generic persona list.
- Domain model: include entities, key fields, relationships, lifecycle states, ownership, data sources, and deterministic rules.
- Product solution: include system boundary, product architecture, solution tradeoffs, and why the chosen path is the minimum sufficient solution.
- Key interaction rules and decision logic: include deterministic validation, branching, conflict handling, feedback timing, disabled states, and rollback or retry rules.
- Detailed module design: for every P0 module, include purpose, entry, list/detail/form fields, operations, validations, states, disabled states, empty/error/no-permission behavior, audit, and acceptance criteria.
- Permissions, data scope, and role matrix: include a table covering role, operation, object scope, data scope, approval requirement, disabled/no-permission state, and audit record.
- Audit, notification, dependencies, and recovery: include read/write ownership, interface dependencies, fallback, notification, rollback, recovery, and consistency handling.
- Milestones, rollout, and acceptance: include P0/P1/P2 rationale, dependencies, rollout, risks, and testable acceptance rows.

Before finalizing, scan the output against this contract. If a section is only 1-2 generic bullets, a generic table, or a decision without fields/rules/states/acceptance, expand it before answering. If the PRD has fewer than 15 required section headings in full-product-design mode, it is incomplete.

For a shareable PRD, each section must contain domain-specific content, not generic placeholder language. Do not leave a diagram section as "shown below" without an actual diagram. If a section is not applicable, write why it is not applicable.

For medium or complex platform PRDs, include Mermaid diagrams in the PRD:

- Concept relationship diagram
- System boundary / layered architecture diagram
- Core flow or sequence diagram
- State machine diagram when lifecycle exists
- Data ownership / source-of-truth diagram when multiple systems exchange data

Keep diagrams compact but meaningful: one diagram answers one question, labels are short and business-readable, arrows are labeled with verbs, and overloaded diagrams should be split. For core concept, boundary, layered, and decision diagrams, a useful diagram usually has 8-14 meaningful nodes; fewer nodes are acceptable only when the domain is genuinely simple.

When the output is intended for tools outside Codex, assume Mermaid may appear as source code only. For each important diagram, provide both the Mermaid block and a short `Diagram Quick Read`. Do not replace diagrams with prose, but make the prose sufficient for review when rendering is unavailable.

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
- First-principles certainty: the solution addresses the underlying problem rather than merely implementing the user's visible workaround.

It should also have high information density: use diagrams instead of tables when relationships matter, tables instead of prose when rows and columns communicate faster, and concise prose only where judgment is needed.

For product experience, a strong PRD should also create interaction certainty: each UI surface should make clear what information the user receives, what decision it supports, what action can close the loop, what fallback exists when data is missing or uncertain, and what ambiguity has been removed through wording, timing, and data choice.
