# Judgment Anchoring

`judgment-anchoring` 是一个 Codex skill，用于在代码设计、API 设计、架构取舍、技术文档、创作和日常思辨决策等判断密集任务中，通过领域锚点激活更稳定的判断标准。

它的核心不是提供一组固定答案，而是先把任务路由到合适的领域配方，再从该领域抽取锚点和必要规则，组装成执行提示词后产出结果。

## 适用场景

- Java 业务服务：订单、支付、会员、库存、退款等涉及状态、事务、幂等的业务逻辑
- Java 库代码：工具类、抽象层、限流器、缓存、连接池、parser、HTTP client 等
- Rust 系统编程：库、CLI、parser、协议实现、限流器、tracer 等
- 中文小说创作：中文武侠、故事、叙事散文
- Skill 设计审查：审查、修订或设计 `SKILL.md`、`flows/`、`references/`、domain README
- 投屏分享 deck：单文件 Vue 3 或单 HTML 的可投屏分享页
- 思辨讨论与决策分析：日常问题讨论、决策、取舍分析、战略思辨、评价与诊断

完整路由规则见 `references/anchor-catalog.md`。

## 使用方式

在支持 skill 的 Codex 环境中调用：

```text
Use $judgment-anchoring to analyze this decision with the right domain anchors.
```

执行入口是 `SKILL.md`。触发后第一步必须读取 `flows/execute.md`，再根据 `references/anchor-catalog.md` 路由到对应 domain。

如果任务没有命中已验证领域，执行流程会现场构造锚点；只有在实际任务效果良好、通过锚点检验后，才建议回写到 `references/domains/`。

## 目录结构

```text
.
├── SKILL.md
├── agents/
│   └── openai.yaml
├── flows/
│   ├── execute.md
│   └── maintain.md
└── references/
    ├── anchor-catalog.md
    ├── anti-patterns.md
    ├── verification.md
    └── domains/
```

- `SKILL.md`：skill 元数据、触发说明和顶层入口
- `agents/openai.yaml`：Codex/OpenAI 产品侧 UI 元数据，不是最低运行必需文件
- `flows/execute.md`：执行任务时的路由、组装 prompt、产出和回写建议流程
- `flows/maintain.md`：新增或修订 domain 配方时的维护流程
- `references/anchor-catalog.md`：已验证领域的路由目录
- `references/anti-patterns.md`：锚点失效、维度漂移、规则污染等问题的诊断参考
- `references/verification.md`：判断依赖现实信息时的独立求证流程
- `references/domains/`：各领域的锚点配方和必要规则

## 维护原则

新增或修订 domain 时，不得凭空写入未经验证的锚点配方。新配方至少需要经过一次实际任务验证，并通过 `references/anti-patterns.md` 中的锚点检验。

新增 domain 必须同步更新 `references/anchor-catalog.md`，并检查触发特征是否与已有领域重叠。修订已有 domain 前，先通读目标 README 全文，确认现有结构和上下文后再修改。
