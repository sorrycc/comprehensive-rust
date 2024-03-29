---
translated_at: '2024-03-26T12:02:30.134Z'
---

# C++ 错误处理

```rust,ignore
{{#include ../../../../third_party/cxx/book/snippets.rs:cpp_exception}}
```

<details>

- 声明为返回 `Result` 的 C++ 函数会捕获在 C++ 侧抛出的任何异常，并将其作为 `Err` 值返回给调用 Rust 函数。
- 如果从一个 extern "C++" 函数中抛出异常，而该函数没有通过 CXX 桥接声明为返回 `Result`，程序将调用 C++ 的 `std::terminate`。此行为等同于通过 `noexcept` C++ 函数抛出相同的异常。

</details>
