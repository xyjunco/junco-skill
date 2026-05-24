# PRD Template

Use this template for high-quality PRDs. Remove sections that are genuinely irrelevant, but do not skip problem, concept, model, rules, and acceptance thinking. If a section is not applicable, state why.

Expression rule: 能图不表，能表不文. Use concise Mermaid diagrams for relationships, flows, boundaries, states, and decisions; use tables for repeated attributes and rule rows; use prose for rationale and conclusions. Mermaid diagrams should be visually tidy. For `graph`, `flowchart`, and `stateDiagram`, include web-safe `classDef` and `class` statements.

Depth rule: a full PRD must not stop at background, goals, glossary, CRUD bullets, permissions, and phases. It must expose the implementation contract: domain model, decision rules, lifecycle, fields, operations, states, dependencies, exceptions, audit, and acceptance.

## 0. Document Information

| Field | Content |
| --- | --- |
| Title |  |
| Status | Draft / Review / Ready / Deprecated |
| Version |  |
| PM |  |
| Sponsor |  |
| Owner |  |
| RD / FE / QA / Design / Ops |  |
| Related docs |  |

## 1. Background And Problem Definition

### Background

Describe the business, system, operational, or incident context.

### Current Situation

Describe current process, current system, current workaround, and who is involved.

### Core Problems

| Problem | Root Cause | Impact | Evidence / Metric |
| --- | --- | --- | --- |
|  |  |  |  |

### Scope

This PRD solves:

- 

This PRD does not solve:

- 

## 2. Goals And Success Metrics

| Goal Type | Goal | Metric / Verification |
| --- | --- | --- |
| User |  |  |
| System |  |  |
| Business |  |  |
| Delivery |  |  |

## 3. Concepts And Glossary

| Concept | Definition | Example | Boundary / Distinction |
| --- | --- | --- | --- |
|  |  |  |  |

## 4. User Roles And Scenarios

| Role | Profile | Daily Behavior | Need | Risk / Concern | Corresponding Capability |
| --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  |

| Role | Scenario | I want to | So that | Function | Acceptance |
| --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  |

## 5. Product Positioning And System Boundary

### Positioning

Describe what this product/module is in the whole system.

### System Responsibilities

| System | Team | Responsibility | Change In This PRD |
| --- | --- | --- | --- |
|  |  |  |  |

### Boundary

This product owns:

- 

This product reuses:

- 

This product only references:

- 

## 6. Domain Model And Key Rules

### Concept Relationship Diagram

Explain the core nouns and relationships before listing fields. Keep the diagram focused on one question. It should usually contain 8-14 meaningful nodes and show actor, core object, related object, data source, rule/control point, audit, and exception where relevant.

```mermaid
graph LR
  Actor["角色 / Owner"] -- "发起 / 维护" --> Entry["入口 / 场景"]
  Entry -- "操作" --> Core["核心对象"]
  Core -- "关联" --> Related["关联对象"]
  Data["数据源 / SOT"] -- "提供" --> Core
  Core -- "受控于" --> Rule["规则 / 策略"]
  Rule -- "判断" --> Decision{"决策结果"}
  Decision -- "通过" --> Runtime["下游执行 / 生效"]
  Decision -- "阻断" --> Risk["异常 / 风险处理"]
  Core -- "变更产生" --> Audit["审计记录"]

  class Actor actor;
  class Entry,Core,Related core;
  class Data,Audit data;
  class Rule,Decision control;
  class Runtime runtime;
  class Risk risk;

  classDef actor fill:#FFCC99,stroke:#CC6600,color:#333333;
  classDef core fill:#CCFFFF,stroke:#0066CC,color:#333333;
  classDef runtime fill:#CCFFCC,stroke:#009966,color:#333333;
  classDef control fill:#FFFFCC,stroke:#CC6600,color:#333333;
  classDef data fill:#CCCCFF,stroke:#663399,color:#333333;
  classDef risk fill:#FFCCCC,stroke:#CC3333,color:#333333;
  classDef neutral fill:#FFFFFF,stroke:#999999,color:#333333;
```

### Entities

| Entity | Description | Unique ID | Owner | Source Of Truth |
| --- | --- | --- | --- | --- |
|  |  |  |  |  |

### Entity Fields

| Entity | Field | Meaning | Type | Required | Default | Validation | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  |  |  |

### Relationships

| Source Entity | Relationship | Target Entity | Cardinality | Notes |
| --- | --- | --- | --- | --- |
|  |  |  |  |  |

### State Machine

```mermaid
stateDiagram-v2
  [*] --> Draft
  Draft --> Pending: "提交"
  Pending --> Effective: "生效"
  Pending --> Rejected: "驳回"
  Pending --> Failed: "执行失败"
  Failed --> Pending: "重试"
  Effective --> [*]

  class Draft,Pending control;
  class Effective runtime;
  class Rejected neutral;
  class Failed risk;

  classDef runtime fill:#CCFFCC,stroke:#009966,color:#333333;
  classDef control fill:#FFFFCC,stroke:#CC6600,color:#333333;
  classDef risk fill:#FFCCCC,stroke:#CC3333,color:#333333;
  classDef neutral fill:#FFFFFF,stroke:#999999,color:#333333;
```

