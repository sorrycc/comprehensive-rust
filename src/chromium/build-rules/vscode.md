---
translated_at: '2024-03-26T11:20:33.835Z'
---

# Visual Studio Code

Rust 代码中的类型被省略，这使得好的 IDE 对于 Rust 来说比对于 C++ 更加有用。Visual Studio Code 对于 Chromium 中的 Rust 支持非常好。要使用它，请：

- 确保你的 VSCode 安装了 `rust-analyzer` 扩展，而不是早期的 Rust 支持形式
- `gn gen out/Debug --export-rust-project`（或者对你的输出目录等效操作）
- `ln -s out/Debug/rust-project.json rust-project.json`

<img src="vscode.png" style="border: 1px solid black;" alt="VSCode 示例截图">

<details>

如果观众对 IDE 天生持怀疑态度，展示 rust-analyzer 的一些代码注释和探索功能的演示可能会很有帮助。

以下步骤可能有助于演示（但也可以选择你最熟悉的与 Chromium 相关的 Rust 代码）：

- 打开 `components/qr_code_generator/qr_code_generator_ffi_glue.rs`
- 将光标放在 `qr_code_generator_ffi_glue.rs` 中的 `QrCode::new` 调用上（大约第 26 行）
- 演示 **显示文档**（典型的绑定：vscode = ctrl k i；vim/CoC = K）。
- 演示 **转到定义**（典型的绑定：vscode = F12；vim/CoC = g d）。（这将带你到 `//third_party/rust/.../qr_code-.../src/lib.rs`。）
- 演示 **大纲** 并导航到 `QrCode::with_bits` 方法（大约第 164 行；大纲在 vscode 的文件资源管理器面板中；典型的 vim/CoC 绑定 = space o）
- 演示 **类型注解**（在 `QrCode::with_bits` 方法中有很多不错的例子）

可能值得指出的是，`gn gen ... --export-rust-project` 需要在编辑 `BUILD.gn` 文件后重新运行（在本次会议的练习中我们会多次这样做）。

</details>
