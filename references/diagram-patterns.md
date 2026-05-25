# Mermaid Diagram Patterns For Junco PRDs

Use diagrams to express concept relationships, system boundaries, flows, and rules. The goal is not decoration. A diagram should reduce ambiguity faster than prose.

Use the expression priority: 能图不表，能表不文.

1. Use diagrams for relationships, ownership, system boundaries, layers, lifecycle, decisions, and flows.
2. Use tables for fields, permissions, validations, rule rows, priorities, milestones, and acceptance criteria.
3. Use prose for rationale, tradeoffs, context, exception explanation, and conclusions.

If a table is mainly describing "who relates to whom" or "what happens next", convert it to a diagram. If prose is mainly listing repeated rows, convert it to a table.

## Web-Safe Palette

Use web-safe colors when styling Mermaid diagrams. Keep color usage semantic and restrained. For generated PRDs, web-safe styling is mandatory for `graph`, `flowchart`, and `stateDiagram` diagrams. Use color to encode meaning, not decoration.

| Class | Use | Fill | Stroke | Text |
| --- | --- | --- | --- | --- |
| `actor` | Users, teams, roles | `#FFCC99` | `#CC6600` | `#333333` |
| `core` | Core product concepts | `#CCFFFF` | `#0066CC` | `#333333` |
| `runtime` | Runtime services or active execution | `#CCFFCC` | `#009966` | `#333333` |
| `control` | Rules, approvals, control plane | `#FFFFCC` | `#CC6600` | `#333333` |
| `data` | Metadata, source of truth, records | `#CCCCFF` | `#663399` | `#333333` |
| `risk` | Failure, block, alert, deletion, danger | `#FFCCCC` | `#CC3333` | `#333333` |
| `neutral` | External or reference-only nodes | `#FFFFFF` | `#999999` | `#333333` |

Recommended class definitions:

```mermaid
graph LR
  User["用户"] --> Product["核心产品"]
  Product --> Data["数据源"]
  Product --> Rule["规则"]
  Product --> Risk["风险"]

  class User actor;
  class Product core;
  class Data data;
  class Rule control;
  class Risk risk;

  classDef actor fill:#FFCC99,stroke:#CC6600,color:#333333;
  classDef core fill:#CCFFFF,stroke:#0066CC,color:#333333;
  classDef runtime fill:#CCFFCC,stroke:#009966,color:#333333;
  classDef control fill:#FFFFCC,stroke:#CC6600,color:#333333;
  classDef data fill:#CCCCFF,stroke:#663399,color:#333333;
  classDef risk fill:#FFCCCC,stroke:#CC3333,color:#333333;
  classDef neutral fill:#FFFFFF,stroke:#999999,color:#333333;
```

## Diagram Selection

| Need | Use | Answers |
| --- | --- | --- |
| Clarify core nouns and relationships | `graph LR` concept relationship diagram | What concepts exist? Who owns what? What maps to what? |
| Explain product position in a larger system | `graph LR` system boundary diagram | What does this product own, reuse, or call? |
| Explain layered platform design | `graph TD` or `graph LR` layered architecture | What belongs to metadata, control plane, runtime, delivery? |
| Explain time-ordered interactions | `sequenceDiagram` | Who calls whom, in what order, and where are writes/reads? |
| Explain user or system decision flow | `flowchart TD` | What happens next under each condition? |
| Explain lifecycle and allowed operations | `stateDiagram-v2` | What states exist and which actions move between them? |
| Explain entities, keys, and cardinality | `erDiagram` | What are the entities and relationship cardinalities? |
| Explain business / architecture view tree | `graph TD` | How does the user navigate from high-level business to resources? |

## Mermaid Rules

