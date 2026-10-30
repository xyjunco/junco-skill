# Junco Skill

Junco is a model-agnostic methodology and reusable skill package for product requirement analysis, product modeling, and high-quality product design.

It helps turn raw needs, vague feature requests, stakeholder feedback, operational pain points, platform/system ideas, or existing PRDs into rigorous product designs with clear problems, concepts, models, flows, rules, page content, actual UI copy, milestones, and acceptance criteria. It also supports scoped PRD revision in the user's established style, preserving confirmed decisions and document structure. The final delivery artifact is often a PRD, but the purpose is product design quality rather than template completion.

## 核心思想文档

Junco 的核心产品思想可参阅仓库提供的 [《做一个好产品》PDF](做一个好产品.pdf)。该文档说明从原始需求回到真实问题、用户思考路径、领域模型、产品规则和可评审 PRD 的方法。

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
9. 按信息任务选择图、表和文字：关系与流程用图，精确条目用表，趋势与分布用图表，判断依据用短文。
10. 具体反馈要抽象成公共规则，而不是只写“不能这样”。
11. 在画页面或流程前，先审计产品逻辑归属：哪个对象拥有哪个字段、哪个动作负责哪类冲突、哪个状态来自哪个系统。
12. 按用户决策合并重复页面，不因为标题不同就保留两套逻辑相同的流程。

处理需求时，Junco 默认按以下链路思考：

```text
Problem -> Minimum-cost goal -> User thinking path -> Human motivation
-> Concept definition -> Domain model -> Role x model user stories
-> First-principles challenge -> Product architecture
-> Game rules / boundaries -> Page content and copy -> Delivery plan -> PRD
```

### 产品逻辑归属审计

当需求涉及保存、预览、同步、发布、删除、审批、运行任务、历史记录或异常处理时，Junco 会先做 `Product Logic Ownership Audit`，避免把逻辑放错页面或动作。

它会检查：

- 每个核心对象拥有什么、不拥有什么，source of truth 是哪里
- 保存、预览、同步、发布、删除、运行任务分别改变什么状态
- 冲突处理应该发生在保存、同步、运行任务还是删除动作中
- 哪些异常是用户当前必须决策的，哪些只应该进入历史、审计或恢复入口
- 用户页面是否暴露了 PRD 推理、实现细节或内部方案说明
- 是否存在多个页面在回答同一个用户问题，需要合并成一个 canonical flow
- 页面是否有明确决策：用户看到什么、判断什么、做什么、失败后去哪

这套审计用于保证产品方案先逻辑正确，再进入交互和视觉设计。

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
- 使用适合目标文档的原生图示或 Mermaid 表达概念关系、系统边界、流程、状态与数据责任

新建复杂产品方案默认完成可评审的完整设计；已有 PRD 修订保留当前结构和授权范围，用户明确要求简版时按简版交付。完整性取决于问题是否回答清楚，而非固定章节数。

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

### PRD 写作与迭代

- **每次写文档、画图前使用 Humanizer。** 文档新写、修订和图示更新都先润色文案，再写入或绘制；覆盖标题、正文、表格、图注、节点和连线。保留业务含义及列表结构。
- **正文分点，一点讲清一件事。** 同组规则用二级列表，步骤用有序列表，对比用表格。正文讲清谁做什么、得到什么结果，工作推理和工具检查留在工作记录。
- 按问题 → 模型 → 规则 → 页面内容与实际文案设计，再使用目标工具的技能交付。沿用用户样文，保留当前结构、确认决定与授权范围；用户诉求写实际工作，评审意见写入方案，归纳的诉求注明来源。
- 区分确认事实、方案、未决决定与验证结果。常规文案与布局作为可评审方案写出；未决业务事实集中记录依据、影响、负责人和下一步。页面展示实际文案，需求、brief 和 PRD 推理留在工作文档。
- 指标写清来源、单位、时点、版本和公式，分别定义计算总体、可见范围和执行集合。正常样例完整可对账；批量操作写清校验、纠错、提交范围、幂等、结果和返回路径。
- 普通重点与导航链接使用不同强调方式；标题、原生枚举标签和空格沿用文档规范。原型与对应模块放在一起，正文示例仅在解释规则时使用。
- Milestone 按迭代说明主要功能和用户目标，P0 先让主链路独立可用。字段与异常细节留在产品方案；需要研发排期时再补有依据的日期、负责人和依赖。修订后回读相关正文与原型，按实际取得的证据报告结果。

