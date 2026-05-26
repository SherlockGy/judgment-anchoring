# 维护流程

## 知识路由（维护视角）

从 references/anchor-catalog.md 开始：

1. 检查目标领域是否已存在
2. 已存在 → 评估需要补充 / 修订什么
3. 不存在 → 创建新 domain 子目录

## 写入原则

### 配方必须经过验证

不得凭空把锚点写入 domains/。新配方必须满足：

- 至少经过一次实际任务验证（用户认可效果）
- 锚点的训练存在性已确认（不是 vanity anchor）
- 通过 references/anti-patterns.md 的锚点检验
- 锚点之间不重叠覆盖维度
- 必要规则是真客观约束，不是任何锚点 facet 的反向陈述（见 anti-patterns「一条边界」）

### 触发特征必须区分度足

新增 domain 的触发特征不能和已有 domain 重叠歧义。
如果重叠 → 应该合并而不是新增。

### 配方必须自包含

每个 domain README.md 必须独立工作，不依赖其他 domain 文件。

> 跨生态搬锚点 / 在锚点后挂规则清单 / 维度漂移 等失败模式，参见 references/anti-patterns.md 的锚点检验。

### 锚点管不了的步骤独立成文、按需引用

锚点能产出判断，但有些步骤锚点做不到——典型是**求证**（出去核对现实）。这类步骤不写进通用的 `flows/execute.md`，而是独立成文（如 `references/verification.md`），**只被需要它的 domain 在自己 README 里引用**。判断密集、结论依赖现实认识的 domain（思辨 / 决策 / 诊断）才引用；产出型 domain（代码 / 小说等）不引用。新增 domain 时按其类型决定引不引用。

## 工作流

### 场景 A：新增 domain 配方（最常见）

触发条件见 `flows/execute.md` Step 4。

1. 在 `references/domains/` 创建新子目录 `{领域名}/`
2. 写 `README.md`，按下方模板填写
3. 在 `references/anchor-catalog.md` 追加索引行
4. 检查新 domain 的触发特征是否和已有 domain 重叠 — 重叠则需要合并讨论

### 场景 B：修订已有 domain

- 锚点失效（某个人不再活跃 / 更好的锚点出现）→ 替换锚点
- 新发现的硬约束（非锚点 facet 能覆盖的）→ 加到 README 的「必要规则」段
- 触发特征不准确（误匹配率高）→ 修改 catalog 的匹配规则
- 需要合并或拆分 domain（两个 domain 触发特征重叠 / 一个 domain 内部出现两类显著不同的任务）→ 先和用户讨论方案再动手

每次修订前先通读目标 README.md 全文，理清现有结构和上下文，不得跳过理解直接局部修改。

## 模板

### domains/{领域名}/README.md

```markdown
# 领域：{领域名}

**适用：** {一句话触发描述，和 anchor-catalog.md 对齐}

## 锚点配方

| 维度 | 人名 | facet |
|---|---|---|
| {维度 1} | {人名} | {该人在此维度的具体立场，一句话} |
| ... | ... | ... |

## 必要规则

- {规则 1：锚点无法自带的客观约束——语言 / 工具 / 格式 / 客观陷阱}
- {规则 2}
- ...
```

### anchor-catalog.md 中的一行

| {领域名} | {ALL 必须满足的特征} | domains/{领域名}/README.md |

## 违反就停

任一发生立即停止：

- 凭空写入未经验证的配方（无真实任务支撑、未通过锚点检验）
- 修订前没读目标 README 全文就开始局部修改
- 新建 domain 但未同步更新 anchor-catalog.md
- 新 domain 的触发特征与已有 domain 重叠歧义
- 在定义新 domain 时跨生态搬锚点（如把 Rust 锚点用在 Python domain）
- 新增 domain 配方里没有「必要规则」段，或必要规则里全是锚点 facet 的反向陈述（无真客观约束）—— 这是凭印象写 domain 的信号
