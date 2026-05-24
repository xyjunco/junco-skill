# Junco Skill

Junco is a Codex skill for product requirement analysis, product modeling, and high-quality PRD writing.

It helps turn raw needs, vague feature requests, stakeholder feedback, operational pain points, or early product ideas into structured product documents with clear problems, concepts, models, flows, rules, milestones, and acceptance criteria.

## 中文说明

### 这个 Skill 解决什么问题

Junco 用于把“想做一个功能”“有个产品想法”“这里体验不好”这类原始需求，转成可评审、可设计、可开发、可验收的 PRD。

它的核心判断是：

> 产品是解决问题的思考路径的具象化。

所以使用 Junco 时，不会先从页面或功能列表开始，而是先澄清：

- 要解决什么问题
- 谁遇到了这个问题
- 用户在什么场景下做决策
- 系统里有哪些核心概念
- 数据、状态、权限、边界和流程如何组织
- 方案如何被交付和验收

### 适合使用的场景

- 从 0 到 1 撰写完整 PRD
- 梳理平台、后台、运营系统、工作流产品
- 把模糊需求拆成概念模型、流程和模块
- 审查 PRD 是否足够清晰、完整、可落地
- 把具体 UX 反馈抽象成可复用的产品规则
- 设计 P0/P1/P2 范围、验收标准和质量门禁

### 核心方法

Junco 强调：

1. 先定义问题，再设计功能。
2. 先建立概念模型，再落页面模块。
3. 先理解用户思考路径，再写交互规则。
4. 图优先于表，表优先于散文说明。
5. 具体反馈要抽象成公共规则，而不是只写“不能这样”。

其中 `Feedback-to-Rule Method` 用于处理迭代中的体验反馈：

- 提取用户所处的决策点
- 区分用户语言和内部实现语言
- 检查筛选项是否同层级、正交
- 判断信息出现时机是否匹配用户意图
- 对齐颜色、布局、状态的产品语义
- 校验数据是否足以支撑用户动作
- 同步更新 PRD、验收标准和项目规则

### 安装

将仓库克隆到 Codex skills 目录：

```bash
git clone https://github.com/xyjunco/junco-skill ~/.codex/skills/junco
```

如果本地已经存在：

```bash
cd ~/.codex/skills/junco
git pull
```

### 使用方式

在 Codex 中显式触发：

```text
[$junco] 请帮我把这个需求整理成 PRD
```

或在需要产品需求分析、PRD 写作、PRD review、产品规则抽象时使用。

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

Junco helps Codex turn raw product input into rigorous product requirements.

It is useful when a request starts as a vague idea, a stakeholder ask, an operational pain point, a platform/system design problem, or concrete UX feedback that needs to become a reusable rule.

The central principle is:

> A product is the tangible expression of a thinking path for solving a problem.

Junco therefore starts from the problem, not from screens or feature lists.

### When To Use It

Use Junco when you need to:

- Draft a full PRD from an early product idea
- Model a platform, workflow, admin system, or operational tool
- Define concepts, entities, states, ownership, and boundaries
- Turn user paths into modules, rules, permissions, and acceptance criteria
- Review an existing PRD for clarity, completeness, and delivery readiness
- Abstract repeated UX feedback into reusable product quality gates
- Split scope into P0/P1/P2 and define milestone acceptance

### Core Method

Junco emphasizes:

1. Define the problem before designing features.
2. Model concepts before designing pages.
3. Understand user thinking paths before writing interaction rules.
4. Prefer diagrams over tables, and tables over prose.
5. Convert concrete feedback into positive product standards, not only prohibitions.

The `Feedback-to-Rule Method` helps convert implementation feedback into reusable product rules:

- Extract the user's decision moment
- Separate user language from internal implementation language
- Check whether options in one control are conceptually orthogonal
- Match information timing to user intent
- Align visual semantics with product semantics
- Verify that the data shown is precise enough to support the action
- Keep PRDs, acceptance criteria, and project rules in sync

### Installation

Clone this repository into your Codex skills directory:

```bash
git clone https://github.com/xyjunco/junco-skill ~/.codex/skills/junco
```

If you already have it locally:

```bash
cd ~/.codex/skills/junco
git pull
```

### Usage

Trigger it explicitly in Codex:

```text
[$junco] Help me turn this product request into a PRD.
```

You can also use it whenever you need product requirement analysis, PRD writing, PRD review, or abstraction of product interaction rules.

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