详细规范见 [PRD 写作与迭代规范](references/prd-writing-lessons.md)、[产品方案写作风格](references/prd-product-solution-writing-style.md) 和 [检查清单](references/review-checklist.md)。

### 安装

先在同一运行环境中安装并注册 `humanizer` skill，确保模型能够找到并读取它。Humanizer 是必需依赖，由使用者单独安装。

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

常见用法：

```text
使用 junco 阅读这个 PRD，找出产品逻辑、边界、异常和验收遗漏。
```

```text
使用 junco 重新梳理这个同步/保存/删除流程，判断冲突处理应该放在哪个动作里。
```

```text
使用 junco 把这轮原型反馈抽象成通用产品规则，并更新 PRD。
```

### 依赖与边界

Junco 是产品设计和 PRD 方法论技能。文档与图示文案依赖 `humanizer` skill，Figma、本地 UI 组件库和代码运行环境按任务需要使用。

- 每次写文档或画图前使用 Humanizer 润色当前文案，业务事实、权限、范围、枚举和对象关系保持准确。
- Humanizer 缺失时说明依赖情况，先推进可独立完成的分析，补齐后继续写文档或画图。
- 如果只做需求分析、PRD 设计或产品逻辑审查，不需要 Figma。
- Junco 先完成需求抽象、页面展示内容和实际文案；后续视觉设计或实现遵从用户范围与项目流程。
- 如果项目要求先进行 Product Design 页面设计、再输出 Figma，应依次完成 Junco → Product Design → `arco-design` / Figma。这是适用项目的流程要求，不是 Junco 的全局依赖。
- Junco 负责产品模型、流程、规则、页面内容、文案、异常、权限、验收和文档质量；视觉组件、图表组件、真实组件实例、Figma library 加载和画布 QA 由设计系统与目标工具技能负责。

### 目录结构

```text
junco/
├── README.md
├── SKILL.md
├── 做一个好产品.pdf
├── agents/
│   └── openai.yaml
└── references/
    ├── diagram-patterns.md
    ├── methodology.md
    ├── platform-patterns.md
    ├── prd-depth-rubric.md
    ├── prd-product-solution-writing-style.md
    ├── prd-template.md
    ├── prd-writing-lessons.md
    └── review-checklist.md
```

## English

### Core Methodology Source

The core product philosophy is documented in the [《做一个好产品》 repository PDF](做一个好产品.pdf). It explains how to move from a raw request to the real problem, user thinking paths, domain models, product rules, and a reviewable PRD.

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
9. Choose diagrams for relationships and flows, tables for precise items and rules, charts for quantitative patterns, and concise prose for judgment.
10. Convert concrete feedback into positive product standards, not only prohibitions.
11. Audit product logic ownership before drawing pages or flows: which object owns which field, which action owns which conflict, and which system owns each state.
12. Merge duplicate pages by user decision instead of keeping two flows with different titles but the same logic.

The default reasoning chain is:

```text
Problem -> Minimum-cost goal -> User thinking path -> Human motivation
-> Concept definition -> Domain model -> Role x model user stories
-> First-principles challenge -> Product architecture
-> Game rules / boundaries -> Page content and copy -> Delivery plan -> PRD
```

### Product Logic Ownership Audit

When a requirement involves saving, previewing, syncing, publishing, deleting, approving, runtime jobs, history, or exception handling, Junco runs a Product Logic Ownership Audit before designing screens.

It checks:

- What each core object owns, does not own, and uses as source of truth
- What state is changed by save, preview, sync, publish, delete, and runtime jobs
- Whether conflict handling belongs in save, sync, runtime history, or deletion
- Which exceptions require an immediate user decision and which belong in audit, history, or recovery
- Whether user-facing pages expose PRD reasoning, implementation details, or internal solution notes
- Whether multiple pages answer the same user decision and should be merged into one canonical flow
- Whether each page has a clear decision: what the user sees, judges, acts on, and does after failure

