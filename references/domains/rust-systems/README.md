# 领域:Rust 系统编程

**适用:** Rust 写系统级代码(库、CLI、parser、协议实现、限流器、tracer 等),强调零成本抽象、错误显式、所有权清晰。

## 锚点配方

| 维度 | 人名 | facet |
|---|---|---|
| 错误结构化 | BurntSushi (ripgrep, walkdir) | 错误是 enum + 结构化字段;错误必须告诉调用方"什么 / 哪 / 何时";区分 Exhausted(可重试)和 Unsatisfiable(永远不可能);retry 信号通过子类型表达而非 message 字符串 |
| API 设计与 trait 层次 | dtolnay (serde, thiserror, anyhow) | trait 层次的简洁性;`Borrow<Q>` 模式让热路径不 clone;库代码用 thiserror 哲学(结构化错误),应用代码用 anyhow 哲学(context-rich) |
| 并发与锁粒度 | jonhoo / Jon Gjengset | 避免一把大锁锁所有 key;双层锁如 `RwLock<HashMap<K, Mutex<Bucket>>>` 让 per-key 不互相阻塞;思考读写比和争用模式;注释里主动承认 trade-off |
| 测试结构 | matklad (rust-analyzer) | 只测真正不平凡的行为,不为覆盖率而测;每个测试 pin 一个清晰的不变量;测试用 latch / condvar 而不是 sleep |

## 必要规则

- 产出的 Rust 代码须能 `cargo build` 无 warnings
- 错误不能 stringify(如 `reqwest::Error` 不拍扁成 String),必须保留原始类型链让调用方可以 `.is_timeout()` / `.status()`
- 不过度泛型(不为"灵活"写 5 层泛型嵌套破坏可读性)
- 不写同义反复测试(如 `assert!(x.is_ok() || x.is_err())`)
- 测试禁用 sleep 同步,用 latch / condvar
