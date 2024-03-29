---
minutes: 5
translated_at: '2024-03-26T10:46:20.551Z'
---

# `impl Trait`

与 trait 约束类似，可在函数参数和返回值中使用 `impl Trait` 语法：

```rust,editable
// 语法糖等同于：
//   fn add_42_millions<T: Into<i32>>(x: T) -> i32 {
fn add_42_millions(x: impl Into<i32>) -> i32 {
    x.into() + 42_000_000
}

fn pair_of(x: u32) -> impl std::fmt::Debug {
    (x + 1, x - 1)
}

fn main() {
    let many = add_42_millions(42_i8);
    println!("{many}");
    let many_more = add_42_millions(10_000_000);
    println!("{many_more}");
    let debuggable = pair_of(27);
    println!("可以调试的：{debuggable:?}");
}
```

<details>

`impl Trait` 允许你操作无法命名的类型。`impl Trait` 在不同位置的含义有所不同。

- 对于参数，`impl Trait` 像是一个具有 trait 约束的匿名泛型参数。

- 对于返回类型，这意味着返回类型是某个实现了该 trait 的具体类型，但不命名该类型。当你不希望在公共 API 中暴露具体类型时，这非常有用。

  在返回位置进行类型推断是困难的。一个返回 `impl Foo` 的函数选择它返回的具体类型，而无需在源代码中书写。一个返回泛型类型如 `collect<B>() -> B` 的函数可以返回任何满足 `B` 的类型，调用者可能需要选择一个，例如使用 `let x: Vec<_> = foo.collect()` 或者使用 turbofish, `foo.collect::<Vec<_>>()`。

`debuggable` 的类型是什么？尝试使用 `let debuggable: () = ..` 来查看错误信息显示。

</details>
