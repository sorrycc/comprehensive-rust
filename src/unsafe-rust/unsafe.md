---
minutes: 5
translated_at: '2024-03-26T09:51:10.986Z'
---

# Unsafe Rust

Rust 语言有两个部分：

- **Safe Rust：** 内存安全，不可能出现未定义行为。
- **Unsafe Rust：** 如果违反了前提条件，可能触发未定义行为。

我们在这门课程中看到的主要是 safe Rust，但了解 Unsafe Rust 是很重要的。

Unsafe 代码通常很小并且是孤立的，它的正确性应该被仔细记录。它通常被包裹在一个安全的抽象层中。

Unsafe Rust 为你提供了五个新的能力：

- 解引用原始指针。
- 访问或修改可变静态变量。
- 访问 `union` 字段。
- 调用 `unsafe` 函数，包括 `extern` 函数。
- 实现 `unsafe` 特性。

我们将简要介绍 unsafe 的能力。要了解完整的细节，请查阅 [Rust 书籍的第 19.1 章](https://doc.rust-lang.org/book/ch19-01-unsafe-rust.html) 和 [Rustonomicon](https://doc.rust-lang.org/nomicon/)。

<details>

Unsafe Rust 并不意味着代码是不正确的。它意味着开发者关闭了一些编译器安全特性，并且必须自己编写正确的代码。这意味着编译器不再强制执行 Rust 的内存安全规则。

</details>
