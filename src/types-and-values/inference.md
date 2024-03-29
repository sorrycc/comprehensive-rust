---
minutes: 3
translated_at: '2024-03-26T09:56:57.489Z'
---

# 类型推断

Rust 会根据变量的 _使用_ 来确定类型：

<!-- mdbook-xgettext: skip -->

```rust,editable
fn takes_u32(x: u32) {
    println!("u32: {x}");
}

fn takes_i8(y: i8) {
    println!("i8: {y}");
}

fn main() {
    let x = 10;
    let y = 20;

    takes_u32(x);
    takes_i8(y);
    // takes_u32(y);
}
```

<details>

本幻灯片展示了 Rust 编译器如何根据变量声明和使用给出的约束来推断类型。

非常重要的一点是要强调，像这样声明的变量并不是某种能够保存任何数据的动态“任意类型”。通过这样的声明生成的机器代码与显式声明类型的代码是相同的。编译器帮我们完成了这项工作，并帮助我们编写更简洁的代码。

当没有东西限制整数字面量的类型时，Rust 默认为 `i32`。这有时会在错误消息中显示为 `{integer}`。同样，浮点数字面量默认为 `f64`。

```rust,compile_fail
fn main() {
    let x = 3.14;
    let y = 20;
    assert_eq!(x, y);
    // 错误：没有为 `{float} == {integer}` 实现
}
```

</details>
