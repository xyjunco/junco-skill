---
name: junco
description: First-principles product design, domain modeling, and PRD writing. Use to turn raw needs, operational pain, platform ideas, or product feedback into clear problems, user paths, concepts, ownership, rules, page content, flows, milestones, and acceptance criteria. Also use to review or revise existing PRDs, write Chinese 产品方案 in the user's established style, clarify metrics and batch workflows, or maintain product logic across documents and prototypes. Requires the humanizer skill to polish copy before writing documents or diagrams. Preserve the requested scope and distinguish confirmed facts, proposed design, open decisions, and verified delivery.
---

# Junco

## Overview

Solve a real problem with the minimum sufficient cost. Recover the user's thinking path, abstract a clean model, define the product's operating rules, then express them through flows, page content, and a reviewable PRD. The purpose is product design quality rather than filling a template.

Use the user's language. Read the current project context, latest decisions, source PRD, and requested destination before drafting. Treat an implementation request as a possible solution while preserving business boundaries that the user has already confirmed.

Write the PRD for the people who use and build the product: who does what, under which conditions, and what happens afterward. Keep working analysis, coverage matrices, tool checks, and design-review history separate from the reader-facing document. Completeness is not a reason to publish every internal checklist.

For Chinese `产品方案`, page/module specifications, or PRD rewrites in the user's style, read `references/prd-product-solution-writing-style.md` completely. For writing, reviewing, or revising a PRD, also read `references/prd-writing-lessons.md`. These govern expression after the sequence problem -> model -> rules -> pages.

Choose the form by the reader's task: relationships and flow need diagrams; repeated rules and executable items need tables; trends and distributions need charts; rationale needs concise prose. An existing document's structure, the user's explicit format, and native capabilities of the destination take priority.

Use target-native editable diagrams when supported. Use Mermaid when it suits the host; load `references/diagram-patterns.md` for its style conventions. Verify actual rendering before claiming a preview. If rendering is unavailable, supply valid source with a short reading guide; publish rendered assets or native figures when the destination supports them. Node count is not a quality target: include the objects and control points needed to answer the diagram's question.

## Required Humanizer pass

- `humanizer` is a required companion skill. Resolve it from the available-skills catalog and read its `SKILL.md`; use the installed location rather than a personal absolute path.
- Before writing or revising a document, or creating or updating a diagram, apply `$humanizer` to the current copy. Cover body text, headings, tables, captions, and diagram labels before writing or rendering them. Review affected copy again when it changes.
- Follow Humanizer's draft, audit, and final-rewrite process. Keep product facts, permissions, scope, enums, IDs, formulas, and relationships intact. Keep the working audit out of the delivered body unless requested.
- Organize body content into short, meaningful points. Use two-level lists for grouped rules, ordered lists for steps, and tables for comparisons. Humanizer improves wording while preserving this structure; it should not merge useful points into long paragraphs or add filler labels to every bullet.
- If Humanizer is unavailable, report the missing dependency. Continue independent analysis where useful, then resume writing or drawing once it is available. Claim the pass only after completing it.

## PRD Writing And Revision Standards

- **Source and role:** distinguish real work needs from review feedback, UI choices, writing instructions, and assistant proposals. Record role, task, frequency, scale, pain, and desired outcome; identify synthesized needs rather than presenting them as interview quotes.
- **Product semantics:** write what the object means, what the user does, and how the system responds. Turn feedback into positive responsibility and action rules. Keep necessary exclusions, permissions, and risk constraints; avoid copying prompt rules into the PRD or product UI.
- **Evidence and uncertainty:** keep confirmed facts, proposed design, and unresolved business decisions distinguishable. Put blocking decisions in one decision table with owner, impact, and next step. Authorized routine layout and copy can be written directly as the proposed solution, without attaching `建议文案` to every control. Product pages use actual user-facing copy.
- **Model and data:** distinguish planned, saved, submitted, executed, acknowledged, and current-state quantities. Define field source, scope, unit, time, version, and formula. Comparison population, visible subset, and modification set are separate contracts.
- **Examples and copy:** prototypes use complete, coherent representative data. PRD examples and exact copy belong where they clarify behavior or are explicitly required. Apply the required Humanizer pass before document or diagram output. Genuine source gaps remain open decisions. A tool failure is not a business state.
- **Scale and action:** choose the workflow from real volume and cadence. Define batch input, full-batch validation, correction, submission scope, idempotency, result, and return path. Add a page or confirmation only when it serves a distinct decision or material consequence.
- **Information and visual meaning:** separate immediate action guidance from static evidence and history. Group values by object and meaning, align before/after comparisons, place status with its object, and use semantic emphasis. Visual simplification retains the original information needed for decisions.
- **Delivery and revision:** propagate changes to affected prose, tables, captions, diagrams, prototypes, permissions, examples, and acceptance rules. Review their shared product meaning, including copy-only and screenshot updates; see `references/prd-writing-lessons.md` sections 2 and 8. Preserve withdrawn scope. Iteration milestones describe functional scope and user outcomes; a detailed execution schedule adds supported dates, owners, dependencies, and exit criteria when requested.
- **Readable revision:** group rules before editing bullets. Keep page behavior, iteration scope, and implementation detail at their own levels. Write body content as short points with familiar business nouns, useful list hierarchy, native editable blocks, and sparse emphasis. Bold does not imply blue; follow the document's link/navigation color convention. See `references/prd-writing-lessons.md` for density repair and native maintenance.

