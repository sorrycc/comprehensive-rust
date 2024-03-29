---
minutes: 5
translated_at: '2024-03-26T10:00:18.727Z'
---

# 模式与解构

在处理元组和其他结构化值时，通常会想要将内部值提取到本地变量中。这可以通过直接访问内部值手动完成：

```rust,editable
fn print_tuple(tuple: (i32, i32)) {
    let left = tuple.0;
    let right = tuple.1;
    println!("left: {left}, right: {right}");
}
```

然而，Rust 也支持使用模式匹配来解构一个较大的值到其组成部分：

```rust,editable
fn print_tuple(tuple: (i32, i32)) {
    let (left, right) = tuple;
    println!("left: {left}, right: {right}");
}
```

<details>

- 这里使用的模式是“无可辩驳的”，意味着编译器可以静态验证等号右侧的值与模式具有相同的结构。
- 变量名是一个无可辩驳的模式，总是匹配任意值，因此我们也可以使用 `let` 来声明单一变量。
- Rust 也支持在条件语句中使用模式，允许在相同时间进行等值比较和解构。这种形式的模式匹配将在后面更详细地讨论。
- 编辑上面的示例，展示当模式与被匹配的值不符时编译器报错。

</details>
