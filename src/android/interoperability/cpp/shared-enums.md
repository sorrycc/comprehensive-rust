---
translated_at: '2024-03-26T12:01:16.719Z'
---

# 共享枚举

```rust,ignore
{{#include ../../../../third_party/cxx/book/snippets.rs:shared_enums_bridge}}
```

生成的 Rust 代码：

```rust
{{#include ../../../../third_party/cxx/book/snippets.rs:shared_enums_rust}}
```

生成的 C++ 代码：

```c++
{{#include ../../../../third_party/cxx/book/snippets.cc:shared_enums_cpp}}
```

<details>

- 在 Rust 端，为共享枚举生成的代码实际上是一个包装了数值的结构体。这是因为在 C++ 中，枚举类持有与所有列出的变体不同的值并不是 UB（未定义行为），而我们的 Rust 表示需要具有相同的行为。

</details>
