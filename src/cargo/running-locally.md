---
translated_at: '2024-03-26T11:26:57.921Z'
---

# 本地使用 Cargo 运行代码

如果你想在自己的系统上尝试代码，那么首先需要安装 Rust。请按照 [Rust 书籍中的指南][1] 完成安装。这应该会给你一个可工作的 `rustc` 和 `cargo`。在撰写本文时，最新的稳定 Rust 版本号如下：

```shell
% rustc --version
rustc 1.69.0 (84c898d65 2023-04-16)
% cargo --version
cargo 1.69.0 (6e9a83356 2023-04-12)
```

你也可以使用任何更新版本，因为 Rust 保持向后兼容。

有了这些，按照以下步骤从本教程中的示例构建一个 Rust 二进制文件：

1. 点击你想复制的示例上的 "复制到剪贴板" 按钮。

2. 使用 `cargo new exercise` 创建一个新的 `exercise/` 目录用于你的代码：

   ```shell
   $ cargo new exercise
        Created binary (application) `exercise` package
   ```

3. 导航到 `exercise/` 并使用 `cargo run` 来构建并运行你的二进制文件：

   ```shell
   $ cd exercise
   $ cargo run
      Compiling exercise v0.1.0 (/home/mgeisler/tmp/exercise)
       Finished dev [unoptimized + debuginfo] target(s) in 0.75s
        Running `target/debug/exercise`
   Hello, world!
   ```

4. 用你自己的代码替换 `src/main.rs` 中的样板代码。例如，使用上一页的示例，让 `src/main.rs` 看起来像

   ```rust
   fn main() {
       println!("Edit me!");
   }
   ```

5. 使用 `cargo run` 来构建并运行你更新后的二进制文件：

   ```shell
   $ cargo run
      Compiling exercise v0.1.0 (/home/mgeisler/tmp/exercise)
       Finished dev [unoptimized + debuginfo] target(s) in 0.24s
        Running `target/debug/exercise`
   Edit me!
   ```

6. 使用 `cargo check` 快速检查你的项目是否有错误，使用 `cargo build` 编译但不运行它。你会在 `target/debug/` 找到正常调试构建的输出。使用 `cargo build --release` 在 `target/release/` 生成一个优化的发布构建。

7. 通过编辑 `Cargo.toml`，你可以为你的项目添加依赖项。当你

执行 `cargo` 命令，它将会自动下载并编译所缺少的依赖项。

[1]: https://doc.rust-lang.org/book/ch01-01-installation.html

<details>

尽量鼓励课程参与者安装 Cargo 并使用本地编辑器。
这将让他们的生活变得更轻松，因为他们将拥有一个正常的开发环境。

</details>
