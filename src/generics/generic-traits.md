---
Minutes: 5
translated_at: '2024-03-26T10:46:46.568Z'
---

# 泛型 Traits

Traits 也可以是泛型的，就像类型和函数一样。当使用 trait 时，其参数会获得具体的类型。

```rust,editable
#[derive(Debug)]
struct Foo(String);

impl From<u32> for Foo {
    fn from(from: u32) -> Foo {
        Foo(format!("Converted from integer: {from}"))
    }
}

impl From<bool> for Foo {
    fn from(from: bool) -> Foo {
        Foo(format!("Converted from bool: {from}"))
    }
}

fn main() {
    let from_int = Foo::from(123);
    let from_bool = Foo::from(true);
    println!("{from_int:?}, {from_bool:?}");
}
```

<details>

- `From` trait 将在课程后面详细讲解，但其在 `std` 文档中的[定义](https://doc.rust-lang.org/std/convert/trait.From.html)很简单。

- Trait 的实现不需要覆盖所有可能的类型参数。这里，`Foo::From("hello")` 将无法编译，因为没有为 `Foo` 实现 `From<&str>`。

- 泛型 traits 以类型作为“输入”，而关联类型则是一种“输出类型”。一个 trait 可以针对不同的输入类型有多个实现。

- 实际上，Rust 要求对于任何类型 T 最多只能匹配一个 trait 的实现。与一些其他语言不同，Rust 没有选择“最具体”匹配的启发式规则。正在努力添加这种支持，称为[特化](https://rust-lang.github.io/rfcs/1210-impl-specialization.html)。

</details>
