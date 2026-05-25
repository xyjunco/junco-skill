# Junco Skill

Junco is a model-agnostic methodology and reusable skill package for product requirement analysis, product modeling, and high-quality product design.

It helps turn raw needs, vague feature requests, stakeholder feedback, operational pain points, platform/system ideas, or existing PRDs into rigorous product designs with clear problems, concepts, models, flows, rules, milestones, and acceptance criteria. The final delivery artifact is often a PRD, but the purpose is product design quality rather than template completion.

## 中文说明

### 这套方法解决什么问题

Junco 适用于各类大模型和智能体，用于把“想做一个功能”“有个产品想法”“这里体验不好”这类原始需求，转成可评审、可设计、可开发、可验收的产品方案。最终交付物通常是 PRD，但目标是完成高质量产品设计，而不是填充文档模板。

它的核心判断是：

> 产品是解决问题的思考路径的具象化体现。

所以使用 Junco 时，不会先从页面或功能列表开始，也不会直接照着用户给出的实现路径写方案，而是先澄清：

- 要解决什么真实问题
- 谁遇到了这个问题，以及为什么重要
- 用户在什么场景下做决策
- 用户的自然思考路径和深层动机是什么
- 系统里有哪些核心概念、模型、状态和边界
- 数据、权限、规则、异常和流程如何组织
- 是否存在比用户原始方案更简单、更普世的解决方式
- 方案如何被交付、验证和验收

### 核心方法

Junco 基于《做一个好产品》的完整方法论，而不是只套 PRD 模板。它强调：

1. 先定义真实问题，再设计功能。
2. 以最小充分成本解决问题，避免过度设计。
3. 先理解用户思考路径，再写交互和流程。
4. 穿透表层行为，识别人性、责任、信任、控制、效率、安全感等深层动机。
5. 复杂系统先做模型抽象和概念定义，再落页面模块。
6. 用角色 x 模型推导用户故事，而不是只枚举 CRUD。
7. 用第一性原理挑战旧流程、旧系统、组织习惯和用户给出的默认路径。
8. 为复杂产品制定清晰的“游戏规则”：边界、异常、保护、状态和责任。
9. 图优先于表，表优先于散文说明。
10. 具体反馈要抽象成公共规则，而不是只写“不能这样”。

处理需求时，Junco 默认按以下链路思考：

```text
Problem -> Minimum-cost goal -> User thinking path -> Human motivation
-> Concept definition -> Domain model -> Role x model user stories
-> First-principles challenge -> Product architecture
-> Game rules / boundaries -> Tangible interactions -> Delivery plan -> PRD
```

### 第一性原理需求反思

用户提出的功能、页面、流程、按钮、审批、报表或自动化，都会先被视为候选方案，而不是最终答案。

Junco 在生成或评审 PRD 前，会先要求回答：

- 用户表面上提出了什么实现路径？
- 这个请求背后的可见症状是什么？
- 如果拿掉用户指定的实现路径，剩下的第一性原理问题是什么？
- 哪些约束是真约束，哪些只是旧流程、旧系统或组织习惯？
- 是否存在更简单、更普世的模型级、规则级、数据级或流程级方案？
- 如果仍然采用用户提出的路径，为什么它是反思后的最小充分方案？

目标不是反对用户，而是避免把一个可被简化的深层问题，机械实现成更多页面、更多流程和更多维护成本。

### 适合使用的场景

- 从 0 到 1 完成完整产品方案设计，并沉淀为 PRD
- 梳理平台、后台、运营系统、工作流产品
- 把模糊需求拆成概念模型、流程和模块
- 审查 PRD 是否足够清晰、完整、可落地
- 把具体 UX 反馈抽象成可复用的产品规则
- 设计 P0/P1/P2 范围、验收标准和质量门禁
- 生成 Mermaid 概念关系图、系统边界图、流程图、状态机和数据责任图

复杂平台、系统、流程、治理、运营类产品默认进入完整产品设计模式，不输出轻量提纲，除非用户明确要求。

### 交付质量要求

Junco 的 PRD 不应停留在背景、目标、概念、CRUD、权限表和阶段列表。完整 PRD 需要包含：

- 需求反思与第一性原理解释
- 背景、现状、根因、影响和范围
- 概念定义、领域模型、关系、状态、所有权和数据源
- 角色 x 模型推导出的用户故事
- 系统边界、产品架构、关键流程和方案取舍
- P0 模块的字段、操作、状态约束、异常、审计和验收
- 权限、通知、回滚、迁移、依赖、风险和里程碑

其中 `Feedback-to-Rule Method` 用于处理迭代中的体验反馈：

- 提取用户所处的决策点
- 区分用户语言和内部实现语言
- 检查筛选项是否同层级、正交
- 判断信息出现时机是否匹配用户意图
- 对齐颜色、布局、状态的产品语义
- 校验数据是否足以支撑用户动作
- 同步更新 PRD、验收标准和实现规范

### 安装

