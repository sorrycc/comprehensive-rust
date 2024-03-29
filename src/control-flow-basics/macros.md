---
minutes: 2
translated_at: '2024-03-26T11:01:26.470Z'
---

# 宏

宏会在编译期间展开成 Rust 代码，可以接收变化的参数数量。它们通过结尾的 `!` 来区分。Rust 标准库包括了一系列有用的宏。

- `println!(format, ..)` 将一行内容打印到标准输出，应用在 [`std::fmt`](https://doc.rust-lang.org/std/fmt/index.html) 中描述的格式化。
- `format!(format, ..)` 的工作方式与 `println!` 相同，但它返回结果为一个字符串。
- `dbg!(expression)` 记录表达式的值并返回它。
- `todo!()` 标记一段代码为尚未实现。如果执行，它会 panic。
- `unreachable!()` 标记一段代码为不可达。如果执行，它会 panic。

```rust,editable
fn factorial(n: u32) -> u32 {
    let mut product = 1;
    for i in 1..=n {
        product *= dbg!(i);
    }
    product
}

fn fizzbuzz(n: u32) -> u32 {
    todo!()
}

fn main() {
    let n = 4;
    println!("{n}! = {}", factorial(n));
}
```

<details>

本节的要点是这些常见的便利工具存在，以及如何使用它们。它们为什么被定义为宏，以及它们展开成什么，不是特别关键。

本课程不涵盖定义宏，但后续章节将描述 derive 宏的使用。

</details>
