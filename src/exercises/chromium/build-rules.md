---
translated_at: '2024-03-26T10:53:55.381Z'
---

# 构建规则练习

在你的 Chromium 构建中，向 `//ui/base/BUILD.gn` 添加一个新的 Rust 目标，包含：

```rust
#[no_mangle]
pub extern "C" fn hello_from_rust() {
    println!("Hello from Rust!")
}
```

**重要**：请注意这里的 `no_mangle` 被 Rust 编译器视为一种不安全类型，因此你需要在你的 `gn` 目标中允许不安全代码。

将这个新的 Rust 目标作为 `//ui/base:base` 的依赖项。在 `ui/base/resource/resource_bundle.cc` 的顶部声明这个函数（稍后，我们将看到如何通过绑定生成工具自动化这个过程）：

```cpp
extern "C" void hello_from_rust();
```

从 `ui/base/resource/resource_bundle.cc` 的某个地方调用这个函数 - 我们建议在 `ResourceBundle::MaybeMangleLocalizedString` 的顶部。构建并运行 Chromium，确保多次打印 "Hello from Rust!"。

如果你使用 VSCode，现在在 VSCode 中设置 Rust 以便良好工作。这将在后续练习中非常有用。如果你成功了，你将能够使用右键 "转到定义" 在 `println!` 上。

## 寻找帮助的地方

- [ `rust_static_library` gn 模板][0] 提供的选项
- 关于 [`#[no_mangle]`][1] 的信息
- 关于 [`extern "C"`][2] 的信息
- 关于 gn 的 [`--export-rust-project`][3] 开关的信息
- [如何在 VSCode 中安装 rust-analyzer][4]

<details>
确保学生能够运行此程序非常重要，因为未来的练习将以此为基础。

这个示例是不寻常的，因为它归结为最低公分母的互操作语言 C。C++ 和 Rust 都可以本地声明和调用 C ABI 函数。在课程的后面部分，我们将直接将 C++ 连接到 Rust。

此处需要 `allow_unsafe = true`，因为 `#[no_mangle]` 可能允许 Rust 生成两个具有相同名称的函数，并且 Rust 无法再保证调用的是正确的一个。

如果你需要一个纯 Rust 可执行文件，你也可以使用 `rust_executable` gn 模板实现。

</details>

[0]: https://source.chromium.org/chromium/chromium/src/+/main:build/rust/rust_static_library.gni;l=16

\[1\]: https://doc.rust-lang.org/beta/reference/abi.html#the-no_mangle-attribute
\[2\]: https://doc.rust-lang.org/std/keyword.extern.html
\[3\]: https://gn.googlesource.com/gn/+/main/docs/reference.md#compilation-database
\[4\]: https://code.visualstudio.com/docs/languages/rust
