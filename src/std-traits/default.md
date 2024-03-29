---
minutes: 5
translated_at: '2024-03-26T10:09:55.621Z'
---

# `Default` 特性

[`Default`][1] 特性为类型生成一个默认值。

```rust,editable
#[derive(Debug, Default)]
struct Derived {
    x: u32,
    y: String,
    z: Implemented,
}

#[derive(Debug)]
struct Implemented(String);

impl Default for Implemented {
    fn default() -> Self {
        Self("John Smith".into())
    }
}

fn main() {
    let default_struct = Derived::default();
    println!("{default_struct:#?}");

    let almost_default_struct =
        Derived { y: "Y is set!".into(), ..Derived::default() };
    println!("{almost_default_struct:#?}");

    let nothing: Option<Derived> = None;
    println!("{:#?}", nothing.unwrap_or_default());
}
```

<details>

- 它可以直接实现，也可以通过 `#[derive(Default)]` 派生。
- 派生的实现将产生一个所有字段都设置为其默认值的值。
  - 这意味着结构体中的所有类型也必须实现 `Default`。
- 标准 Rust 类型通常实现 `Default` 以提供合理的值（例如 `0`、`""` 等）。
- 部分结构体初始化与默认值很好地配合使用。
- Rust 标准库意识到类型可以实现 `Default` 并提供使用它的便利方法。
- `..` 语法称为 [结构体更新语法][2]。

</details>

[1]: https://doc.rust-lang.org/std/default/trait.Default.html
[2]: https://doc.rust-lang.org/book/ch05-01-defining-structs.html#creating-instances-from-other-instances-with-struct-update-syntax