Project-specific objects, role counts, thresholds, color values, terminology, and batch sizes belong to that project's contract. The worked examples in the references illustrate methods; they are not global defaults.

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
   - Choose the representation that carries the logic: diagrams for relationships and flows, tables for repeated rules and exact items, charts for quantitative patterns, and concise prose for judgment. User-requested forms and the destination take precedence over a blanket hierarchy.

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
   - For a new full PRD, include concise design reasoning in the appropriate context section: request, symptom, root problem, challenged assumptions, alternatives, and chosen conclusion. In a scoped revision, keep this reasoning in the working analysis unless it changes the requested section. Preserve already-confirmed business boundaries.
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

## Product Logic Ownership Audit

Use this audit before designing pages, flows, confirmations, sync jobs, approvals, or exception handling. The goal is to prevent product logic from drifting into the wrong surface: a lightweight save action should not become a heavy conflict-resolution wizard; a runtime synchronization action should not hide material overwrite choices; a user page should not expose PRD reasoning or implementation notes.

1. Name the product objects and their owners.
   - For every core noun, define its responsibility, source of truth, and relationship to adjacent objects. State an exclusion when it resolves an actual ambiguity.
   - Do not let two objects claim the same responsibility unless the relationship is explicit, such as policy -> applied instance, template -> generated item, or scope -> matched objects.
   - If a field or conflict depends on another object, place the decision where that object is changed or materialized.

2. Classify each action by its product effect.
   - Draft/save: stores configuration and should be lightweight unless it writes to live users, money, security, runtime behavior, or irreversible records.
   - Preview: calculates impact and exposes uncertainty before commitment; it should not secretly mutate state.
   - Apply/sync/publish/submit: materializes configuration into downstream objects or runtime behavior; this is where overwrite, skip, conflict, missing data, and retry decisions usually belong.
   - Runtime job: reacts to ongoing data changes after configuration is saved; users usually need history, errors, retry, and audit rather than a blocking wizard every time.
   - Delete/archive: changes ownership or lifecycle; define the handling of dependent objects. Ask for a choice when the product genuinely offers alternatives; otherwise show the established policy and its effect.

3. Put conflict handling at the decision point that creates the conflict.
   - A conflict belongs to the action that changes the contested target.
   - If a save action only defines a scope, then expression syntax and scope impact may be validated there, but downstream variable missing, instance overwrite, or notification failure should not be handled there unless save also materializes those downstream objects.
   - If a sync/apply action writes generated instances, then duplicate target handling, overwrite/ignore, partial failure, retry, and owner notification belong in that flow.
   - If a runtime job later detects additions/removals, expose the job's result in history and recovery surfaces instead of forcing an unrelated edit flow.

4. Separate UI surfaces from PRD and implementation reasoning.
   - User pages should show object identity, current state, impact, available choices, validation errors, and recovery entry points.
   - Product rationale, why a component exists, fallback implementation behavior, hidden audit details, and "what this page demonstrates" belong in PRD, annotations, or acceptance criteria, not in the product UI.
   - If the copy sounds like a reviewer note, implementation comment, or internal mechanism, rewrite it into user language or remove it from the interface.

5. Remove duplicate flows by intent, not by page title.
   - When two pages both answer the same user question, merge them into one canonical flow even if their titles differ.
   - Keep separate pages only when the entry, decision, permission, state source, or recovery path is meaningfully different.
   - If a later design adds pages that overlap an earlier flow, update the earlier flow instead of leaving two competing versions in the prototype or PRD.

