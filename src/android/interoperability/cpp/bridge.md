---
translated_at: '2024-03-26T12:03:29.431Z'
---

# 桥接模块

CXX 依赖于对将要从每种语言暴露给对方的函数签名的描述。您可以使用带有 `#[cxx::bridge]` 属性宏的 Rust 模块中的 extern 块来提供这种描述。

```rust,ignore
{{#include ../../../../third_party/cxx/blobstore/src/main.rs:bridge}}
```

<details>

- 桥接通常在你的箱（crate）中的 `ffi` 模块中声明。
- 从桥接模块中声明的项，CXX 将会生成匹配的 Rust 和 C++ 类型/函数定义，以便将这些项暴露给两种语言。
- 要查看生成的 Rust 代码，可以使用 [cargo-expand] 查看展开的过程宏。对于大多数示例，您将使用 `cargo expand ::ffi` 来只展开 `ffi` 模块（尽管这不适用于 Android 项目）。
- 要查看生成的 C++ 代码，请查看 `target/cxxbridge` 中的内容。

[cargo-expand]: https://github.com/dtolnay/cargo-expand

</details>
