---
translated_at: '2024-03-26T11:13:24.625Z'
---

# 与 C++ 的互操作性

Rust 社区为 C++/Rust 互操作提供了多种选项，而且一直在开发新的工具。目前，Chromium 使用的工具叫做 CXX。

你可以在接口定义语言中描述整个语言边界（看起来很像 Rust），然后 CXX 工具会为 Rust 和 C++ 中的函数和类型生成声明。

<img src="../android/interoperability/cpp/overview.svg" alt="CXX 概览图，展现了同一个接口定义用来创建 C++ 和 Rust 端的代码，随后通过最少公分母 C API 进行通信">

查看 [CXX 教程][1]，了解使用此工具的完整示例。

[1]: https://cxx.rs/tutorial.html
[2]: https://cxx.rs/bindings.html

<details>

讨论该图表。解释一下，幕后发生的事情和之前你做的是一样的。指出将此过程自动化带来以下好处：

- 该工具保证 C++ 和 Rust 两边匹配（例如，如果 `#[cxx::bridge]` 与实际的 C++ 或 Rust 定义不匹配，你会得到编译错误，但如果是不同步的手工绑定就会得到未定义行为）
- 该工具自动化生成 FFI thunk（小型的、兼容 C-ABI 的免费函数），用于非 C 特性（例如，允许对 Rust 或 C++ 方法进行 FFI 调用；手动绑定需要手工编写这样的顶层免费函数）
- 该工具和库可以处理一组核心类型 - 例如：
  - `&[T]` 可以跨越 FFI 边界传递，尽管它不保证任何特定的 ABI 或内存布局。在手工绑定中，`std::span<T>` / `&[T]` 必须手动解构并重建为指针和长度 - 鉴于每种语言表示空切片的方式略有不同，这是容易出错的
  - 智能指针如 `std::unique_ptr<T>`、`std::shared_ptr<T>` 和/或 `Box` 被原生支持。在手动绑定中，必须传递兼容 C-ABI 的原始指针，这会增加生命周期和内存安全风险
  - `rust::String` 和 `CxxString` 类型理解并维护跨语言的字符串表现形式的差异（例如 `rust::String::lossy` 可以从非 UTF-8 输入构建 Rust 字符串，而 `rust::String::c_str` 可以对字符串进行 NUL 结束）。

</details>
