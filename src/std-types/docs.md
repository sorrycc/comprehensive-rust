---
minutes: 5
translated_at: '2024-03-26T10:06:55.630Z'
---

# 文档

Rust 拥有丰富的文档资料。例如：

- 有关 [循环](https://doc.rust-lang.org/stable/reference/expressions/loop-expr.html) 的所有细节。
- 原始类型，如 [`u8`](https://doc.rust-lang.org/stable/std/primitive.u8.html)。
- 标准库类型，如 [`Option`](https://doc.rust-lang.org/stable/std/option/enum.Option.html) 或 [`BinaryHeap`](https://doc.rust-lang.org/stable/std/collections/struct.BinaryHeap.html)。

实际上，你可以给自己的代码编写文档：

```rust,editable
/// 确定第一个参数是否能被第二个参数整除。
///
/// 如果第二个参数为零，则结果为假。
fn is_divisible_by(lhs: u32, rhs: u32) -> bool {
    if rhs == 0 {
        return false;
    }
    lhs % rhs == 0
}
```

内容被视为 Markdown 格式。所有发布的 Rust 库包都会在 [`docs.rs`](https://docs.rs) 上自动使用 [rustdoc](https://doc.rust-lang.org/rustdoc/what-is-rustdoc.html) 工具生成文档。习惯上，会使用这种模式记录 API 中所有公共项的文档。

要从条目内部（例如在模块内）记录条目，请使用 `//!` 或 `/*! .. */`，称为“内部文档注释”：

```rust,editable
//! 本模块包含与整数可除性相关的功能。
```

<details>

- 为学生展示 `rand` 包生成的文档，网址为 <https://docs.rs/rand>。

</details>
