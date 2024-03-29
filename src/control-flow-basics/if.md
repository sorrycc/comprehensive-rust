---
minutes: 4
translated_at: '2024-03-26T11:02:01.585Z'
---

# `if` 表达式

你可以像在其他语言中使用 `if` 语句一样使用 [`if` 表达式](https://doc.rust-lang.org/reference/expressions/if-expr.html#if-expressions)：

```rust,editable
fn main() {
    let x = 10;
    if x == 0 {
        println!("zero!");
    } else if x < 100 {
        println!("biggish");
    } else {
        println!("huge");
    }
}
```

此外，你可以将 `if` 用作表达式。每个块的最后一个表达式会成为 `if` 表达式的值：

```rust,editable
fn main() {
    let x = 10;
    let size = if x < 20 { "small" } else { "large" };
    println!("number size: {}", size);
}
```

<details>

因为 `if` 是一个表达式并且必须具有特定的类型，所以其分支块必须具有相同的类型。尝试在第二个例子中的 `"small"` 后面添加 `;` 来看看会发生什么。

当 `if` 用于表达式时，表达式必须有一个 `;` 来将其与下一个语句分隔。尝试移除 `println!` 前的 `;` 来查看编译器错误。

</details>
