---
translated_at: '2024-03-26T11:14:19.591Z'
---

# 比较 Chromium 和 Cargo 生态系统

Rust 社区通常使用 `cargo` 和 [crates.io][2] 上的库。
Chromium 是使用 `gn` 和 `ninja` 以及一套精选的依赖构建的。

在 Rust 中编写代码时，你的选择有：

- 使用 `gn` 和 `ninja`，借助 `//build/rust/*.gni` 中的模板
  （例如，稍后我们将遇到的 `rust_static_library`）。这使用了 Chromium 审核过的工具链和 crates。
- 使用 `cargo`，但
  [限制自己使用 Chromium 审核过的工具链和 crates][0]
- 使用 `cargo`，信任[工具链][1]和/或
  [从互联网下载的 crates][2]

从这里开始，我们将聚焦于 `gn` 和 `ninja`，因为这是将 Rust 代码构建为 Chromium 浏览器的方式。同时，Cargo 是 Rust 生态系统中的重要部分，你应该将其保留在工具箱中。

## 小练习

分成小组并：

- 头脑风暴 `cargo` 可能提供优势的场景，并评估这些场景的风险配置文件。
- 讨论使用 `gn` 和 `ninja`、离线 `cargo` 等时，需要信任哪些工具、库和人群。

<details>

在完成练习之前，要求学生避免偷看演讲者的笔记。假设参加课程的人在一起，要求他们分成 3-4 人的小组进行讨论。

与练习第一部分相关的笔记/提示（“Cargo 可能提供优势的场景”）：

- 当编写工具或原型化 Chromium 的一部分时，能够访问 crates.io 库丰富的生态系统是非常棒的。几乎对于任何事情都有一个 crate，并且它们通常都很好用。（`clap` 用于命令行解析，`serde` 用于序列化/反序列化到/从各种格式，`itertools` 用于处理迭代器等）。

  - `cargo` 使尝试库变得简单（只需在 `Cargo.toml` 中添加一行，然后开始编写代码）
  - 比较 CPAN 如何帮助使 `perl` 成为一个受欢迎的选择可能是值得的。或者与 `python` + `pip` 进行比较。

- 开发经验不仅仅通过 Rust 核心工具变得非常友好（例如，使用 `rustup` 在测试需要在夜间版、当前稳定版和旧稳定版上运行的 crate 时切换到不同的 `rustc` 版本），还通过第三方工具生态系统得到提升（例如，Mozilla 提供的 `cargo vet` 用于简化和共享安全审计; `criterion` 箱提供了一种流畅的方式来运行基准测试）。

  - `cargo` 通过 `cargo install --locked cargo-vet` 方便地添加工具。
  - 与 Chrome 扩展或 VScode 扩展比较可能是值得的。

- 在哪些项目中使用 `cargo` 可能是正确选择的广泛、通用示例：

  - 或许令人惊讶的是，Rust 在行业中用于编写命令行工具的流行度越来越高。库的广度和人体工程学可与 Python 媲美，同时更加健壮（得益于丰富的类型系统）并且运行速度更快（作为一种编译语言，而非解释型语言）。
  - 参与 Rust 生态系统需要使用标准 Rust 工具，如 Cargo。想要获得外部贡献，并希望在 Chromium 之外被使用（例如，在 Bazel 或 Android/Soong 构建环境中）的库，应该考虑使用 Cargo。

- 与 Chromium 相关的基于 `cargo` 的项目示例：
  - `serde_json_lenient`（在 Google 的其他部分进行了试验，并导致了性能改进的 PR）
  - 像 `font-types` 这样的 Fontations 库
  - `gnrt` 工具（我们将在课程后面遇到它），它依赖于 `clap` 进行命令行解析和 `toml` 进行配置文件。
    - 免责声明：使用 `cargo` 的独特原因是在构建 Rust 标准库和构建 Rust 工具链时 `gn` 不可用。
    - `run_gnrt.py` 使用 Chromium 的 `cargo` 和 `rustc` 副本。`gnrt` 依赖于从互联网下载的第三方库，但 `run_gnrt.py` 要求 `cargo` 仅通过 `Cargo.lock` 允许 `--locked` 内容。

学生可能会认识到以下项目被隐式或显式地信任：

- `rustc`（Rust 编译器），它依赖于 LLVM 库、Clang 编译器、`rustc` 源代码（从 GitHub 获取，由 Rust 编译器团队审核），用于引导的二进制 Rust 编译器下载
- `rustup`（值得指出的是，`rustup` 是在 https://github.com/rust-lang/ 组织的支持下开发的 - 与 `rustc` 同属一家）
- `cargo`、`rustfmt` 等。
- 各种内部基础设施（构建 `rustc` 的机器人，向 Chromium 工程师分发预构建工具链的系统等）
- Cargo 工具，如 `cargo audit`、`cargo vet` 等。
- 被引入 `//third_party/rust` 的 Rust 库（由 security@chromium.org 审核）
- 其他 Rust 库（一些小众的，一些非常流行且常用的）

</details>

[0]: https://chromium.googlesource.com/chromium/src/+/refs/heads/main/docs/rust.md#Using-cargo
[1]: https://rustup.rs/
[2]: https://crates.io/
