---
translated_at: '2024-03-26T11:35:17.045Z'
---

# `buddy_system_allocator`

[`buddy_system_allocator`][1] 是一个第三方 crate，实现了基本的伙伴系统分配器。它既可以用于实现 [`GlobalAlloc`][3] 的 [`LockedHeap`][2]，从而你可以使用标准的 `alloc` crate（正如我们之前看到的[那样][4]），也可以用来分配其他地址空间。例如，我们可能想为 PCI BARs 分配 MMIO 空间：

<!-- mdbook-xgettext: skip -->

```rust,editable,compile_fail
{{#include allocator-example/src/main.rs:main}}
```

<details>

- PCI BARs 的对齐总是等于它们的大小。
- 使用命令 `cargo run` 在 `src/bare-metal/useful-crates/allocator-example/` 下运行示例。（在 Playground 中无法运行，因为存在 crate 依赖。）

</details>

[1]: https://crates.io/crates/buddy_system_allocator
[2]: https://docs.rs/buddy_system_allocator/0.9.0/buddy_system_allocator/struct.LockedHeap.html
[3]: https://doc.rust-lang.org/core/alloc/trait.GlobalAlloc.html
[4]: ../alloc.md
