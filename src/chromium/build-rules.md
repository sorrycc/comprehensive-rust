---
translated_at: '2024-03-26T11:14:56.155Z'
---

# 构建规则

Rust 代码通常使用 `cargo` 进行构建。出于效率考虑，Chromium 使用 `gn` 和 `ninja` 构建 --- 其静态规则允许最大并行性。Rust 也不例外。

## 在 Chromium 中添加 Rust 代码

在某个已有的 Chromium `BUILD.gn` 文件中，声明一个 `rust_static_library`：

```gn
import("//build/rust/rust_static_library.gni")

rust_static_library("my_rust_lib") {
  crate_root = "lib.rs"
  sources = [ "lib.rs" ]
}
```

你也可以添加 `deps` 来依赖其他 Rust 目标。稍后我们将使用它来依赖第三方代码。

<details>

你必须同时指定 _crate root_ 和完整的源文件列表。`crate_root` 是提供给 Rust 编译器的文件，代表编译单元的根文件 --- 通常是 `lib.rs`。`sources` 是所有源文件的完整列表，`ninja` 需要它来确定何时需要重建。

(Rust 中没有所谓的 `source_set`，因为在 Rust 中，一整个包（crate）就是一个编译单元。`static_library` 是最小的单位。)

学生们可能在想，为什么我们需要一个 gn 模板，而不是使用 [gn 对 Rust 静态库的内置支持][0]。答案是这个模板为 CXX 互操作、Rust 功能和单元测试提供了支持，我们稍后将会用到这些功能。

</details>

[0]: https://gn.googlesource.com/gn/+/main/docs/reference.md#func_static_library
