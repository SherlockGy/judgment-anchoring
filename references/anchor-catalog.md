# 锚点配方总目录

## 用法

按行扫描，匹配第一个"触发特征 ALL 全中"的行。路由规则(命中 / 多候选 / 未命中)见 `flows/execute.md` Step 0。

## 已验证领域

| 领域                      | 必须满足的特征                                                                          | 路由到                                   |
|-------------------------|----------------------------------------------------------------------------------|---------------------------------------|
| **java-business**       | Java + 业务逻辑（订单 / 支付 / 会员 / 库存 / 退款等）+ 涉及状态 / 事务 / 幂等                             | domains/java-business/README.md       |
| **java-stdlib**         | Java + 库代码或工具类 + 强调可复用性 / API 设计                                                 | domains/java-stdlib/README.md         |
| **rust-systems**        | Rust + （库 / CLI / parser / 系统编程）                                                 | domains/rust-systems/README.md        |
| **chinese-fiction**     | 中文 + （小说 / 创作 / 叙事 / 散文）                                                         | domains/chinese-fiction/README.md     |
| **skill-design-review** | 审查 / 修订 / 设计 Claude skill 文件本身（SKILL.md / flows / references / domain README）    | domains/skill-design-review/README.md |
| **presentation-deck**   | 单文件 web deck / 投屏分享页 / slides / 演示页 + 单页内 17±5 屏切屏导航（不是滚动长文，不是普通报告，不是 dashboard） | domains/presentation-deck/README.md   |
| **deliberation**        | 日常问题讨论 / 决策 / 取舍分析 / 战略思辨 + 以想清楚为目的、不产出代码或文档工件                                   | domains/deliberation/README.md        |
