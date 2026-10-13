# PRD Review Checklist

Apply relevant checks to the requested scope. A passing PRD has clear business behavior and verifiable rules; it need not reproduce every template heading.

## Context, Work, And Scope

- Current project context, source PRD, latest decisions, user sample style, and destination have been read. Sources have been checked for the same project, object, scope, and time; reference examples and unrelated history have not become current facts.
- Work problem, role, cadence, volume, pain, impact, and success signal are concrete.
- The proposed feature/path has been tested against simpler solutions, while confirmed business boundaries remain valid.
- Real work needs, prototype feedback, writing instructions, and assistant proposals are separated; inferred needs are identified.
- Active scope and adjacent responsibility are clear; withdrawn flows have been removed from all affected current artifacts.
- Role merges preserve responsibility, data scope, approval, notifications, and stories.

## Objects, Rules, And Effects

- Core nouns have meaning, ownership, source of truth, relationships, cardinality, and lifecycle.
- Business objects and underlying implementation/physical objects are distinguished.
- Saved configuration, proposed change, submitted request, executed result, acknowledgment, and current state have distinct effects where applicable.
- States have actual sources, entry/exit conditions, available actions, and meaningful display semantics.
- Rules cover deterministic validation, conflicts, precedence, versions, idempotency, permissions, and audit as relevant.
- Exceptions are justified by the product contract; template examples have not become invented business states.
- Model and term changes propagate to prose, fields, calculations, actions, histories, permissions, figures, and acceptance.

## Data And Metrics

- Each metric supports a role's decision and has source, object, population, unit, time/version, formula, deduplication, precision, and update timing.
- Original, transformed, planned, actual, cumulative, and current-state quantities have explicit relationships.
- Business formulas use verified source-field names and mappings; engineering symbols are defined separately where needed. Undefined numerators/denominators have not been inferred from nearby nouns or examples.
- Comparison population, displayed subset, and modified/executed set are distinct; filter, Tab, selection, and pagination behavior is explicit.
- Nonparticipation, numerical zero, missing facts, empty data, and operational failure have distinct semantics.
- Normal examples are complete, coherent, and reconciled across lists, details, charts, totals, and rates; illustrative data is not presented as production truth.
- Thresholds are sourced and tested with full precision; percentage-point differences are expressed accurately.
- Genuine data gaps are visible decisions; a tooling failure has not been inserted as a product-data state.

## Scenarios, Pages, And Batch

- Role-action-value-acceptance stories cover actual main work and relevant permission, exception, and recovery paths.
- Each surface has a decision or useful information task, required context, clear primary action, and completion/return path.
- Existing context is carried forward; repeated selection, explanation-only steps, and redundant result pages are removed.
- Fields, operations, visibility, defaults, validation, state constraints, outcomes, and audit are specified where they affect behavior.
- Batch input fits cadence and volume; whole-batch validation, cross-row constraints, correction, exact submission scope, duplicate handling, and results are defined.
- Confirmation follows actual consequence and reversibility. It adds a necessary decision instead of repeating a sufficient preview.
- Action guidance, static evidence, pre/post impact, exceptions, and history have distinct roles.
- Same-group fields align; duplicate metadata has one canonical definition; status and auxiliary actions stay with their object.
- Default view appears first. Charts serve quantitative patterns; tables serve exact lookup and execution. Dimension views show the selected dimension with consistent scale and reconcilable totals.
- Visual simplification preserves original decision information, using hierarchy and drill-down rather than deleting core metrics.

## Permissions, Dependencies, And Delivery

- Permissions name role, action/state, object/data scope, approval/prerequisite, no-permission behavior, and audit.
- Interfaces identify provider/consumer, read/write truth, timing, consistency, version, and relevant failure/recovery behavior.
- Risk handling exposes affected objects, consequences, required choices, and recovery; risk is not inferred from an action name alone.
- Priorities reflect closure, risk, dependency, and cost.
- Milestones have specific usable capability, dated window/cutoff, deliverable, acceptance signal, actual dependency, owner, and date basis.
- Independent work streams proceed in parallel; dependencies constrain specific nodes rather than serializing every stream.
- Roadmap agrees with milestone dates, durations, overlap, and acceptance. Proposed schedule is distinguished from a staffed commitment.
- Acceptance checks observable main paths, permissions, validation, dependency failure, recovery, audit, and data consistency.

## Writing, Format, And Maintenance

- Prose describes object responsibility, actions, rules, and results, rather than repeating prompt or review instructions.
- Necessary exclusions remain accurate; long repeated negative constructions have been rewritten positively.
- User sample voice, short sentences, stable terms, meaningful headings, and exact action copy are preserved.
- Chinese/English, numbers/units, punctuation, and date formats follow the document convention; IDs and code identifiers stay intact.
- Ordinary prose/data retain normal weight; emphasis and color are local and semantic. Rich-text fonts, links, indentation, and adjacent content are preserved.
- Diagram, table, chart, or prose is chosen by the information task and requested destination, rather than a blanket preference.
- Figures answer one question and agree with models/rules. Native or Mermaid rendering is verified; source-only output is identified honestly.
- Open business decisions are consolidated with source, impact, owner, and next step; routine UI copy carries no process-label prefix.
- WIP debris, duplicate explanations, outdated alternatives, empty placeholders, and withdrawn features are absent from the current solution.
- Remote edits use the relevant skill and current native structure. Unknown write results are read back before retries; concurrent edits and user deletions are preserved.
- Affected text, structures, links, images/boards, and rendered layout are verified. Static, runtime, and user-acceptance evidence are reported separately.

## Common Failure Signals

- A full PRD replaced by a capability outline, or a scoped edit expanded into an unrelated full rewrite.
- Reviewer demands treated as user research, or proposals described as implemented facts.
- Familiar old fields retained after the object model changes.
- Submitted or saved quantities counted as actual execution.
- Incomplete normal examples filled with source-error placeholders.
- Pagination or selection silently shrinking a global calculation or batch execution.
- A high-volume batch task implemented as repeated single-item forms.
- Decorative charts/cards, dense scattered facts, or whitespace changes that discard required information.
- Identical long date bars masquerading as detailed milestones.
- Text-only replacement claimed as full logic/visual verification.
