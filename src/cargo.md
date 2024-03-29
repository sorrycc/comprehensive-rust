---
translated_at: '2024-03-26T09:41:25.925Z'
---

# 使用 Cargo

当你开始阅读 Rust 相关的资料时，你很快就会遇到 [Cargo](https://doc.rust-lang.org/cargo/)，这是 Rust 生态系统中用来构建和运行 Rust 应用程序的标准工具。在这里我们想简要介绍一下 Cargo 是什么，以及它如何融入更广泛的生态系统和本培训中。

## 安装

> **请按照 <https://rustup.rs/> 上的说明进行操作。**

这将为你提供 Cargo 构建工具（`cargo`）和 Rust 编译器（`rustc`）。你还会得到 `rustup`，一个命令行实用程序，你可以使用它来安装不同版本的编译器。

安装 Rust 之后，你应该配置你的编辑器或 IDE 来兼容 Rust。大多数编辑器通过对话 [rust-analyzer] 来实现这一点，为 [VS Code]、[Emacs]、[Vim/Neovim] 等提供自动补全和跳转到定义的功能。还有另一个叫做 [RustRover] 的不同 IDE 可用。

<details>

- 在 Debian/Ubuntu 上，你也可以通过 `apt` 安装 Cargo、Rust 源代码和 [Rust 格式化工具]。但是，这会让你得到一个过时的 rust 版本，并可能导致意外的行为。命令如下：

  ```shell
  sudo apt install cargo rust-src rustfmt
  ```

</details>

[rust-analyzer]: https://rust-analyzer.github.io/
[VS Code]: https://code.visualstudio.com/
[Emacs]: https://rust-analyzer.github.io/manual.html#emacs
[Vim/Neovim]: https://rust-analyzer.github.io/manual.html#vimneovim
[RustRover]: https://www.jetbrains.com/rust/
[Rust 格式化工具]: https://github.com/rust-lang/rustfmt
