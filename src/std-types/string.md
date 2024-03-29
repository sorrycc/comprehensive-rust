---
minutes: 10
translated_at: '2024-03-26T10:03:53.815Z'
---

# 字符串

[`String`][1] 是标准的堆分配的可增长 UTF-8 字符串缓冲区：

```rust,editable
fn main() {
    let mut s1 = String::new();
    s1.push_str("Hello");
    println!("s1: len = {}, capacity = {}", s1.len(), s1.capacity());

    let mut s2 = String::with_capacity(s1.len() + 1);
    s2.push_str(&s1);
    s2.push('!');
    println!("s2: len = {}, capacity = {}", s2.len(), s2.capacity());

    let s3 = String::from("🇨🇭");
    println!("s3: len = {}, number of chars = {}", s3.len(), s3.chars().count());
}
```

`String` 实现了 [`Deref<Target = str>`][2]，这意味着你可以在 `String` 上调用所有 `str` 方法。

[1]: https://doc.rust-lang.org/std/string/struct.String.html
[2]: https://doc.rust-lang.org/std/string/struct.String.html#deref-methods-str

<details>

- `String::new` 返回一个新的空字符串，当你知道想要添加多少数据到字符串时，使用 `String::with_capacity`。
- `String::len` 返回 `String` 的大小（以字节为单位），这和它的字符长度可能不同。
- `String::chars` 返回一个实际字符的迭代器。注意，一个 `char` 和人类认为的“字符”可能不同，这是由于[字素簇](https://docs.rs/unicode-segmentation/latest/unicode_segmentation/struct.Graphemes.html)。
- 当人们谈论字符串时，他们可能指的是 `&str` 或 `String`。
- 当类型实现了 `Deref<Target = T>` 时，编译器会让你无障碍地调用 `T` 的方法。
  - 我们还没有讨论过 `Deref` 特性，所以在这一点上，这主要解释了文档旁边栏的结构。
  - `String` 实现了 `Deref<Target = str>`，这让它可以透明地访问 `str` 的方法。
  - 写下并比较 `let s3 = s1.deref();` 和 `let s3 = &*s1;`。
- `String` 被实现为一个字节向量的封装，许多你在向量上看到的操作也支持在 `String` 上，但是有一些额外的保证。
- 比较不同的索引 `String` 的方法：

```markdown
  - 通过使用 `s3.chars().nth(i).unwrap()` 来访问字符，其中 `i` 为界内或界外。
  - 通过使用 `s3[0..4]` 来访问子字符串，无论该切片是否在字符边界上。
- 许多类型可以使用 [`to_string`](https://doc.rust-lang.org/std/string/trait.ToString.html#tymethod.to_string) 方法转换为字符串。这个特性会自动为所有实现了 `Display` 的类型实现，因此任何可以格式化的东西也都可以被转换为字符串。

</details>
```
