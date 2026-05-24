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
- Quote labels with Chinese text or punctuation: `A["结算单元"]`.
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
  User["算法 RD"] -- "提交" --> Job["训练任务"]
  Job -- "生成" --> Checkpoint["Checkpoint"]
  Checkpoint -- "写入" --> Path["规范路径"]
  Path -- "归属到" --> ResourceGroup["资源组"]
  ResourceGroup -- "隶属于" --> SettlementUnit["结算单元"]
  SettlementUnit -- "拥有" --> QuotaPool["Quota 池"]
  QuotaPool -- "受控于" --> Watermark["水位规则"]
  QuotaPool -- "变更产生" --> Audit["审计记录"]
  Scheduler["调度平台"] -- "提交前校验" --> Admission["准入校验"]
  Admission -- "读取" --> QuotaPool
  Admission -- "返回 pass / queue / reject" --> Scheduler

  class User actor;
  class Job,Checkpoint,Path core;
  class ResourceGroup,SettlementUnit,QuotaPool data;
  class Watermark,Admission control;
  class Scheduler runtime;
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
    POC["业务 POC"]
    SRE["平台 SRE"]
    RD["算法 RD"]
  end

  subgraph Product["本产品：HDFS Quota 管理"]
    Overview["Quota 总览"]
    Request["Quota 申请"]
    Admission["准入判断"]
    Watermark["水位管理"]
    Audit["审计"]
  end

  subgraph Upstream["上游数据源"]
    CMDB["CMDB：结算单元 / 资源组 / Owner"]
    HDFS["HDFS / QuotaService：容量与 Quota API"]
  end

  subgraph Downstream["下游协作系统"]
    Scheduler["调度平台"]
    BPM["审批系统"]
    Ckpt["Checkpoint 管理"]
  end

  POC -- "申请 / 查看 / 腾挪" --> Product
  SRE -- "配置规则 / 全局治理" --> Product
  RD -- "提交任务时感知结果" --> Scheduler
  Product -- "读取元数据" --> CMDB
  Product -- "查询 / 设置 Quota" --> HDFS
  Scheduler -- "调用准入接口" --> Product
  Product -- "创建审批单" --> BPM
  Product -- "跳转治理" --> Ckpt

  class POC,SRE,RD actor;
  class Overview,Request core;
  class Admission,Watermark,Audit control;
  class CMDB,HDFS data;
  class Scheduler,BPM,Ckpt runtime;

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
    Job["训练任务"]
    Framework["训练框架 / Dump 服务"]
    HDFS["HDFS 存储"]
  end

  subgraph Control["控制面"]
    Quota["Quota 管理服务"]
    Admission["准入校验"]
    Watermark["水位规则"]
    Audit["审计"]
  end

  subgraph Metadata["元数据层"]
    CMDB["结算单元 / 资源组 / Owner"]
    Policy["审批规则 / 权限"]
  end

  CMDB --> Quota
  Policy --> Quota
  Job --> Admission
  Admission --> Quota
  Quota --> Watermark
  Quota --> HDFS
  Framework --> HDFS
  Quota --> Audit

  class Job,Framework,HDFS runtime;
  class Quota,Admission,Watermark,Audit control;
  class CMDB,Policy data;

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
  participant User as "业务 POC"
  participant Product as "Quota 管理"
  participant BPM as "审批系统"
  participant HDFS as "HDFS QuotaService"
  participant Audit as "审计"

  User->>Product: "提交扩容申请"
  Product->>Product: "校验结算单元、容量、权限"
  Product->>BPM: "创建审批单"
  BPM-->>Product: "审批通过"
  Product->>HDFS: "设置新的 Quota"
  HDFS-->>Product: "返回成功"
  Product->>Audit: "记录变更前后值和原因"
  Product-->>User: "扩容生效"
```

Use `alt` for branching:

```mermaid
sequenceDiagram
  participant Scheduler as "调度平台"
  participant Quota as "Quota 管理"
  participant HDFS as "HDFS QuotaService"

  Scheduler->>Quota: "提交准入校验"
  Quota->>HDFS: "查询已用量"
  HDFS-->>Quota: "返回 used / total"
  alt "余量充足"
    Quota-->>Scheduler: "pass + 规范路径"
  else "达到预警线"
    Quota-->>Scheduler: "warn_pass + 提示"
  else "容量不足"
    Quota-->>Scheduler: "queue / reject + 处理入口"
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
  Approved --> Effective: "底层 Quota 设置成功"
  Approved --> Failed: "底层 Quota 设置失败"
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

Use this for CMDB, resource management, quota, topology, or other products where users need different navigation views.

```mermaid
graph TD
  Business["业务视图"] --> BU["预算单元"]
  BU --> Settlement["结算单元"]
  Settlement --> RG["资源组"]
  RG --> Model["模型"]
  Model --> Instance["模型实例"]

  Architecture["架构视图"] --> IaaS["IaaS 层"]
  Architecture --> PaaS["PaaS 层"]
  Architecture --> SaaS["SaaS 层"]
  IaaS --> Server["服务器"]
  IaaS --> Package["套餐"]
  PaaS --> HDFS["HDFS"]
  PaaS --> PS["PS"]
  SaaS --> Job["训练任务"]
  SaaS --> Checkpoint["Checkpoint"]

  class Business,BU,Settlement,RG,Model actor;
  class Instance,Job,Checkpoint core;
  class Architecture,IaaS,PaaS,SaaS control;
  class Server,Package,HDFS,PS runtime;

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
  Start["任务提交"] --> Identify["识别结算单元 / 资源组"]
  Identify --> HasQuota{"是否存在 Quota 池？"}
  HasQuota -- "否" --> RejectNoQuota["拒绝：无 Quota 配置"]
  HasQuota -- "是" --> Query["查询已用量和预留量"]
  Query --> Enough{"预计写入后是否超限？"}
  Enough -- "否" --> Pass["放行并返回规范路径"]
  Enough -- "达到预警线" --> Warn["放行并发送预警"]
  Enough -- "达到熔断线" --> Block["排队或拒绝"]

  class Start,Identify core;
  class HasQuota,Enough control;
  class Query data;
  class Pass runtime;
  class Warn,Block,RejectNoQuota risk;

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
