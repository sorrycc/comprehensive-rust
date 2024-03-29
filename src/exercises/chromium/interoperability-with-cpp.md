---
translated_at: '2024-03-26T10:52:51.597Z'
---

# 练习：与 C++ 的互操作性

## 第一部分

- 在你之前创建的 Rust 文件中，添加一个 `#[cxx::bridge]`，它指定了一个单独的函数，将从 C++ 中调用，名为 `hello_from_rust`，不接受任何参数，也不返回任何值。
- 修改你之前的 `hello_from_rust` 函数，去除 `extern "C"` 和 `#[no_mangle]`。这现在只是一个标准的 Rust 函数。
- 修改你的 `gn` 目标来构建这些绑定。
- 在你的 C++ 代码中，移除对 `hello_from_rust` 的前向声明。相反，包含生成的头文件。
- 构建并运行！

## 第二部分

稍微玩玩 CXX 是个好主意。它帮助你思考 Rust 在 Chromium 中实际上有多灵活。

一些尝试的事情：

- 从 Rust 回调到 C++。你将需要：
  - 一个额外的头文件，你可以从你的 `cxx::bridge` 中 `include!`。你需要在这个新的头文件中声明你的 C++ 函数。
  - 一个 `unsafe` 块来调用这样的函数，或者在你的 `#[cxx::bridge]` 中指定 `unsafe` 关键字[如此处所述][0]。
  - 你可能还需要包含 `#include "third_party/rust/cxx/v1/crate/include/cxx.h"`
- 从 C++ 传递一个 C++ 字符串到 Rust。
- 传递一个对 C++ 对象的引用到 Rust。
- 故意使 Rust 函数签名与 `#[cxx::bridge]` 不匹配，并习惯于你看到的错误。
- 故意使 C++ 函数签名与 `#[cxx::bridge]` 不匹配，并习惯于你看到的错误。
- 从 C++ 传递一个某种类型的 `std::unique_ptr` 到 Rust，使 Rust 拥有一些 C++ 对象。
- 创建一个 Rust 对象并将其传入 C++，使 C++ 拥有它。（提示：你需要一个 `Box`）。
- 在一个 C++ 类型上声明一些方法。从 Rust 调用它们。
- 在一个 Rust 类型上声明一些方法。从 C++ 调用它们。

## 第三部分

现在你理解了 CXX 互操作的优势和局限性，思考在 Chromium 中使用 Rust 的一些用例，其中接口将是足够简单的。勾勒出你可能定义那个接口的方式。

## 在哪里寻找帮助

- [`cxx` 绑定参考][1]
- [`rust_static_library` gn 模板][2]

<details>
随着学生探索第二部分，他们必将对如何实现这些目标，以及 CXX 如何在幕后工作产生许多问题。

你可能遇到的一些问题：

- 我在用类型 Y 初始化类型 X 的变量时遇到了问题，其中 X 和 Y 都是函数类型。这是因为你的 C++ 函数与你的 `cxx::bridge` 中的声明不完全匹配。
- 我似乎可以自由地将 C++ 引用转换为 Rust 引用。这难道不会冒险产生 UB 吗？对于 CXX 的 _不透明_ 类型，没有，因为它们是零大小的。对于 CXX 的平凡类型是的，_可能_ 会造成 UB，尽管 CXX 的设计使得构造这样的例子变得相当困难。

</details>

[0]: https://cxx.rs/extern-c++.html#functions-and-member-functions
[1]: https://cxx.rs/bindings.html
[2]: https://source.chromium.org/chromium/chromium/src/+/main:build/rust/rust_static_library.gni;l=16
