---
translated_at: '2024-03-26T11:43:47.572Z'
---

# 使用它

让我们编写一个小程序，使用我们的驱动程序来向串行控制台写入数据，并
回显接收到的字节。

```rust,editable,compile_fail
{{#include ../examples/src/main_improved.rs:main}}
```

<details>

- 如同[内联汇编](../inline-assembly.md)示例中所展示的，这个 `main`
  函数是从我们的入口点代码 `entry.S` 中调用的。具体详情请参见那里的讲义笔记。
- 在 `src/bare-metal/aps/examples` 下运行 `make qemu` 命令来在 QEMU 中运行示例。

</details>
