# 领域:Java 标准库风格的库代码

**适用:** Java 写库代码、工具类、抽象层(rate limiter、cache、connection pool、parser、HTTP client 等),强调可复用性和 API 设计美感。

## 锚点配方

| 维度 | 人名 | facet |
|---|---|---|
| API 设计与不可变 | Joshua Bloch | Effective Java:Builder + 配置即时校验;不可变 record / final class;静态工厂;"让 API 难以被误用";提供 throwing 和 non-throwing 两种 API 变体;Item 71 checked exception 用于可恢复条件 |
| 并发与内存模型 | Brian Goetz | Java Concurrency in Practice:happens-before 契约;锁粒度选择;避免持锁调外部代码;不变量保护策略 |
| 并发原语选择 | Doug Lea | java.util.concurrent:ConcurrentHashMap 的恰当用法;RwLock vs Mutex;读多写少场景的设计取向;lock-free 思维 |
| 测试结构 | Kent Beck | 每个测试 pin 一个不变量,测试名描述行为,不为覆盖率而测;区分 Exhausted(可重试)/ Unsatisfiable(永远不可能);注入式 Clock / Time provider 便于测试 |

## 必要规则

- 产出的 Java 库代码须能编译(默认 Java 17+)
- 不用 boolean 返回掩盖失败原因,必须用结构化异常或 Result 类型
- 单一异常类不塞所有失败类型,每种失败独立异常类 + 结构化字段(retry-after 等)
- 测试禁用 Thread.sleep 作为同步手段,必须用 latch / condvar
- 禁止写同义反复测试(如 `assert(x.isOk() || !x.isOk())`)
