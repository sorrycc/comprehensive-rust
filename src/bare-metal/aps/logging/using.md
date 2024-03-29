---
translated_at: '2024-03-26T11:43:27.711Z'
---

# 使用它

我们需要在使用它之前初始化日志记录器。

```rust, 编辑, 编译失败
{{#include ../examples/src/main_logger.rs:main}}
```

<details>

- 注意，我们的 panic 处理程序现在可以记录 panic 的详细信息了。
- 在 `src/bare-metal/aps/examples` 下，使用 `make qemu_logger` 运行示例。

</details>
