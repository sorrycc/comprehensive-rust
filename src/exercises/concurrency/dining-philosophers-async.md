---
translated_at: '2024-03-26T10:50:19.092Z'
---

# 哲学家就餐问题 --- 异步

请查看[哲学家就餐问题](dining-philosophers.md)获取问题的描述。

像之前一样，你需要本地的 [Cargo 安装](../../cargo/running-locally.md) 来做这个练习。复制下面的代码到一个名为 `src/main.rs` 的文件中，填写空白处，并且测试运行 `cargo run` 时不会发生死锁：

<!-- 文件 src/main.rs -->

```rust,compile_fail
{{#include dining-philosophers-async.rs:Philosopher}}
    // left_fork: ...
    // right_fork: ...
    // thoughts: ...
}

{{#include dining-philosophers-async.rs:Philosopher-think}}

{{#include dining-philosophers-async.rs:Philosopher-eat}}
{{#include dining-philosophers-async.rs:Philosopher-eat-body}}
{{#include dining-philosophers-async.rs:Philosopher-eat-end}}
    // 创建叉子

    // 创建哲学家

    // 让他们思考和进餐

    // 输出他们的想法
}
```

由于这次你使用的是异步 Rust，你需要一个 `tokio` 依赖。你可以使用下面的 `Cargo.toml`：

<!-- 文件 Cargo.toml -->

```toml
[package]
name = "dining-philosophers-async-dine"
version = "0.1.0"
edition = "2021"

[dependencies]
tokio = { version = "1.26.0", features = ["sync", "time", "macros", "rt-multi-thread"] }
```

还要注意，这次你必须使用 `tokio` 包中的 `Mutex` 和 `mpsc` 模块。

<details>

- 你能让你的实现变为单线程的吗？

</details>
