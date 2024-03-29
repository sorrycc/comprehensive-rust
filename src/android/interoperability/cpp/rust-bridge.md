---
translated_at: '2024-03-26T12:01:46.873Z'
---

# Rust 桥接声明

```rust,ignore
{{#include ../../../../third_party/cxx/book/snippets.rs:rust_bridge}}
```

<details>

- 在 `extern "Rust"` 中声明的条目引用了父模块范围内的条目。
- CXX 代码生成器使用您的 `extern "Rust"` 部分来生成一个包含相应 C++ 声明的 C++ 头文件。生成的头文件与包含桥接的 Rust 源文件具有相同的路径，不同之处在于文件扩展名为 .rs.h。

</details>
