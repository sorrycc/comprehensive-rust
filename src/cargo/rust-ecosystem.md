---
translated_at: '2024-03-26T11:26:04.373Z'
---

# Rust 生态系统

Rust 生态系统由许多工具组成，主要的有：

- `rustc`：Rust 编译器，可以将 `.rs` 文件编译成二进制文件和其它中间格式。

- `cargo`：Rust 的依赖管理和构建工具。Cargo 知道如何下载通常托管在 <https://crates.io> 上的依赖，并且在构建项目时将它们传递给 `rustc`。Cargo 同时内置了测试运行器，用于执行单元测试。

- `rustup`：Rust 工具链安装器和更新器。这个工具用于在 Rust 发布新版本时安装和更新 `rustc` 和 `cargo`。此外，`rustup` 还可以下载标准库的文档。你可以同时安装多个版本的 Rust，并根据需要使用 `rustup` 在它们之间切换。

<details>

要点：

- Rust 有一个快速的发布周期，每六周就会发布一个新版本。新版本保持向后兼容老版本 --- 同时它们会启用新的功能。

- 有三个发布渠道："stable"、"beta" 和 "nightly"。

- 新特性首先在 "nightly" 上进行测试，"beta" 每六周就变成 "stable"。

- 依赖关系也可以从其它 [registries]、git、文件夹等方式解决。

- Rust 还推出了 [editions]：当前版本是 Rust 2021。前几个版本分别是 Rust 2015 和 Rust 2018。
  
  - Editions 允许对语言进行不兼容的更改。
  
  - 为了防止破坏现有代码，editions 是选择加入的：通过 `Cargo.toml` 文件为你的 crate 选择 edition。
  
  - 为了避免生态系统分裂，Rust 编译器可以混合使用为不同 editions 编写的代码。
  
  - 需要指出的是，直接使用编译器而不通过 `cargo` 的情况十分罕见（大多数用户从未这样做过）。
  
  - 值得一提的是，Cargo 本身是一个非常强大和全面的工具。它具有许多高级特性，包括但不限于：
    - 项目/包结构
    - [workspaces]
    - 开发依赖和运行时依赖管理/缓存
    - [build scripting]
    - [global installation]
    - 它还支持使用子命令插件进行扩展（例如 [cargo clippy]）。
  - 从 [官方 Cargo 书籍] 阅读更多信息。

[版本]: https://doc.rust-lang.org/edition-guide/
[工作空间]: https://doc.rust-lang.org/cargo/reference/workspaces.html
[构建脚本]: https://doc.rust-lang.org/cargo/reference/build-scripts.html
[全局安装]: https://doc.rust-lang.org/cargo/commands/cargo-install.html
[cargo clippy]: https://github.com/rust-lang/rust-clippy
[官方 Cargo Book]: https://doc.rust-lang.org/cargo/
[注册表]: https://doc.rust-lang.org/cargo/reference/registries.html

</details>
