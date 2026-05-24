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
  Core["最小集内核"] -- "提供" --> CommonFields["通用字段"]
  Core -- "提供" --> CommonState["通用状态"]
  Core -- "提供" --> CommonAction["通用动作"]
  Scenario["业务场景"] -- "扩展" --> Extension["场景扩展"]
  Extension -- "补充" --> SceneFields["场景字段"]
  Extension -- "补充" --> SceneRules["场景规则"]
  Core -- "承载" --> Task["具体对象 / 任务"]
  Extension -- "解释" --> Task

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
  Business["业务视图"] --> Owner["业务归属"]
  Owner --> Object["业务对象"]
  Object --> Instance["实例 / 任务"]

  Architecture["架构视图"] --> Layer["架构层级"]
  Layer --> Component["组件"]
  Component --> Resource["资源实例"]

  Object -- "映射到" --> Resource

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
  subgraph Metadata["元数据层"]
    Identity["对象标识"]
    Ownership["归属 / Owner"]
    Relationship["关联关系"]
  end

  subgraph Control["管控层"]
    Permission["权限"]
    Rule["规则"]
    Audit["审计"]
  end

  subgraph Runtime["运行层"]
    Execution["执行对象"]
    Status["运行状态"]
    Callback["回调 / 结果"]
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
  [*] --> Draft: "创建"
  Draft --> Active: "提交 / 生效"
  Active --> Paused: "停用"
  Paused --> Active: "启用"
  Active --> Failed: "执行失败"
  Failed --> Active: "重试成功"
  Active --> Archived: "归档"
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
  Start["发起动作"] --> Identify["识别对象、角色、上下文"]
  Identify --> Permission{"是否有权限？"}
  Permission -- "否" --> NoPermission["拒绝并提示原因"]
  Permission -- "是" --> Validate["校验字段、状态、依赖"]
  Validate --> Conflict{"是否存在冲突？"}
  Conflict -- "是" --> Block["阻断并展示处理建议"]
  Conflict -- "否" --> Execute["执行动作"]
  Execute --> Result{"是否成功？"}
  Result -- "成功" --> Success["反馈成功并写审计"]
  Result -- "失败" --> Fail["反馈失败并提供重试 / 回滚入口"]

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
