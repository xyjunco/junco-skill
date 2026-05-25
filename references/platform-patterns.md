# Platform Modeling Patterns

Use these patterns for complex platform or multi-system PRDs. They are abstracted from the provided PRDs and "make a good product" methodology: define the problem, align with the user's thinking path, build a clear model, then make rules and interactions tangible.

All `graph`, `flowchart`, and `stateDiagram` examples in this file use web-safe Mermaid classes. Preserve this style when adapting the patterns.

## Pattern 1: Minimal Kernel And Scenario Extension

Use when a product needs to support multiple business scenarios without turning the core model into a pile of business-specific fields.

Core idea:

- Kernel owns stable nouns, common fields, common states, common actions, and common audit.
- Scenario extensions own scenario-only fields, rules, views, and workflow differences.
- A scenario can add to the kernel, but should not rewrite the kernel's meaning.

Model check:

| Question | Good Signal | Risk Signal |
| --- | --- | --- |
| What belongs in the kernel? | Used by most scenarios and stable over time | Added only for one urgent case |
| What belongs in extensions? | Scenario-only fields or rules | Business fields placed in common tables |
| How does a new scenario onboard? | Add extension metadata and mapping | Change the core model every time |

Diagram template:

```mermaid
graph LR
  Core["Minimal Kernel"] -- "provides" --> CommonFields["Common Fields"]
  Core -- "provides" --> CommonState["Common State"]
  Core -- "provides" --> CommonAction["Common Actions"]
  Scenario["Business Scenario"] -- "extends" --> Extension["Scenario Extension"]
  Extension -- "adds" --> SceneFields["Scenario Fields"]
  Extension -- "adds" --> SceneRules["Scenario Rules"]
  Core -- "carries" --> Task["Specific Object / Task"]
  Extension -- "explains" --> Task

  class Core,CommonFields,CommonState,CommonAction core;
  class Scenario,Extension actor;
  class SceneFields data;
  class SceneRules control;
  class Task runtime;

  classDef actor fill:#FFCC99,stroke:#CC6600,color:#333333;
  classDef core fill:#CCFFFF,stroke:#0066CC,color:#333333;
  classDef runtime fill:#CCFFCC,stroke:#009966,color:#333333;
  classDef control fill:#FFFFCC,stroke:#CC6600,color:#333333;
  classDef data fill:#CCCCFF,stroke:#663399,color:#333333;
  classDef risk fill:#FFCCCC,stroke:#CC3333,color:#333333;
  classDef neutral fill:#FFFFFF,stroke:#999999,color:#333333;
```

## Pattern 2: Business View And Architecture View

Use when one set of resources must support different user mental models.

Core idea:

- Business users often start from business hierarchy, owner, settlement unit, model, service, or task.
- Platform and SRE users often start from resource hierarchy, architecture layer, cluster, component, host, or dependency.
- The product should clarify whether it owns one physical model and multiple views, or multiple models with mapping rules.

View table:

| View | User Question | Typical Nodes | Risk If Missing |
| --- | --- | --- | --- |
| Business view | Who owns this and what business does it affect? | BU, settlement unit, resource group, model, service | Responsibility is unclear |
| Architecture view | Where does it run and what does it depend on? | Layer, component, cluster, host, instance | Troubleshooting is slow |
| Governance view | What is risky, unaudited, or out of policy? | Rule, risk, audit, action | Platform cannot manage at scale |

Diagram template:

```mermaid
graph TD
  Business["Business View"] --> Owner["Business Ownership"]
  Owner --> Object["Business Object"]
  Object --> Instance["Instance / Task"]

  Architecture["Architecture View"] --> Layer["Architecture Layer"]
  Layer --> Component["Component"]
  Component --> Resource["Resource Instance"]

  Object -- "maps to" --> Resource

  class Business,Owner actor;
  class Object,Instance core;
  class Architecture,Layer,Component control;
  class Resource runtime;

  classDef actor fill:#FFCC99,stroke:#CC6600,color:#333333;
  classDef core fill:#CCFFFF,stroke:#0066CC,color:#333333;
  classDef runtime fill:#CCFFCC,stroke:#009966,color:#333333;
  classDef control fill:#FFFFCC,stroke:#CC6600,color:#333333;
  classDef data fill:#CCCCFF,stroke:#663399,color:#333333;
  classDef risk fill:#FFCCCC,stroke:#CC3333,color:#333333;
  classDef neutral fill:#FFFFFF,stroke:#999999,color:#333333;
```

## Pattern 3: Metadata, Control, Runtime

Use when the product must distinguish management configuration from runtime execution.

Core idea:

- Metadata layer answers "what exists, who owns it, what it means".
- Control layer answers "what is allowed, what should happen, what is audited".
- Runtime layer answers "what is executing, what changed, what failed".

Layer table:

| Layer | Owns | Should Not Own |
| --- | --- | --- |
| Metadata | identity, ownership, attributes, relationships | high-frequency runtime state |
| Control | rules, permissions, approvals, policies, audits | raw execution details |
| Runtime | execution, status, measurements, callbacks | source-of-truth business ownership |

Diagram template:

```mermaid
graph TD
  subgraph Metadata["Metadata Layer"]
    Identity["Object Identity"]
    Ownership["Ownership / Owner"]
    Relationship["Relationships"]
  end

  subgraph Control["Control Layer"]
    Permission["Permissions"]
    Rule["Rule"]
    Audit["Audit"]
  end

  subgraph Runtime["Runtime Layer"]
    Execution["Execution Object"]
    Status["Runtime State"]
    Callback["Callback / Result"]
  end

  Metadata --> Control
  Control --> Runtime
  Runtime --> Control

  class Identity,Ownership,Relationship data;
  class Permission,Rule,Audit control;
  class Execution,Status,Callback runtime;

  classDef actor fill:#FFCC99,stroke:#CC6600,color:#333333;
  classDef core fill:#CCFFFF,stroke:#0066CC,color:#333333;
  classDef runtime fill:#CCFFCC,stroke:#009966,color:#333333;
  classDef control fill:#FFFFCC,stroke:#CC6600,color:#333333;
  classDef data fill:#CCCCFF,stroke:#663399,color:#333333;
  classDef risk fill:#FFCCCC,stroke:#CC3333,color:#333333;
  classDef neutral fill:#FFFFFF,stroke:#999999,color:#333333;
```

## Pattern 4: Lifecycle And Operation Matrix

Use when actions depend on object state.

State machine template:

```mermaid
stateDiagram-v2
  [*] --> Draft: "create"
  Draft --> Active: "submit / become effective"
  Active --> Paused: "pause"
  Paused --> Active: "enable"
  Active --> Failed: "execution failed"
  Failed --> Active: "retry succeeded"
  Active --> Archived: "archive"
  Archived --> [*]

  class Draft,Paused control;
  class Active runtime;
  class Failed risk;
  class Archived neutral;

  classDef runtime fill:#CCFFCC,stroke:#009966,color:#333333;
  classDef control fill:#FFFFCC,stroke:#CC6600,color:#333333;
  classDef risk fill:#FFCCCC,stroke:#CC3333,color:#333333;
  classDef neutral fill:#FFFFFF,stroke:#999999,color:#333333;
```

After the state machine, add an operation matrix:

| State | User Meaning | Allowed Actions | Blocked Actions | Audit |
| --- | --- | --- | --- | --- |
| Draft | Not effective yet | Edit, submit, delete | Runtime execution | yes |
| Active | Effective and in use | View, pause, change with confirmation | Unsafe direct deletion | yes |
| Failed | Action did not complete | View error, retry, rollback | Treat as effective | yes |
| Archived | No longer active | View history | Edit, execute | yes |

## Pattern 5: Deterministic Decision Flow

Use when the product must make a decision from rules, data, state, permissions, or dependencies.

Decision flow template:

```mermaid
flowchart TD
  Start["initiate action"] --> Identify["identify object, role, and context"]
  Identify --> Permission{"has permission?"}
  Permission -- "no" --> NoPermission["reject and show reason"]
  Permission -- "yes" --> Validate["validate fields, state, and dependencies"]
  Validate --> Conflict{"conflict exists?"}
  Conflict -- "yes" --> Block["block and show handling guidance"]
  Conflict -- "no" --> Execute["execute action"]
  Execute --> Result{"succeeded?"}
  Result -- "success" --> Success["show success and write audit"]
  Result -- "failure" --> Fail["show failure with retry / rollback entry"]

  class Start,Identify,Execute core;
  class Permission,Validate,Conflict,Result control;
  class Success runtime;
  class NoPermission,Block,Fail risk;

  classDef actor fill:#FFCC99,stroke:#CC6600,color:#333333;
  classDef core fill:#CCFFFF,stroke:#0066CC,color:#333333;
  classDef runtime fill:#CCFFCC,stroke:#009966,color:#333333;
  classDef control fill:#FFFFCC,stroke:#CC6600,color:#333333;
  classDef data fill:#CCCCFF,stroke:#663399,color:#333333;
  classDef risk fill:#FFCCCC,stroke:#CC3333,color:#333333;
  classDef neutral fill:#FFFFFF,stroke:#999999,color:#333333;
```

Decision table:

| Decision Point | Input | Rule | Result | User Feedback |
| --- | --- | --- | --- | --- |
| Permission | role, object scope | user must have action permission | allow / block | show missing permission |
| Validation | fields, state | required, unique, type, range | allow / block | show field-level error |
| Conflict | related objects | no unresolved conflict | allow / block | show conflict source |
| Dependency | downstream system | dependency available or fallback exists | execute / retry / fail | show retry or owner |