- Prefer one clear diagram per question. Do not put every detail into one huge diagram.
- Avoid toy diagrams. A core PRD diagram should usually contain 8-14 meaningful nodes and cover at least three semantic classes such as actor, core, data, control, runtime, and risk.
- Keep diagrams concise. Split into multiple diagrams when relationships, flow, and state compete for space, or when a graph grows beyond roughly 16 meaningful nodes.
- Keep the visual layout tidy: use one dominant direction, group related nodes with `subgraph`, avoid long crossing arrows, and keep labels similar in length.
- Keep node labels business-readable. Use product nouns, not implementation-only variable names unless the PRD is API-facing.
- Quote labels with Chinese text or punctuation: `A["业务对象"]`.
- Label edges with verbs: `-- "申请" -->`, `-- "归属到" -->`, `-- "调用" -->`.
- Separate management-side concepts from runtime-side concepts.
- Use subgraphs for layers, ownership boundaries, or systems.
- Add a short paragraph before each diagram explaining what the reader should learn.
- Add tables after diagrams for fields, permissions, validations, and exceptions.
- For `graph`, `flowchart`, and `stateDiagram`, always add `classDef` and `class` statements from the web-safe palette. Do not output default monochrome diagrams.
- For `sequenceDiagram` and `erDiagram`, use clear participant/entity grouping; if renderer styling is limited, pair the sequence or ERD with a colored concept, boundary, or decision diagram when color semantics matter.
- Never leave a diagram placeholder. If the PRD says "relationship is shown below", include the Mermaid diagram immediately below it.

## Pattern 1: Concept Relationship Diagram

Use this after concept definitions and before detailed functions. It should make the domain model visible.

```mermaid
graph LR
  User["业务用户"] -- "发起" --> Request["业务请求"]
  Request -- "作用于" --> CoreObject["核心对象"]
  CoreObject -- "关联" --> Resource["关联资源"]
  CoreObject -- "归属到" --> Owner["责任主体"]
  Owner -- "受控于" --> Policy["规则策略"]
  Policy -- "判断" --> Decision{"处理结果"}
  Decision -- "通过" --> Runtime["执行系统"]
  Decision -- "阻断" --> Exception["异常处理"]
  CoreObject -- "变更产生" --> Audit["审计记录"]
  DataSource["数据源"] -- "提供事实" --> CoreObject

  class User actor;
  class Request,CoreObject,Resource core;
  class Owner,DataSource,Audit data;
  class Policy,Decision control;
  class Runtime runtime;
  class Exception risk;
  class Audit data;

  classDef actor fill:#FFCC99,stroke:#CC6600,color:#333333;
  classDef core fill:#CCFFFF,stroke:#0066CC,color:#333333;
  classDef runtime fill:#CCFFCC,stroke:#009966,color:#333333;
  classDef control fill:#FFFFCC,stroke:#CC6600,color:#333333;
  classDef data fill:#CCCCFF,stroke:#663399,color:#333333;
  classDef risk fill:#FFCCCC,stroke:#CC3333,color:#333333;
  classDef neutral fill:#FFFFFF,stroke:#999999,color:#333333;
```

When adapting:

- Replace nouns with the real product concepts.
- Show ownership and source-of-truth relationships.
- Show runtime relationships separately from management relationships when they differ.

## Pattern 2: System Boundary Diagram

Use this when a PRD depends on multiple systems or needs to clarify what the product owns.

```mermaid
graph LR
  subgraph Users["用户与角色"]
    BusinessUser["业务用户"]
    Operator["运营 / 管理员"]
    PlatformOwner["平台负责人"]
  end

  subgraph Product["本产品"]
    Overview["总览"]
    Request["申请 / 配置"]
    Rule["规则判断"]
    Execution["执行编排"]
    Audit["审计"]
  end

  subgraph Upstream["上游数据源"]
    Directory["组织 / 权限目录"]
    Inventory["对象 / 资源清单"]
  end

  subgraph Downstream["下游协作系统"]
    Workflow["审批 / 工单系统"]
    Runtime["执行系统"]
    Notify["通知系统"]
  end

  BusinessUser -- "查看 / 申请 / 操作" --> Product
  Operator -- "处理 / 维护" --> Product
  PlatformOwner -- "配置规则 / 治理" --> Product
  Product -- "读取身份与权限" --> Directory
  Product -- "读取对象事实" --> Inventory
  Product -- "创建 / 回调" --> Workflow
  Product -- "触发执行" --> Runtime
  Product -- "发送结果" --> Notify

  class BusinessUser,Operator,PlatformOwner actor;
  class Overview,Request,Execution core;
  class Rule,Audit control;
  class Directory,Inventory data;
  class Workflow,Runtime,Notify runtime;

  classDef actor fill:#FFCC99,stroke:#CC6600,color:#333333;
  classDef core fill:#CCFFFF,stroke:#0066CC,color:#333333;
  classDef runtime fill:#CCFFCC,stroke:#009966,color:#333333;
  classDef control fill:#FFFFCC,stroke:#CC6600,color:#333333;
  classDef data fill:#CCCCFF,stroke:#663399,color:#333333;
  classDef risk fill:#FFCCCC,stroke:#CC3333,color:#333333;
  classDef neutral fill:#FFFFFF,stroke:#999999,color:#333333;
```

