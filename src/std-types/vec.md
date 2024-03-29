---
minutes: 10
translated_at: '2024-03-26T10:03:12.527Z'
---

# `Vec`

[`Vec`][1] 是标准的可伸缩堆分配缓冲区：

```rust,editable
fn main() {
    let mut v1 = Vec::new();
    v1.push(42);
    println!("v1: len = {}, capacity = {}", v1.len(), v1.capacity());

    let mut v2 = Vec::with_capacity(v1.len() + 1);
    v2.extend(v1.iter());
    v2.push(9999);
    println!("v2: len = {}, capacity = {}", v2.len(), v2.capacity());

    // 初始化向量并添加元素的规范宏。
    let mut v3 = vec![0, 0, 1, 2, 3, 4];

    // 仅保留偶数元素。
    v3.retain(|x| x % 2 == 0);
    println!("{v3:?}");

    // 删除连续的重复项。
    v3.dedup();
    println!("{v3:?}");
}
```

`Vec` 实现了 [`Deref<Target = [T]>`][2]，这意味着你可以在 `Vec` 上调用切片方法。

[1]: https://doc.rust-lang.org/std/vec/struct.Vec.html
[2]: https://doc.rust-lang.org/std/vec/struct.Vec.html#deref-methods-%5BT%5D

<details>

- `Vec` 是一种集合类型，与 `String` 和 `HashMap` 并列。它包含的数据存储在堆上。这意味着数据量不需要在编译时知道。它可以在运行时增长或收缩。
- 注意 `Vec<T>` 也是一个泛型类型，但你不必显式指定 `T`。如同 Rust 类型推断的通常情况，`T` 在第一次 `push` 调用时已经确定。
- `vec![...]` 是一个替代 `Vec::new()` 的规范宏，它支持向向量添加初始元素。
- 要索引向量，你使用 `[` `]`，但如果越界会引起恐慌。另外，使用 `get` 将返回一个 `Option`。`pop` 函数将移除最后一个元素。
- 第 3 天会讲到切片。现在，学生只需要知道类型为 `Vec` 的值也可以访问所有文档中的切片方法。

</details>
