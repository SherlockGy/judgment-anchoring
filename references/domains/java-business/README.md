# 领域:Java 业务服务

**适用:** Java 写业务服务(订单、支付、库存、会员、退款、积分等),涉及状态机、事务、幂等、第三方依赖。

## 锚点配方

| 维度 | 人名 | facet |
|---|---|---|
| 业务建模 | Eric Evans | DDD:核心业务建模为有不变量的聚合根;状态变更走显式状态机(enum + 显式转移);不变量封装在聚合根/仓储上不散落 service;不变量违反明确表达为领域异常 |
| API 与异常分层 | Joshua Bloch | Effective Java:checked 用于业务可恢复失败,unchecked 用于程序员错误;不可变 DTO、Builder;"让 API 难以被误用";异常类型分层(业务/系统/第三方独立类型) |
| 错误结构化(映射到 Java) | BurntSushi 风格(显式跨生态映射\*) | 错误必须告诉调用方"什么 key、在哪一层、什么时候"出了什么事;retry 信号是异常的结构化字段而非 message 字符串 |
| 边界与失败模式 | Kyle Kingsbury (Jepsen) | 主动思考"第三方 timeout / 两个请求并发 / 第三方说成功但其实没到账",这些边界写成显式代码路径;不变量保护放在锁内,第三方调用放在锁外 |

> \* **跨生态说明:** BurntSushi 原是 Rust 生态(ripgrep / walkdir),但其"结构化错误"哲学在 Java 里有直接对应(异常类型 + 字段)。本条是 `anti-patterns.md` 锚点检验「维度对口」(跨生态)的**显式映射例外**。

## 必要规则

- 产出的 Java 代码须能编译(默认 Java 17+,可用 record / sealed / pattern matching)
- 业务方法不用 boolean 返回掩盖失败,必须用结构化异常或 Result 类型
- 同一业务字段不能在聚合根和子实体上双写,避免 UNKNOWN 状态下的超额漏洞
- 第三方调用的异常必须保留 cause 链,不能 catch 后 stringify 成新异常丢掉结构化信息
