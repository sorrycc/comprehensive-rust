---
translated_at: '2024-03-26T11:05:45.655Z'
---

# `Send` 和 `Sync`

Rust 是如何知道禁止跨线程共享访问的呢？答案在于两个 trait：

- [`Send`][1]：如果一个类型 `T` 安全地移动到线程边界外是安全的，那么 `T` 就是 `Send`。
- [`Sync`][2]：如果一个类型 `T` 安全地将 `&T` 移动到线程边界外是安全的，那么 `T` 就是 `Sync`。

`Send` 和 `Sync` 是[不安全的 trait][3]。只要你的类型仅包含 `Send` 和 `Sync` 类型，编译器将自动为你的类型推导它们。当你知道这样做是有效的，也可以手动实现它们。

[1]: https://doc.rust-lang.org/std/marker/trait.Send.html
[2]: https://doc.rust-lang.org/std/marker/trait.Sync.html
[3]: ../unsafe/unsafe-traits.md

<details>

- 可以将这些 trait 看作是标记类型具有某些线程安全属性的标记。
- 它们可以像普通 trait 一样在泛型约束中使用。

</details>
