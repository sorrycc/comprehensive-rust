---
minutes: 5
translated_at: '2024-03-26T09:57:33.665Z'
---

# 你好，世界

让我们来看看最简单的 Rust 程序，一个经典的 Hello World 程序：

```rust,editable
fn main() {
    println!("Hello 🌍!");
}
```

你所看到的：

- 函数以 `fn` 开头。
- 块由花括号分隔，就像在 C 和 C++ 中一样。
- `main` 函数是程序的入口点。
- Rust 拥有卫生宏（hygienic macros），`println!` 就是一个例子。
- Rust 字符串是 UTF-8 编码的，可以包含任何 Unicode 字符。

<details>

此幻灯片试图让学生们对 Rust 代码感到舒服。接下来的四天里他们会看到大量的它，因此我们从熟悉的东西开始小步走。

关键点：

- Rust 在很大程度上像 C/C++/Java 传统中的其他语言。它是命令式的，并且除非绝对必要，否则不试图重新发明东西。

- Rust 是现代的，对诸如 Unicode 之类的事物提供全面支持。

- Rust 在你想要有可变数量的参数的情况下使用宏（没有函数[重载](../control-flow-basics/functions.md)）。

- 宏是“卫生的”意味着它们不会意外捕获它们所用范围内的标识符。实际上，Rust 宏只是[部分卫生的](https://veykril.github.io/tlborm/decl-macros/minutiae/hygiene.html)。

- Rust 是多范式的。例如，它具有强大的[面向对象编程特性](https://doc.rust-lang.org/book/ch17-00-oop.html)，而且，虽然它不是一种函数式语言，它包括一系列的[函数式概念](https://doc.rust-lang.org/book/ch13-00-functional-features.html)。

</details>
