---
translated_at: '2024-03-26T11:44:01.679Z'
---

# 多个寄存器

我们可以使用一个结构体来代表 UART 寄存器的内存布局。

```rust,editable,compile_fail
{{#include ../examples/src/pl011.rs:Registers}}
```

<details>

- [`#[repr(C)]`](https://doc.rust-lang.org/reference/type-layout.html#the-c-representation)
  告诉编译器按照顺序放置结构体字段，遵循与 C 相同的规则。这对于我们的结构体来说是必须的，因为它需要有一个可预测的布局，而默认的 Rust 表示允许编译器自行决定如何（在其他事情中）重新排列字段。

</details>