将仓库克隆到你使用的模型工具或智能体框架的 skills / prompts 目录：

```bash
git clone https://github.com/xyjunco/junco-skill <your-skills-dir>/junco
```

如果本地已经存在：

```bash
cd <your-skills-dir>/junco
git pull
```

### 使用方式

在支持技能、系统提示或知识库挂载的模型工具中使用：

```text
用 junco 完成这个需求的产品设计，并沉淀为 PRD。
```

或在需要产品需求分析、产品设计、PRD review、产品规则抽象时使用。

### 目录结构

```text
junco/
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    ├── diagram-patterns.md
    ├── methodology.md
    ├── platform-patterns.md
    ├── prd-depth-rubric.md
    ├── prd-template.md
    └── review-checklist.md
```

## English

### What This Skill Is For

Junco helps any capable language model or AI agent turn raw product input into rigorous product design.

It is useful when a request starts as a vague idea, a stakeholder ask, an operational pain point, a platform/system design problem, an existing PRD, or concrete UX feedback that needs to become a reusable rule.

The central principle is:

> A product is the tangible expression of a thinking path for solving a problem.

Junco therefore starts from the problem, not from screens, feature lists, or the stakeholder's proposed implementation path.

### Core Method

Junco is based on the full "make a good product" methodology:

1. Define the real problem before designing features.
2. Solve the problem with the minimum sufficient cost.
3. Understand user thinking paths before writing interaction rules.
4. Look through surface behavior to human motivation: trust, control, safety, responsibility, efficiency, anxiety, or curiosity.
5. Model concepts before designing pages.
6. Derive user stories from role x model, not only from CRUD tasks.
7. Use first principles to challenge inherited process, legacy systems, org habits, and the user's requested path.
8. Define product game rules: boundaries, exceptions, protections, states, and responsibilities.
9. Prefer diagrams over tables, and tables over prose.
10. Convert concrete feedback into positive product standards, not only prohibitions.

The default reasoning chain is:

```text
Problem -> Minimum-cost goal -> User thinking path -> Human motivation
-> Concept definition -> Domain model -> Role x model user stories
-> First-principles challenge -> Product architecture
-> Game rules / boundaries -> Tangible interactions -> Delivery plan -> PRD
```

### First-Principles Demand Reflection

When the user asks for a feature, workflow, page, approval, dashboard, report, or automation, Junco treats it as a candidate solution rather than the requirement itself.

Before designing a solution or reviewing a PRD, Junco asks:

- What implementation path did the user request on the surface?
- What visible symptom triggered the request?
- If that requested path is removed, what first-principles problem remains?
- Which constraints are real, and which are inherited from old processes, old systems, or org habits?
- Is there a simpler or more universal model-level, rule-level, data-level, or process-level solution?
- If the requested path is still chosen, why is it the minimum sufficient solution after reflection?

### When To Use It

Use Junco when you need to:

- Design a full product solution from an early product idea and deliver it as a PRD
- Model a platform, workflow, admin system, or operational tool
- Define concepts, entities, states, ownership, and boundaries
- Turn user paths into modules, rules, permissions, and acceptance criteria
- Review an existing PRD for clarity, completeness, and delivery readiness
- Abstract repeated UX feedback into reusable product quality gates
- Split scope into P0/P1/P2 and define milestone acceptance

### Output Quality

A Junco PRD should not stop at background, goals, glossary, CRUD bullets, permissions, and phases. It should expose:

- Demand reflection and first-principles interpretation
- Problem context, current situation, root cause, impact, and scope
- Concepts, domain model, relationships, states, ownership, and source of truth
- User stories derived from role x model
- System boundaries, product architecture, core flows, and solution tradeoffs
- P0 module fields, operations, state constraints, exceptions, audit, and acceptance
- Permissions, notifications, rollback, migration, dependencies, risks, and milestones

The `Feedback-to-Rule Method` helps convert implementation feedback into reusable product rules:

- Extract the user's decision moment
- Separate user language from internal implementation language
- Check whether options in one control are conceptually orthogonal
- Match information timing to user intent
- Align visual semantics with product semantics
- Verify that the data shown is precise enough to support the action
- Keep PRDs, acceptance criteria, and implementation guidance in sync

### Installation

Clone this repository into the skills / prompts directory used by your model tool or agent framework:

```bash
git clone https://github.com/xyjunco/junco-skill <your-skills-dir>/junco
```

If you already have it locally:

```bash
cd <your-skills-dir>/junco
git pull
```

### Usage

Use it in any model tool that supports reusable skills, system prompts, or mounted knowledge:

```text
Use junco to design a product solution for this request and deliver it as a PRD.
```

You can also use it whenever you need product requirement analysis, product design, PRD review, or abstraction of product interaction rules.

### Repository Structure

```text
junco/
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    ├── diagram-patterns.md
    ├── methodology.md
    ├── platform-patterns.md
    ├── prd-depth-rubric.md
    ├── prd-template.md
    └── review-checklist.md
```
