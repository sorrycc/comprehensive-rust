---
translated_at: '2024-03-26T11:44:11.838Z'
---

# 驱动

现在让我们在我们的驱动中使用新的 `Registers` 结构体。

```rust,editable,compile_fail
{{#include ../examples/src/pl011.rs:Uart}}
```

<details>

- 注意使用 `addr_of!` / `addr_of_mut!` 来获取指向各个字段的指针，而不创建中间引用，这将是不稳定的。

</details>