| Current State | Action | Next State | Actor | Validation | User Feedback |
| --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  |

### Key Rules

- 

## 7. Product Solution Overview

### System Boundary / Layered Architecture

Use this diagram to show ownership and dependency boundaries, not every implementation detail.

```mermaid
graph LR
  subgraph Users["用户与角色"]
    UserA["角色 A"]
    UserB["角色 B"]
  end

  subgraph Product["本产品"]
    View["视图 / 入口"]
    Manage["管理能力"]
    Rule["规则 / 管控"]
    Audit["审计 / 通知"]
  end

  subgraph Upstream["上游数据源"]
    Meta["元数据"]
    Permission["权限 / 归属"]
  end

  subgraph Downstream["下游系统"]
    Runtime["运行系统"]
    Workflow["审批 / 工单"]
  end

  UserA -- "查看 / 操作" --> View
  UserB -- "维护 / 审批" --> Manage
  View --> Manage
  Manage --> Rule
  Rule --> Audit
  Meta -- "提供对象数据" --> Product
  Permission -- "提供权限范围" --> Product
  Product -- "调用 / 写入" --> Runtime
  Product -- "创建 / 回调" --> Workflow

  class UserA,UserB actor;
  class View,Manage core;
  class Rule,Audit control;
  class Meta,Permission data;
  class Runtime,Workflow runtime;

  classDef actor fill:#FFCC99,stroke:#CC6600,color:#333333;
  classDef core fill:#CCFFFF,stroke:#0066CC,color:#333333;
  classDef runtime fill:#CCFFCC,stroke:#009966,color:#333333;
  classDef control fill:#FFFFCC,stroke:#CC6600,color:#333333;
  classDef data fill:#CCCCFF,stroke:#663399,color:#333333;
  classDef risk fill:#FFCCCC,stroke:#CC3333,color:#333333;
  classDef neutral fill:#FFFFFF,stroke:#999999,color:#333333;
```

### Information Architecture

Describe modules, navigation, and entry points.

### Core Flow

Describe the main user flow and system flow. Prefer a sequence diagram or flowchart over prose when order, branching, or responsibility matters.

```mermaid
sequenceDiagram
  participant User as "用户"
  participant Product as "本产品"
  participant External as "外部系统"
  User->>Product: "发起操作"
  Product->>Product: "校验权限和规则"
  Product->>External: "调用外部能力"
  External-->>Product: "返回结果"
  Product-->>User: "反馈结果"
```

### Solution Tradeoffs

| Solution | Description | Pros | Cons | Risks | Conclusion |
| --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  |

## 8. Detailed Module Design

Repeat this section for each module.

### Module: [Name]

#### Positioning

What this module solves and who uses it.

#### Entry

Where users enter from, and what context is carried.

#### Page / Layout

Describe major areas and information priority.

#### Data Display Contract

| Area | Field / Content | Source | Sort / Filter | Empty / Error Behavior | Permission |
| --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  |

#### Fields

| Field | Meaning | Type | Source | Required | Default | Validation | Permission / State | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  |  |  |  |

#### Operations

| Operation | Entry | Preconditions | Flow | Success Feedback | Failure Feedback | Audit | Permission |
| --- | --- | --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  |  |  |

#### Operation Rules

| Rule | Trigger | System Judgment | User Feedback | Audit / Notification |
| --- | --- | --- | --- | --- |
|  |  |  |  |  |

#### States And Exceptions

| State / Exception | Trigger | UI Behavior | System Behavior | Notes |
| --- | --- | --- | --- | --- |
| Empty |  |  |  |  |
| Loading |  |  |  |  |
| No permission |  |  |  |  |
| Validation failed |  |  |  |  |
| Dependency unavailable |  |  |  |  |

## 9. Permissions, Audit, Data, And Dependencies

### Permission Matrix

| Function | Role A | Role B | Role C | Notes |
| --- | --- | --- | --- | --- |
| View |  |  |  |  |
| Create |  |  |  |  |
| Edit |  |  |  |  |
| Delete |  |  |  |  |
| Approve |  |  |  |  |

### Audit

Audit must record:

- Actor
- Time
- Object
- Operation type
- Before value
- After value
- Reason
- Related ticket / task / rule

### Data And Interfaces

| Data / Interface | Provider | Consumer | Sync Method | Consistency Requirement | Fallback |
| --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  |

## 10. Milestones And Priority

### Priority

| Priority | Function | Reason | Dependency |
| --- | --- | --- | --- |
| P0 |  |  |  |
| P1 |  |  |  |
| P2 |  |  |  |

### Milestones

| Milestone | Product Goal | Scope | Dependency | Delivery Result |
| --- | --- | --- | --- | --- |
| M1 |  |  |  |  |
| M2 |  |  |  |  |
| M3 |  |  |  |  |

## 11. Risks, TODOs, And Open Questions

| Type | Item | Impact | Owner | Due Date | Status |
| --- | --- | --- | --- | --- | --- |
| Risk |  |  |  |  |  |
| TODO |  |  |  |  |  |
| Open question |  |  |  |  |  |

## 12. Acceptance Criteria

| Scenario | Preconditions | Operation | Expected Result | Verification |
| --- | --- | --- | --- | --- |
|  |  |  |  |  |
