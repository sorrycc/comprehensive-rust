---
translated_at: '2024-03-26T12:00:49.673Z'
---

# 共享类型

```rust,ignore
{{#include ../../../../third_party/cxx/book/snippets.rs:shared_types}}
```

<details>

- 仅支持 C 风格（单元）枚举。
- 对于在共享类型上使用 `#[derive()]`，支持有限数量的 trait。相应的功能也会为 C++ 代码生成，例如，如果你派生了 `Hash`，也会为对应的 C++ 类型生成一个 `std::hash` 的实现。

</details>
