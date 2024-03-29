---
translated_at: '2024-03-26T11:17:42.043Z'
---

## 在 Chromium 中使用 cxx

在 Chromium 中，我们为每个想要使用 Rust 的叶节点定义一个独立的 `#[cxx::bridge] mod`。通常你会为每个 `rust_static_library` 有一个。只需添加

```gn
cxx_bindings = [ "my_rust_file.rs" ]
   # 包含 #[cxx::bridge] 的文件列表，不是所有源文件
allow_unsafe = true
```

到你现有的 `rust_static_library` 目标中，与 `crate_root` 和 `sources` 并列。

C++ 头文件将在合理的位置生成，因此你可以直接

```cpp
#include "ui/base/my_rust_file.rs.h"
```

你将在 `//base` 中找到一些实用函数，用于转换 Chromium C++ 类型和 CXX Rust 类型——比如 [`SpanToRustSlice`][0]。

<details>

学生可能会问——为什么我们仍然需要 `allow_unsafe = true`？

广义上讲，没有任何 C/C++ 代码是“安全的”，按照正常的 Rust 标准。在 Rust 和 C/C++ 之间来回调用可能会对内存做任意的操作，并且破坏 Rust 自身数据布局的安全性。在 C/C++ 互操作中存在 _太多_ `unsafe` 关键字会损害这样一个关键字的信号-噪声比，这是 [有争议的][1]，但严格来说，引入任何外来代码到 Rust 二进制文件都可能从 Rust 的角度导致不期望的行为。

狭义上的答案在 [这个页面][2] 的顶部图表中——在幕后，CXX 生成 Rust `unsafe` 和 `extern "C"` 函数，就像我们在前一节手动做的那样。

</details>

[0]: https://source.chromium.org/chromium/chromium/src/+/main:base/containers/span_rust.h;l=21
[1]: https://steveklabnik.com/writing/the-cxx-debate
[2]: ../interoperability-with-cpp.md
