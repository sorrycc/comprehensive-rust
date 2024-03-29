---
translated_at: '2024-03-26T10:49:46.164Z'
---

# 哲学家就餐问题

哲学家就餐问题是并发中的一个典型问题：

> 五位哲学家共同在同一张桌子上就餐。每位哲学家都有自己在桌上的位置。每个盘子之间都放着一把叉子。上的是一种需要用两把叉子吃的意大利面。每位哲学家只能交替地思考和吃饭。此外，一位哲学家只有在手里拿着左边和右边的叉子时才能吃他的意大利面。因此，两把叉子只有当它们两边最近的邻居都在思考、没有在吃饭时才可用。一个哲学家吃完后，他们会放下两把叉子。

你将需要本地的 [Cargo 安装](../../cargo/running-locally.md) 来完成这个练习。将下面的代码复制到一个名为 `src/main.rs` 的文件中，填写空白处，并测试 `cargo run` 不会导致死锁：

<!-- 文件 src/main.rs -->

```rust,compile_fail
{{#include dining-philosophers.rs:Philosopher}}
    // left_fork: ...
    // right_fork: ...
    // thoughts: ...
}

{{#include dining-philosophers.rs:Philosopher-think}}

{{#include dining-philosophers.rs:Philosopher-eat}}
        // 拿起叉子...
{{#include dining-philosophers.rs:Philosopher-eat-end}}
    // 创建叉子

    // 创建哲学家

    // 使他们每人思考和吃饭 100 次

    // 输出他们的思考
}
```

你可以使用下面的 `Cargo.toml`：

<!-- 文件 Cargo.toml -->

```toml
[package]
name = "dining-philosophers"
version = "0.1.0"
edition = "2021"
```
