---
translated_at: '2024-03-26T11:44:25.284Z'
---

# Bitflags

[`bitflags`](https://crates.io/crates/bitflags) 包对于处理 bitflags 很有用。

```rust,editable,compile_fail
{{#include ../examples/src/pl011.rs:Flags}}
```

<details>

- `bitflags!` 宏创建了一个类似 `Flags(u16)` 的新类型，同时带有许多方法实现，用于获取和设置标志。

</details>
