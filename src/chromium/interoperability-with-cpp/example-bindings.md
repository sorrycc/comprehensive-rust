---
translated_at: '2024-03-26T11:18:25.370Z'
---

# 示例绑定

CXX 要求在 `.rs` 源代码文件内的 `cxx::bridge` 模块中声明整个 C++/Rust 边界。

```rust,ignore
{{#include ../../../third_party/cxx/book/snippets.rs:cxx_overview}}
```

<details>

指出：

- 虽然这看起来像一个常规的 Rust `mod`，但 `#[cxx::bridge]` 过程宏对它进行了复杂的处理。生成的代码要复杂得多 - 尽管这确实在你的代码中生成了一个名为 `ffi` 的 `mod`。
- Rust 中对 C++ 的 `std::unique_ptr` 的原生支持
- C++ 中对 Rust 切片的原生支持
- 从 C++ 调用 Rust，以及 Rust 类型（在顶部部分）
- 从 Rust 调用 C++，以及 C++ 类型（在底部部分）

**常见误解**：它 _看起来_ 像是 Rust 正在解析一个 C++ 头文件，但这是误导。这个头文件从未被 Rust 解释，而只是在生成的 C++ 代码中被 `#include`，以便于 C++ 编译器使用。

</details>
