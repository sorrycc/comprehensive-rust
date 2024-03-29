---
translated_at: '2024-03-26T11:43:20.418Z'
---

# 更多特性

我们已经派生了 `Debug` 特性。实现一些其他特性也会很有用。

```rust,editable,compile_fail
{{#include ../examples/src/pl011_minimal.rs:Traits}}
```

<details>

- 实现 `Write` 使我们能够在我们的 `Uart` 类型上使用 `write!` 和 `writeln!` 宏。
- 在 `src/bare-metal/aps/examples` 下通过 `make qemu_minimal` 运行示例。

</details>
