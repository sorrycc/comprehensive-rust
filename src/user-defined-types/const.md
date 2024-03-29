---
translated_at: '2024-03-26T09:50:25.502Z'
---

# `const`

常量在编译时被求值，它们的值在被使用的地方内联：

<!-- mdbook-xgettext: skip -->

```rust,editable
const DIGEST_SIZE: usize = 3;
const ZERO: Option<u8> = Some(42);

fn compute_digest(text: &str) -> [u8; DIGEST_SIZE] {
    let mut digest = [ZERO.unwrap_or(0); DIGEST_SIZE];
    for (idx, &b) in text.as_bytes().iter().enumerate() {
        digest[idx % DIGEST_SIZE] = digest[idx % DIGEST_SIZE].wrapping_add(b);
    }
    digest
}

fn main() {
    let digest = compute_digest("Hello");
    println!("digest: {digest:?}");
}
```

根据 [Rust RFC Book][1]，这些在使用时被内联。

只有标记为 `const` 的函数可以在编译时调用以生成 `const` 值。然而，`const` 函数可以在运行时被调用。

<details>

- 提到 `const` 在语义上类似于 C++ 的 `constexpr`
- 一个人需要在运行时求值的常量并不是很常见，但这样做有助于安全，比使用静态更好。

</details>

[1]: https://rust-lang.github.io/rfcs/0246-const-vs-static.html