## Pattern 3: Layered Architecture Diagram

Use this for platform products, especially when separating metadata, control, and runtime.

```mermaid
graph TD
  subgraph Runtime["运行层"]
    UserAction["用户操作"]
    Worker["后台任务"]
    TargetSystem["目标系统"]
  end

  subgraph Control["控制面"]
    Management["管理服务"]
    Admission["准入校验"]
    Policy["规则策略"]
    Audit["审计"]
  end

  subgraph Metadata["元数据层"]
    ObjectMeta["对象元数据"]
    Permission["权限 / 归属"]
  end

  ObjectMeta --> Management
  Permission --> Management
  UserAction --> Admission
  Admission --> Management
  Management --> Policy
  Management --> TargetSystem
  Worker --> TargetSystem
  Management --> Audit

  class UserAction,Worker,TargetSystem runtime;
  class Management,Admission,Policy,Audit control;
  class ObjectMeta,Permission data;

  classDef actor fill:#FFCC99,stroke:#CC6600,color:#333333;
  classDef core fill:#CCFFFF,stroke:#0066CC,color:#333333;
  classDef runtime fill:#CCFFCC,stroke:#009966,color:#333333;
  classDef control fill:#FFFFCC,stroke:#CC6600,color:#333333;
  classDef data fill:#CCCCFF,stroke:#663399,color:#333333;
  classDef risk fill:#FFCCCC,stroke:#CC3333,color:#333333;
  classDef neutral fill:#FFFFFF,stroke:#999999,color:#333333;
```

Good layered diagrams show why a concept belongs in a layer. If a node could sit in two layers, clarify ownership in text.

## Pattern 4: Sequence Diagram

Use this for write paths, read paths, approval paths, task submission, config publish, or any flow where order matters.

```mermaid
sequenceDiagram
  participant User as "业务用户"
  participant Product as "本产品"
  participant Workflow as "审批 / 工单系统"
  participant Runtime as "执行系统"
  participant Audit as "审计"

  User->>Product: "提交业务请求"
  Product->>Product: "校验对象、规则、权限"
  Product->>Workflow: "创建审批或处理单"
  Workflow-->>Product: "审批通过"
  Product->>Runtime: "触发执行"
  Runtime-->>Product: "返回结果"
  Product->>Audit: "记录变更前后值和原因"
  Product-->>User: "反馈处理结果"
```

Use `alt` for branching:

```mermaid
sequenceDiagram
  participant Caller as "调用方"
  participant Rule as "规则服务"
  participant Resource as "资源系统"

  Caller->>Rule: "提交准入校验"
  Rule->>Resource: "查询资源状态"
  Resource-->>Rule: "返回当前状态"
  alt "满足规则"
    Rule-->>Caller: "通过 + 下一步"
  else "触发提醒"
    Rule-->>Caller: "有条件通过 + 提示"
  else "不满足规则"
    Rule-->>Caller: "阻断 + 处理入口"
  end
```

## Pattern 5: State Machine

Use this when actions depend on status. PRD text should map each state to visible operations.

```mermaid
stateDiagram-v2
  [*] --> Draft: "创建申请"
  Draft --> PendingApproval: "提交"
  PendingApproval --> Approved: "审批通过"
  PendingApproval --> Rejected: "审批驳回"
  Approved --> Effective: "执行成功"
  Approved --> Failed: "执行失败"
  Failed --> Approved: "重试"
  Effective --> [*]
  Rejected --> [*]

  class Draft,PendingApproval control;
  class Approved,Effective runtime;
  class Failed risk;
  class Rejected neutral;

  classDef runtime fill:#CCFFCC,stroke:#009966,color:#333333;
  classDef control fill:#FFFFCC,stroke:#CC6600,color:#333333;
  classDef risk fill:#FFCCCC,stroke:#CC3333,color:#333333;
  classDef neutral fill:#FFFFFF,stroke:#999999,color:#333333;
```

