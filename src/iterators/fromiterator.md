---
minutes: 5
translated_at: '2024-03-26T10:43:22.826Z'
---

# FromIterator

[`FromIterator`][1] 允许你从一个 [`Iterator`][2] 构建集合。

```rust,editable
fn main() {
    let primes = vec![2, 3, 5, 7];
    let prime_squares = primes.into_iter().map(|p| p * p).collect::<Vec<_>>();
    println!("prime_squares: {prime_squares:?}");
}
```

<details>

`Iterator` 实现了

```rust,ignore
fn collect<B>(self) -> B
where
    B: FromIterator<Self::Item>,
    Self: Sized
```

有两种方法可以为这个方法指定 `B`：

- 使用 “turbofish”：`some_iterator.collect::<COLLECTION_TYPE>()`，就像上面展示的。
  这里使用的 `_` 简写允许 Rust 推断 `Vec` 元素的类型。
- 使用类型推断：`let prime_squares: Vec<_> = some_iterator.collect()`。
  重写示例以使用这种形式。

`FromIterator` 为 `Vec`、`HashMap` 等提供了基本实现。
还有一些更专业的实现，可以让你做一些很酷的事情，
比如将 `Iterator<Item = Result<V, E>>` 转换为 `Result<Vec<V>, E>`。

</details>

[1]: https://doc.rust-lang.org/std/iter/trait.FromIterator.html
[2]: https://doc.rust-lang.org/std/iter/trait.Iterator.html
