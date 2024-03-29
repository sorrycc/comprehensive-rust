---
minutes: 3
translated_at: '2024-03-26T10:02:08.668Z'
---

# 编译器 Lints 和 Clippy

Rust 编译器产生的错误消息非常出色，同时还提供了有用的内置 lint。[Clippy](https://doc.rust-lang.org/clippy/) 提供了更多的 lint，这些 lint 被组织到可以按项目启用的组中。

```rust,editable,should_panic
#[deny(clippy::cast_possible_truncation)]
fn main() {
    let x = 3;
    while (x < 70000) {
        x *= 2;
    }
    println!("X 可能适合 u16，对吗？{}", x as u16);
}
```

<details>

运行代码示例并检查错误消息。这里也有 lint 可见，但这些在代码编译后将不会显示。切换到 Playground 网站以显示这些 lint。

解决 lint 之后，在 playground 网站上运行 `clippy` 以显示 clippy 警告。Clippy 有大量其 lint 的文档，并且一直在增加新的 lint（包括默认拒绝的 lint）。

请注意，带有 `help: ...` 的错误或警告可以通过 `cargo fix` 或通过你的编辑器修复。

</details>