After the diagram, add an operations table:

| State | Visible Actions | Hidden Actions | Audit |
| --- | --- | --- | --- |
| PendingApproval | Cancel / View | BPM callback | yes |

## Pattern 6: Business View And Architecture View Tree

Use this when the same objects need to support different mental models, such as business ownership, operational responsibility, architecture hierarchy, or resource topology.

```mermaid
graph TD
  Business["业务视图"] --> BU["预算单元"]
  BU --> Team["团队"]
  Team --> ProductLine["产品线"]
  ProductLine --> ObjectGroup["对象分组"]
  ObjectGroup --> BusinessObject["业务对象"]

  Architecture["架构视图"] --> IaaS["IaaS 层"]
  Architecture --> PaaS["PaaS 层"]
  Architecture --> SaaS["SaaS 层"]
  IaaS --> Host["基础资源"]
  IaaS --> Network["网络资源"]
  PaaS --> Service["平台服务"]
  PaaS --> Storage["存储 / 数据服务"]
  SaaS --> Application["业务应用"]
  SaaS --> Task["业务任务"]

  class Business,BU,Team,ProductLine actor;
  class ObjectGroup,BusinessObject,Application,Task core;
  class Architecture,IaaS,PaaS,SaaS control;
  class Host,Network,Service,Storage runtime;

  classDef actor fill:#FFCC99,stroke:#CC6600,color:#333333;
  classDef core fill:#CCFFFF,stroke:#0066CC,color:#333333;
  classDef runtime fill:#CCFFCC,stroke:#009966,color:#333333;
  classDef control fill:#FFFFCC,stroke:#CC6600,color:#333333;
  classDef data fill:#CCCCFF,stroke:#663399,color:#333333;
  classDef risk fill:#FFCCCC,stroke:#CC3333,color:#333333;
  classDef neutral fill:#FFFFFF,stroke:#999999,color:#333333;
```

Use a view tree when the same data needs to support different mental models.

## Pattern 7: Core Decision Flow

Use this for validations, admission checks, approval decisions, fallback logic, or rule matching.

```mermaid
flowchart TD
  Start["提交请求"] --> Identify["识别对象与归属"]
  Identify --> HasPolicy{"是否存在适用规则？"}
  HasPolicy -- "否" --> RejectNoPolicy["阻断：缺少规则配置"]
  HasPolicy -- "是" --> Query["查询对象状态和资源条件"]
  Query --> Allowed{"是否满足执行条件？"}
  Allowed -- "满足" --> Pass["通过并返回下一步"]
  Allowed -- "需提醒" --> Warn["有条件通过并提示"]
  Allowed -- "不满足" --> Block["阻断并给出处理入口"]

  class Start,Identify core;
  class HasPolicy,Allowed control;
  class Query data;
  class Pass runtime;
  class Warn,Block,RejectNoPolicy risk;

  classDef actor fill:#FFCC99,stroke:#CC6600,color:#333333;
  classDef core fill:#CCFFFF,stroke:#0066CC,color:#333333;
  classDef runtime fill:#CCFFCC,stroke:#009966,color:#333333;
  classDef control fill:#FFFFCC,stroke:#CC6600,color:#333333;
  classDef data fill:#CCCCFF,stroke:#663399,color:#333333;
  classDef risk fill:#FFCCCC,stroke:#CC3333,color:#333333;
  classDef neutral fill:#FFFFFF,stroke:#999999,color:#333333;
```

## PRD Diagram Checklist

For complex PRDs, include at least:

- One concept relationship diagram.
- One system boundary or layered architecture diagram.
- One sequence or flowchart for the core path.
- One state machine if there is lifecycle or workflow state.
- One source-of-truth / data flow diagram if multiple systems write or read the same domain data.

Avoid:

- Diagrams that duplicate tables without adding relationships.
- Mixing user journey, data flow, state machine, and architecture into one unreadable graph.
- Unlabeled arrows.
- Missing ownership boundaries.