6. Match flow weight to risk.
   - Low-risk configuration save: lightweight validation, concise impact preview, simple success/failure feedback, and history link if asynchronous effects exist.
   - Medium-risk materialization: preview affected targets, show skipped/changed/new counts, ask for strategy where user choice matters, then submit.
   - Materially risky operations: expose exact target identity, consequence, required user choice, audit, and recovery. Judge risk by effect and reversibility, rather than names such as bulk, save, or sync. A preview that already supports the final decision can be the submission surface.
   - Do not add steps merely to explain system behavior. Add steps only when the user must make or verify a decision.

7. Define every page by the decision it supports.
   - Before drawing a page, state: entry, user decision, information required, primary action, secondary action, completion state, error state, and where the user goes next.
   - If a page has no user decision and only explains a process, it is probably PRD content, dashboard history, or audit detail rather than an operation page.
   - If a dashboard, list, or detail page exists, define what it helps users perceive quickly: volume, trend, distribution, ownership, priority, progress, anomaly, or recovery.

8. Make state sources explicit.
   - A status label must have a source-of-truth and lifecycle definition.
   - Do not mix states from different systems into one status unless the UI names the source or composes them into a user-meaningful overall state.
   - Color and severity choices should follow the product meaning, not the system that produced the state.

## Workflow

0. **Calibrate scope and evidence.** Determine whether the task is a new full PRD, a scoped section update, a review, a brief, or page-content design. Load the required Humanizer skill for copy work. Read the current document and sample style. Identify confirmed decisions, active proposals, withdrawn scope, and missing facts. For PRD sync, inventory the related text carriers in the affected module using `references/prd-writing-lessons.md` section 8; keep edits within the authorized scope. Ask only for gaps that block dependent work; continue independent modeling. Use `references/prd-depth-rubric.md` for a full PRD or readiness review.

1. **Reframe the problem.** Identify requester, context, workaround, cause, frequency, scale, cost, and success signal. Test a simpler model, rule, data, or process solution when relevant. State goals, scope, and adjacent responsibility. Keep discovery reasoning in its own section or working notes.

2. **Capture the role's work.** Describe daily tasks, decisions, constraints, authority, and desired outcome. Separate these from reviewer preferences and interface prescriptions. If roles merge, reconcile responsibilities, data scopes, approvals, notifications, and stories.

3. **Define concepts and ownership.** Build a glossary of core objects, relationships, source systems, units, lifecycle, and similar concepts. Separate business objects from underlying implementation or physical objects. For a model change, list affected surfaces before editing them.

4. **Build the model and rules.** Define IDs, cardinality, version/history, state truth, deterministic validation, conflict handling, and read/write ownership. Run the Product Logic Ownership Audit. Use `references/platform-patterns.md` for complex platform modeling.

5. **Derive scenarios and stories.** Use role x object x situation. Cover main work, justified exceptions, restricted permissions, and recovery. Connect each story to value and an observable acceptance signal; label inferred needs by source status.

6. **Plan architecture and dependencies.** Define reused and new capabilities, upstream/downstream contracts, and tradeoffs. Diagram only the relationships or sequences that need visual explanation. A business flow's sequence does not imply that development streams must be scheduled serially.

7. **Define page content and copy.** Before drawing, specify entry/context, supported decision, information groups, main action, secondary actions, completion, and return path. Define relevant field sources/units/defaults/validation, action effects, state-dependent operations, and error recovery. Design dashboards around decisions and batch flows around actual volume. Apply Humanizer to the copy before writing the document or drawing labels. Keep body rules in short points and UI copy free of brief, PRD reasoning, and review annotations.

8. **Complete delivery rules.** Specify permissions, dependencies, consistency, and recovery where they affect the product. Split priorities by the first independently usable core path and later improvements, not by feature names. For iteration planning, state each iteration's main functions and user outcome; use internal coverage checks to avoid omissions without copying every field and exception into the milestone table. Add a detailed schedule only at the requested level, with supported dates and actual dependencies.

9. **Review and deliver.** Check terminology, data arithmetic, stages, scope, story coverage, module usability, visual organization, rich-text formatting, and milestones using `references/review-checklist.md`. When editing a remote document, use its relevant skill, patch the current native structure, preserve adjacent content/styles/links, and read back changes. For PRD sync, verify the final version of every inventoried carrier and semantic equivalence of rewritten constraints; identify unread or pending items. For visual changes verify both structure and rendered evidence. Report what is actually verified.

