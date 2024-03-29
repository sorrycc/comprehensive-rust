---
minutes: 8
translated_at: '2024-03-26T10:45:52.568Z'
---

# 特性约束

在使用泛型时，你常常需要要求类型实现某个特性，这样你就可以调用这个特性的方法。

你可以使用 `T: Trait` 或 `impl Trait` 来实现这一点：

```rust,editable
fn duplicate<T: Clone>(a: T) -> (T, T) {
    (a.clone(), a.clone())
}

// struct NotClonable;

fn main() {
    let foo = String::from("foo");
    let pair = duplicate(foo);
    println!("{pair:?}");
}
```

<details>

- 尝试创建一个 `NonClonable` 并将其传递给 `duplicate`。

- 当需要多个特性时，使用 `+` 将它们连接起来。

- 展示一个 `where` 子句，学生在阅读代码时会遇到它。

  ```rust,ignore
  fn duplicate<T>(a: T) -> (T, T)
  where
      T: Clone,
  {
      (a.clone(), a.clone())
  }
  ```

  - 如果你有很多参数，它能让函数签名更清晰。
  - 它具有额外的功能，使其更加强大。
    - 如果有人问，额外的功能是“:`”左边的类型可以是任意的，比如 `Option<T>`。

- 注意 Rust 尚不支持（至今为止）特化。例如，给定原始的 `duplicate` 函数，添加一个专门处理 `duplicate(a: u32)` 的函数是无效的。

</details>
