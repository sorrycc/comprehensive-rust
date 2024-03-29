---
translated_at: '2024-03-26T11:40:10.964Z'
---

# 日志

能够使用 [`log`][1] crate 中的日志宏将会非常好。我们可以通过实现 `Log` 特质来做到这一点。

```rust,editable,compile_fail
{{#include examples/src/logger.rs:main}}
```

<details>

- 在 `log` 中的 unwrap 是安全的，因为我们在调用 `set_logger` 之前初始化了 `LOGGER`。

</details>

[1]: https://crates.io/crates/log
