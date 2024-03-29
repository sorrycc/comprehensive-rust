---
minutes: 5
translated_at: '2024-03-26T11:01:39.463Z'
---

# 循环

在 Rust 中有三个循环关键字：`while`、`loop` 和 `for`：

## `while`

[`while` 关键字](https://doc.rust-lang.org/reference/expressions/loop-expr.html#predicate-loops) 的工作机制与其他语言非常相似，只要条件为真，就执行循环体。

```rust,editable
fn main() {
    let mut x = 200;
    while x >= 10 {
        x = x / 2;
    }
    println!("Final x: {x}");
}
```