This audit keeps product logic correct before interaction or visual design begins.

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
- Use target-native diagrams or Mermaid to explain concepts, system boundaries, flows, states, and data ownership

A new complex product normally receives a complete, reviewable design. Revisions to an existing PRD preserve its useful structure and the authorized scope; an explicitly requested brief stays concise. Completeness depends on answered product questions, not a fixed heading count.

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

### PRD Writing And Revision

- **Use Humanizer before every document or diagram pass.** Polish copy before writing, revising, drawing, or updating. Include headings, body text, tables, captions, nodes, and edge labels. Preserve product meaning and useful list structure.
- **Write the body in clear points, one subject per point.** Use two-level lists for grouped rules, ordered lists for steps, and tables for comparisons. Explain who acts and what they achieve; keep working analysis and tool checks in working notes.
- Follow problem → model → rules → page content and actual copy, then use the destination's skill. Preserve the user's sample style, current structure, confirmed decisions, and scope. User needs describe real work, review feedback belongs in the solution, and synthesized needs retain their source.
- Distinguish confirmed facts, proposed design, unresolved decisions, and verified results. Draft routine copy and layout as a reviewable proposal; record missing business decisions with evidence, impact, owner, and next step. Product pages show actual UI copy; briefs and PRD reasoning stay in working documents.
- Define each metric's source, unit, time, version, and formula. Keep the calculation population, visible subset, and modification set separate. Use coherent sample data; define batch validation, correction, submission scope, idempotency, results, and return path.
- Distinguish ordinary emphasis from navigation links. Follow the document's heading, native enum-tag, and spacing conventions. Align prototypes with their modules and include prose examples where they clarify a rule.
- Iteration milestones state main functions and user outcomes, with an independently usable P0 core path. Keep field and exception detail in the page solution. Add supported dates, owners, and dependencies when scheduling is needed. Read back affected prose and prototypes after revisions and report the evidence obtained.

See [PRD writing and revision standards](references/prd-writing-lessons.md), [product-solution writing style](references/prd-product-solution-writing-style.md), and the [review checklist](references/review-checklist.md).

### Installation

Install and register the `humanizer` skill in the same runtime so the model can find and read it. Humanizer is required and installed separately.

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

Common prompts:

```text
Use junco to review this PRD and find missing product logic, boundaries, exceptions, and acceptance criteria.
```

```text
Use junco to reframe this save/sync/delete flow and decide where conflict handling belongs.
```

```text
Use junco to abstract this prototype feedback into reusable product rules and update the PRD.
```

### Dependencies And Boundaries

Junco is a product design and PRD methodology skill. Document and diagram copy requires the `humanizer` skill. Figma, local UI libraries, and a code runtime depend on the task.

- Use Humanizer before each document or diagram pass. Preserve facts, permissions, scope, enums, and object relationships while polishing copy.
- If Humanizer is missing, report the dependency and continue independent analysis; resume writing or drawing once it is available.
- For requirement analysis, PRD design, or product logic review, Figma is not required.
- Junco first completes requirement abstraction, page content, and actual UI copy. Further visual design or implementation follows the user's scope and project workflow.
- Where the project requires Product Design page design before Figma output, follow Junco → Product Design → `arco-design` / Figma. This is a requirement of the applicable project, not a global Junco dependency.
- Junco owns product models, flows, rules, page content, copy, exceptions, permissions, acceptance, and document quality. Visual components, chart components, real component instances, Figma library loading, and canvas QA belong to the design-system and destination skills.

### Repository Structure

```text
junco/
├── README.md
├── SKILL.md
├── 做一个好产品.pdf
├── agents/
│   └── openai.yaml
└── references/
    ├── diagram-patterns.md
    ├── methodology.md
    ├── platform-patterns.md
    ├── prd-depth-rubric.md
    ├── prd-product-solution-writing-style.md
    ├── prd-template.md
    ├── prd-writing-lessons.md
    └── review-checklist.md
```
