# PRD 产品方案个人写作风格

Use this reference when drafting, rewriting, or reviewing a Chinese PRD `产品方案`, `产品方案与系统架构`, detailed module design, or page specification in the user's established style.

## Contents

1. [Scope And Precedence](#1-scope-and-precedence)
2. [Core Writing Formula](#2-core-writing-formula)
3. [Document And Page Structure](#3-document-and-page-structure)
4. [Atomic Specification Rules](#4-atomic-specification-rules)
5. [Object-Specific Templates](#5-object-specific-templates)
6. [Flow, State, And Data Rules](#6-flow-state-and-data-rules)
7. [Language And Visual Emphasis](#7-language-and-visual-emphasis)
8. [WIP Cleanup](#8-wip-cleanup)
9. [Complete Product-Solution Template](#9-complete-product-solution-template)
10. [Final Checklist](#10-final-checklist)

## 1. Scope And Precedence

Treat this style as an expression and completeness contract, not as a product-discovery method.

- First derive the real problem, concepts, domain model, ownership, system boundary, rules, and states through Junco.
- Then express the stable solution through the page/module writing structure in this reference.
- Do not let the page-based format reverse the reasoning order or turn product design into feature stitching.
- Do not expose the demand, brief, first-principles reasoning, reviewer commentary, implementation notes, or design explanation inside user-facing page copy.
- Distinguish confirmed facts, proposed design, and unresolved business decisions. Put material missing decisions in a consolidated table with evidence, impact, owner, and next step; reference them where they affect the solution.
- Write authorized routine layout and copy directly as the proposed solution. State proposal status at the relevant solution level rather than prefixing every field with `建议方案` or every string with `建议文案`. User-facing pages show the actual copy.
- Preserve uncertainty about real defaults, enums, permissions, sources, transitions, and effects. A template slot is not evidence of a business fact.
- Read `prd-writing-lessons.md` for source classification, product semantics, data/batch contracts, and native-document maintenance.
- If the user explicitly requests another structure, preserve the completeness rules while adapting the presentation.

## 2. Core Writing Formula

Use this formula:

> 页面 / 产品功能模块 -> 1～2 句页面意图与边界 -> 页面区域 -> 字段 / 按钮 / 状态 -> 来源、枚举、默认、约束、联动、流转与异常

Create three kinds of certainty:

- **Scanning certainty**: a reviewer can find the page purpose, region, field, action, state, and exception quickly.
- **Implementation certainty**: engineering and QA can determine values, rules, transitions, and failure behavior.
- **Boundary certainty**: each surface and system has one clear responsibility.

Prefer:

- Page/function modules as the outer skeleton.
- Visible page regions as the inner directory.
- Fields, actions, and states as atomic specification units.
- Unordered lists and short verb-led statements over dense paragraphs.

## 3. Document And Page Structure

### 3.1 Document-Level Order

For a complex product solution, use this order when relevant:

1. Information architecture or page relationships.
2. Necessary concept and logic clarification.
3. Product solution by page or function module.
4. State machines, flows, sequence diagrams, or impact matrices.
5. Permissions, notifications, data definitions, milestones, and acceptance.

Use a concept table before page details when nouns may be confused. Define:

- Meaning.
- Owner.
- Source of truth.
- Lifecycle relevance.
- Difference from similar concepts.

### 3.2 Three-Column Product-Solution Structure

When the destination supports a wide layout, use:

| 产品模块 | 产品方案 | 原型示意 |
|---|---|---|
| 页面 / 子模块 | 结构化方案正文 | 对应页面、抽屉、弹窗、流程图或状态图 |

Use the columns as follows:

- `产品模块`: name the page, flow step, drawer, dialog, or submodule.
- `产品方案`: contain the full structured specification, not a summary.
- `原型示意`: align the relevant visual with the written module.

If the destination does not support wide tables, keep the same hierarchy with headings and unordered lists.

### 3.3 Page-Level Order

For each page or function module:

1. Write one or two sentences explaining:
   - Who uses the page.
   - What decision or task it supports.
   - What it owns.
   - Which adjacent module or system handles related responsibilities when ambiguity exists.
2. Split the page into visible regions.
3. Expand each region by field, action, or state.
4. Extract complex logic into a diagram or rule table.
5. End with exceptions, data ownership, audit, or acceptance when needed.

Use region headings such as:

- 顶部操作
- 顶部筛选控制区
- 顶部指标卡
- 快捷筛选
- 基础信息
- 场景维度补充
- 列表
- 详情
- 操作区
- 影响预览
- 同步记录
- 执行结果

Use noun phrases for headings. Use action-led statements for content.

### 3.4 Page Purpose And Boundary

Start with direct sentences such as:

- `用于……`
- `支持……`
- `展示……`
- `帮助……判断……`
- `解决「……」的问题`
Write responsibility and action in positive business language:

- `列表用于查找和选择计划，操作列直接进入该计划的调整。`
- `影响预览展示拟执行后的变化；实际结果按执行回执更新。`
- `根据配置生成 DAG，运行记录展示节点结果。`
- `消息卡片负责提醒，任务中心负责协作，源系统提供真实状态。`

Keep an explicit exclusion when it determines scope, permission, or risk. Avoid repeating reviewer instructions such as `不展示、不直接、不承担` as the main product specification.

## 4. Atomic Specification Rules

For each important field, action, state, card, metric, filter, or table column, select the relevant labels:

- 控件
- 来源
- 枚举 / 枚举值
- 默认 / 默认值
- 必填
- 格式
- 示例
- 展示
- 约束
- 校验
- 联动
- 点击
- 触发
- 结果
- 状态
- 计算
- 规则
- 权限
- 入口
- 文案
- 异常

Do not mechanically write every label for every object. Include the labels needed to remove implementation ambiguity. Keep each native list item focused on one responsibility. For prototype-to-PRD sync and dense rule repair, apply the regrouping and single-source guidance in `prd-writing-lessons.md` sections 2 and 8 before editing blocks.

When a required business fact is not grounded in the source, record the missing decision and its effect in the decision table. For example: `新建后的状态及可执行动作：由对象负责人确认，影响提交入口`.

When routine design is authorized, write the reviewable proposal directly: `失败时保留输入，展示原因并提供原地重试` or `输入框提示「请输入规则名称」`. This describes proposed behavior without claiming it is already implemented or source-confirmed.

Use complete, consistent representative data for normal examples. Document real empty/error states separately, using established semantics; distinguish missing sample values from genuinely unknown business facts.

Use this default order:

1. What it is or shows.
2. Where its value comes from.
3. What values or range are allowed.
4. Default and required behavior.
5. Format, uniqueness, and validation constraints.
6. Linkage, click destination, or downstream effect.
7. Disabled, no-permission, empty, failure, or concurrency behavior.

## 5. Object-Specific Templates

### 5.1 Field

```markdown
项目名称
- 控件：Input，必填
- 来源：项目创建时填写
- 约束：同一交付对象下不可重名，最长 80 字
- 示例：H200 样机导入
- 点击：进入项目详情页
```

For a field, answer as relevant:

- What component renders it?
- Is it required?
- What is the default?
- What is the source of truth?
- Can the user edit it?
- What values, units, precision, length, or format are allowed?
- Is it unique, permission-limited, or dependent on another field?
- What does it filter, calculate, or change?
- What happens when the value is missing, invalid, stale, or unavailable?

### 5.2 Button Or Action

Write a complete action chain:

```markdown
保存安排
- 展示条件：当前用户有编辑权限
- 前置条件：安排数量与对象版本校验通过
- 点击：保存该对象的拟执行安排
- 携带上下文：对象 ID、当前版本和安排数量
- 成功结果：更新安排版本与预计影响，实际执行结果仍按回执更新
- 页面反馈：提示「已保存」，返回原列表并保留筛选条件
- 异常：提交中禁用按钮；失败保留输入并支持重试
- 审计：记录操作人、时间和变更前后值

确认执行
- 前置条件：预览已完成，执行范围、权限和最新版本校验通过
- 点击：提交预览中的执行对象及数量，按幂等标识创建请求
- 成功结果：记录请求编号与受理状态；实际执行结果按回执更新
- 页面反馈：提示「请求已提交」，返回任务所在列表并刷新相关对象
- 异常：受理结果未知时先查询请求状态，再决定重试
```

Cover as relevant:

- Location and visibility.
- Permission and prerequisites.
- Disabled or hidden behavior.
- Destination, drawer, dialog, or direct mutation.
- Carried object ID, filters, version, or scope.
- Validation and conflict handling.
- Success feedback and state change.
- Failure, retry, idempotency, rollback, and audit.

Do not stop at `点击后打开弹窗`.

### 5.3 List

```markdown
项目列表
- 页面目的：帮助项目经理快速找到需要优先处理的交付项目
- 搜索范围：项目名称、交付对象
- 默认排序：按当前动作优先级和更新时间倒序
- 批量操作：选择范围后展示影响汇总；按实际后果决定是否单独确认，预览已满足最终决定时直接提交

项目名称
- 展示：项目创建时填写的名称
- 来源：项目表
- 约束：超长省略，Hover 时通过 Tooltip 展示全称
- 点击：进入项目详情页

状态
- 枚举：阻塞、预警、待响应、健康
- 来源：项目健康度计算结果
- 展示：使用 Tag 和颜色区分
- 筛选：支持多选

操作
- 查看：进入详情页
- 编辑：有权限时展示
- 删除：进入删除确认流程
```

Define:

- Search trigger and whether it filters the full dataset.
- Filter values and source.
- Default sort.
- Batch input/selection, actual volume, whole-batch validation, execution scope across pagination, correction, submission, and result/return path. Confirmation depends on actual consequence.
- Column value, source, format, filter, sort, truncation, Tooltip, copy, and click destination.
- Status-dependent actions.
- Empty, loading, error, no-permission, and stale-data behavior.

### 5.4 Form, Drawer, Or Dialog

```markdown
新建 / 编辑抽屉
- 入口：点击「新建」或列表操作列「编辑」
- 编辑态：回填当前配置
- 只读态：无权限用户仅可查看

基础信息
- ……

底部操作
- 取消：关闭抽屉，不保存本次修改
- 确认：校验通过后提交
- 提交中：按钮置灰，避免重复点击
- 成功：提示「保存成功」，刷新列表
- 失败：保留已填写内容，并展示失败原因
```

Clarify:

- Whether create, edit, and view reuse the same surface.
- Whether the surface is a page, drawer, full-screen dialog, modal, or popconfirm.
- Which fields are editable, read-only, disabled, or hidden.
- What is reset or preserved on close and reopen.

### 5.5 Status

```markdown
状态
- 枚举：待处理、处理中、已完成、已关闭
- 来源：任务状态机
- 展示：使用 Tag 和颜色区分
- 筛选：支持按状态多选

待处理
- 进入条件：任务已创建，尚未开始处理
- 可执行动作：开始处理、转交、关闭

处理中
- 进入条件：用户接单或外部系统回写处理中
- 可执行动作：完成、转交、补充记录

已完成
- 进入条件：提交结果并通过完成校验
- 可执行动作：重开、补充关闭原因
```

For complex status, define:

- State semantics.
- Source of truth.
- Entry condition.
- Available actions.
- Exit condition.
- Display color, icon, Tag, or Tooltip.
- Downstream effect.
- Terminal, reopen, cancel, rollback, or recovery behavior.
- Whether a visual marker is a mutually exclusive main state or a stackable flag.

### 5.6 High-Risk Action

Classify risk by scope, reversibility, overwrite, and financial/permission/runtime consequences. Action names such as bulk, save, or sync do not determine risk on their own.

```markdown
执行影响
- 展示确切对象、范围、变更前后值和关联对象处理方式
- 有策略选择时，说明每种选择的结果
- 执行前重新校验权限和最新状态
- 成功记录结果与审计；失败保留原因及恢复入口
```

Cover the relevant chain: precheck -> impact -> necessary user choice -> final validation -> idempotent execution -> result/audit -> recovery. The existing preview may already be the final submission surface. Add a separate confirmation only for an additional decision or material consequence; add a result page only for meaningful result review, partial success, or long asynchronous work.

## 6. Flow, State, And Data Rules

### 6.1 Extract Complex Logic

Use a separate diagram or matrix when the logic includes:

- Three or more actors.
- Multiple state branches.
- Asynchronous external callbacks.
- One action affecting several downstream objects.
- Coordinated changes across message, task, event, or source systems.

Choose:

- Information architecture for page relationships.
- Flowchart for branching operations.
- Sequence diagram for cross-system interaction.
- State machine for lifecycle.
- Impact matrix for upstream/downstream propagation.

Keep the detailed page text focused on rules and decisions. Do not repeat the whole diagram in prose.

### 6.2 Data Traceability

For every calculated or summarized value, define:

```markdown
T0 偏差
- 格式：+5d、+2d、0d、-1d
- 来源：预测 T0 减目标 T0
- 约束：正值使用风险色，0 使用中性色，负值表示提前
```

Clarify:

- Source table or external system.
- Formula.
- Deduplication rule.
- Time window.
- Realtime, scheduled, or asynchronous update.
- Snapshot/version.
- Whether multiple pages read one canonical result.
- Actual empty, delayed, stale, or failed-source behavior where established or proposed for the product; keep source gaps in the decision table and tooling failures in the work log.

Verify source-field definitions and variable mappings before renaming a formula. An undefined denominator remains an explicit missing decision; nearby nouns and reference examples are not evidence of its meaning. For business readers, use named-field formulas before engineering symbols. Define numerator/denominator, population, resource/unit, time/version, deduplication, and precision beside the formula. Distinguish comparison population, visible subset, and modification set; pagination and selection must follow an explicit scope contract. Check pre/post values against the same baseline and use full precision for thresholds.

### 6.3 Responsibility And Source Boundaries

Name:

- Which product object owns the rule.
- Which system owns the truth.
- Which page displays, configures, applies, or audits it.
- Which action creates a runtime mutation.
- Which history or recovery surface explains a failure.

Place conflict handling at the action that creates or discovers the conflict. Do not duplicate the same conflict wizard in unrelated save, apply, and history flows.

## 7. Language And Visual Emphasis

### 7.1 Sentence Style

Read the user's current writing sample first. Use short business-readable sentences, with one main rule per sentence and its dependencies intact. Prefer responsibility, object, action, and outcome over repeated negative prompt rules. Use short sentences and verb-led bullets:

- 展示
- 支持
- 点击
- 打开
- 跳转
- 进入
- 过滤
- 触发
- 生成
- 写入
- 更新
- 保留
- 阻断
- 提示
- 记录

Prefer:

- `点击进入详情页`
- `默认按更新时间倒序排列`
- `未选择对象类型时，模板区域置灰`
- `提交后记录请求编号；执行结果按回执更新`

Avoid:

- `用户可以通过点击这个按钮来进入到对应的详情页面，从而查看相关信息。`

### 7.2 Names, Copy, And Identifiers

- Use noun phrases for headings.
- Put button copy, prompt copy, and status names in Chinese quotes: `「新增水位线」`.
- Preserve exact engineering identifiers when they are implementation contracts: `package_id`, `follow_template = true`, `YYYY-MM-DD HH:mm:ss`.
- Use concrete examples, ranges, thresholds, units, and copy when facts are known.
- Use one canonical term consistently. Do not alternate synonyms or mixed capitalization.

### 7.3 Emphasis

Preserve the destination's established font, heading hierarchy, indentation, and semantic colors. Keep ordinary prose and data at normal weight; emphasize short action labels, important thresholds, risks, and conclusions locally. Do not bold whole paragraphs or color every quoted noun. Preserve native links and unrelated rich-text runs during revision.

Normalize Chinese/English, number/unit, punctuation, and date spacing according to the document's convention. Keep IDs, code identifiers, paths, and domains unchanged.

Optional callouts follow the existing style: `🎯` for purpose, `⚠️` for material constraints, `ℹ️` for mechanisms, and `❗` for a confirmed counterintuitive conclusion. Use them only when they improve scanning. Put unresolved business decisions in a consolidated decision table rather than decorating every field.

Keep action guidance, static evidence, comparison, and history visually distinct. Status belongs with its object; supporting links belong next to their data. A rendered review checks alignment, whitespace, weight, color, and clipping.

## 8. WIP Cleanup

Before delivering a reviewable PRD, remove:

- Dated inline change notes such as `0428 新增`.
- Strikethrough alternatives left beside the chosen solution.
- Conversational questions such as `先不考虑？` or `看是否有需求`.
- Duplicated sentences or repeated control descriptions.
- Misspellings, mixed capitalization, and terminology drift.
- Screenshot-only logic without written rules.
- Page copy that exposes PRD rationale, reviewer notes, fallback implementation details, or hidden system mechanisms.
- Happy-path-only descriptions that omit relevant permission, empty, failure, retry, and duplicate-submit rules. Design justified exceptions separately; do not populate normal examples with invented failures or missing-value placeholders.

Preserve change history only when the user explicitly asks for a WIP or revision log. Keep it outside the canonical product-solution body when possible.

## 9. Complete Product-Solution Template

```markdown
## 页面 / 功能模块名称

用 1～2 句话说明页面服务的角色、主要目标、支持的决策和产品边界。

> 🎯 定位：……

| 产品模块 | 产品方案 | 原型示意 |
|---|---|---|
| 模块名称 | 见下方结构化方案 | 对应原型 |

### 顶部操作

搜索框
- 控件：Input
- 支持搜索：……
- 来源：……
- 触发：按 Enter 或点击搜索 icon
- 约束：输入为空时恢复当前筛选结果
- 异常：接口失败时保留输入并提示重试

新建
- 展示条件：……
- 点击：打开「新建……」抽屉
- 权限：……

### 顶部筛选控制区

筛选项名称
- 控件：Select
- 枚举：……
- 默认值：……
- 来源：……
- 联动：影响指标卡、列表和图表
- 约束：……

### 指标卡

指标名称
- 展示：……
- 来源：……
- 计算：……
- 时间口径：……
- 点击：将对应条件应用到列表

### 列表

列表用于……

字段名称
- 展示：……
- 来源：……
- 格式：……
- 筛选 / 排序：……
- 点击：……

状态
- 枚举：……
- 展示：使用 Tag 和颜色区分
- 操作联动：不同状态下展示……

操作
- 查看：……
- 编辑：……
- 删除：……

### 新建 / 编辑抽屉

字段名称
- 控件：……
- 必填：是 / 否
- 默认值：……
- 来源 / 枚举：……
- 约束 / 校验：……
- 联动：……

底部操作
- 取消：关闭抽屉，不保存
- 确认：校验通过后提交
- 提交中：按钮置灰，避免重复点击
- 成功：提示……，刷新……
- 失败：保留填写内容，展示失败原因

### 状态与流转

状态名称
- 进入条件：……
- 可执行动作：……
- 退出条件：……
- 对下游影响：……

### 异常与边界

> ⚠️ 约束
> - ……
> - ……

- 空数据：……
- 加载中：……
- 接口失败：……
- 无权限：……
- 数据已变化 / 并发冲突：……

### 数据与审计

- 数据来源：……
- 计算口径：……
- 审计记录：操作人、操作时间、操作对象、变更前后值、结果
```

## 10. Final Checklist

### Structure

- [ ] Split by page or product-function module.
- [ ] Start every page/module with purpose and responsibility boundary.
- [ ] Split the body by visible page regions.
- [ ] Align each visual with the corresponding written module.

### Fields And Components

- [ ] Define control, required/default behavior, enum/range, format, and source.
- [ ] Define field linkage and read-only/disabled/no-permission behavior.
- [ ] Define invalid, missing, stale, or unavailable-source behavior.

### Actions And Transitions

- [ ] Define visibility, permission, prerequisite, and click destination.
- [ ] Define carried object, filters, scope, or version.
- [ ] Define success feedback and resulting state/data/page changes.
- [ ] Define failure, retry, idempotency, and audit.
- [ ] Show exact impact and necessary choices for materially risky operations; confirmation adds a distinct decision rather than repeating the preview.

### States

- [ ] Define enum, semantics, and source of truth.
- [ ] Define entry condition, available action, and exit condition.
- [ ] Define color, Tag, icon, Tooltip, or disabled semantics.
- [ ] Define downstream effect and reopen/rollback behavior.

### Data And Exceptions

- [ ] Define source, formula, time window, deduplication, and update timing.
- [ ] Cover empty, loading, error, no-permission, concurrency, and duplicate submit.
- [ ] Consolidate material open business decisions with source, impact, owner, and next step.
- [ ] Confirm that no default, enum, permission, source, transition, or result was invented to fill a slot.
- [ ] Distinguish confirmed rules, proposed design, and verified implementation at the solution level.
- [ ] Use actual page copy for authorized routine designs, with no process-label prefixes.
- [ ] Check complete normal examples, quantity arithmetic, units, population, time/version, and precision.
- [ ] Keep comparison, visible, and modification scopes distinct; full-batch validation matches execution scope.

### Expression

- [ ] Use unordered lists and short verb-led statements.
- [ ] Use noun phrases for headings.
- [ ] Put exact button, prompt, and status copy in `「」`.
- [ ] Remove WIP debris, duplicated wording, spelling errors, and term drift.
- [ ] Keep emphasis sparse and semantic; verify rich-text colors, font weight, spacing, links, and rendered layout.
- [ ] Use positive product semantics and preserve real boundaries.
- [ ] Propagate model/term changes to affected diagrams and prototypes; keep withdrawn scope out of the current solution.
