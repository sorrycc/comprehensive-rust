---
translated_at: '2024-03-26T11:37:31.949Z'
---

# 原始内存映射 I/O

大多数微控制器通过内存映射 I/O 来访问外围设备。让我们尝试在 micro:bit 上点亮一个 LED：

```rust,editable,compile_fail
{{#include examples/src/bin/mmio.rs:Example}}
```

<details>

- GPIO 0 管脚 21 连接到 LED 矩阵的第一列，管脚 28 连接到第一行。

使用以下命令运行示例：

```sh
cargo embed --bin mmio
```

</details>