Junco completes requirement abstraction, page content, and copy. Proceed to visual page design or implementation only within the user's requested scope and applicable project workflow. When the project requires Product Design and Arco before Figma, follow those gates; Junco does not replace the destination skills.

## Reference Files

- `references/prd-writing-lessons.md`: required for PRD writing/revision/review; source handling, readable product semantics, metrics, batch scale, information grouping, parallel milestones, native maintenance, and scoped examples.
- `references/prd-product-solution-writing-style.md`: required in full for Chinese page/module specifications; house style, atomic rules, before/after examples, typography, and document structure.
- `references/methodology.md`: deeper first-principles discovery and modeling questions.
- `references/prd-depth-rubric.md`: full-PRD completeness and scoped revision readiness.
- `references/platform-patterns.md`: kernel/extensions, lifecycle governance, views, layers, and ownership.
- `references/diagram-patterns.md`: Mermaid selection and styling when Mermaid is the appropriate format.
- `references/prd-template.md`: adaptable document, role, metric, module, and milestone tables.
- `references/review-checklist.md`: final logic, expression, scope, delivery, and evidence review.

## Output Expectations

### Deliver The Requested Artifact

For a new full PRD, deliver the actual reviewable body with domain-specific behavior and observable outcomes. A section list alone is insufficient. A separate acceptance/test chapter is useful when requested or necessary for the work, not a mandatory way to prove completeness. Without an external target, provide the body in the conversation unless another format is requested. With an external target, write it there and return the important change and an accurate link; report material verification limits briefly.

For an existing PRD or section-only request, preserve its useful outline and update the authorized scope. Complete the dependent rules that the change affects; do not rebuild unrelated chapters merely to match a heading count. For reviews, lead with substantive gaps, their impact, and concrete repairs. For an explicitly requested brief, deliver a brief that retains the important boundaries and dependencies.

### Full PRD Coverage

Use these as coverage areas for a new full PRD, with headings adapted to the user's document:

1. Background, current work, problem, and concise demand reflection.
2. Goals, scope, and measurable success.
3. Roles, work needs, scenarios, and user stories.
4. Concepts, domain model, relationships, source of truth, and lifecycle.
5. Product positioning, system responsibilities, architecture, and tradeoffs.
6. Deterministic rules and detailed page/module solution.
7. Permissions, object/data scope, approvals, audit, and notification.
8. Data/interface dependencies, consistency, exceptions, and recovery.
9. Priorities, milestones, risks, and rollout.
10. Acceptance criteria and verification.

These are coverage questions, not mandatory chapters. Keep relevant scenarios, module rules, permissions, dependencies, recovery, and outcomes easy to locate. Design reasoning can remain in working notes; detailed acceptance can be separate when needed. Completeness is measured by answered product questions, not headings, diagrams, rule counts, or document length. Respect the requested outline and brevity.

### Minimum Depth

- Problem: actual work, root cause, impact, constraints, and chosen solution.
- Roles and stories: responsibility, authority/data scope, cadence/scale, role-action-value-acceptance, and justified exceptional paths.
- Concepts/model: owner, source of truth, cardinality, lifecycle, version, unit, and relationships between related quantities.
- Rules: inputs, scope, precedence, calculation, validation, conflicts, permissions, and effects at each stage.
- P0 modules: purpose, entry/context, relevant list/detail/form fields, closed action chains, state-dependent behavior, audit, and acceptance.
- Metrics: decision served, source, population, unit, time/version, formula, precision, deduplication, update timing, and filter/drill-down relationship.
- Delivery: iteration scope and the user capability it enables; add execution dependencies, supported dates, rollout, risks, and acceptance detail when the assignment needs them.

Use meaningful diagrams for concept relationships, system boundaries, core flows, and lifecycle when needed. Keep one diagram's question clear, label edges, and align source/ownership/states with the written rules. Verify the host's actual render or provide source and a reading guide when unavailable.

## Quality Bar

A reader should know why the problem matters, what each role does, how the objects and rules work, where data comes from, what changes after an action, and how delivery will be verified. Reviewers should locate the rule they need without interpreting prompt instructions or reading a dense paragraph twice.

Treat a written proposal, updated document, static prototype, verified runtime behavior, and user acceptance as distinct evidence levels. Report the level actually reached.
