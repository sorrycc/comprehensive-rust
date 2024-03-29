---
translated_at: '2024-03-26T12:01:30.026Z'
---

# Rust 错误处理

```rust,ignore
{{#include ../../../../third_party/cxx/book/snippets.rs:rust_result}}
```

<details>

- 返回 `Result` 的 Rust 函数在 C++ 端会被转换为异常。
- 抛出的异常总是 `rust::Error` 类型的，它主要提供了获取错误消息字符串的方式。错误消息将来源于错误类型的 `Display` 实现。
- 从 Rust 向 C++ 解开的 panic 会导致进程立即终止。

</details>
