---
translated_at: '2024-03-26T11:34:14.649Z'
---

# `zerocopy`

[`zerocopy`][1] 库（来自 Fuchsia）为安全地在字节序列和其他类型之间转换提供了特征和宏。

```rust,editable,compile_fail
{{#include zerocopy-example/src/main.rs:main}}
```

这不适合于 MMIO（因为它不使用易失性读写），但可以用于处理与硬件共享的结构，例如通过 DMA，或通过某种外部接口发送。

<details>

- `FromBytes` 可以为任何字节模式都有效的类型实现，因此可以安全地从不受信任的字节序列转换。
- 尝试为这些类型派生 `FromBytes` 会失败，因为 `RequestType` 没有将所有可能的 u32 值用作判别符，所以不是所有的字节模式都有效。
- `zerocopy::byteorder` 有意识字节顺序的数字原语类型。
- 在 `src/bare-metal/useful-crates/zerocopy-example/` 下使用 `cargo run` 运行示例。（因为依赖项的原因，不能在 Playground 中运行。）

</details>

[1]: https://docs.rs/zerocopy/
