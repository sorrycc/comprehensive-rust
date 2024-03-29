---
minutes: 5
translated_at: '2024-03-26T09:55:56.214Z'
---

# 变量

Rust 通过静态类型提供类型安全。变量绑定使用 `let`：

```rust,editable
fn main() {
    let x: i32 = 10;
    println!("x: {x}");
    // x = 20;
    // println!("x: {x}");
}
```

<details>

- 取消注释 `x = 20` 来演示变量默认是不可变的。添加 `mut` 关键字以允许更改。

- 这里的 `i32` 是变量的类型。这必须在编译时知道，但类型推断（稍后介绍）允许程序员在许多情况下省略它。

</details>
