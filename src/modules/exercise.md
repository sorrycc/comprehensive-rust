---
minutes: 15
translated_at: '2024-03-26T10:28:29.067Z'
---

# 练习：GUI 库的模块化

在本次练习中，你需要重新组织一个小型 GUI 库的实现。这个库定义了一个 `Widget` 特性以及一些该特性的实现，还包含了一个 `main` 函数。

通常，我们会将每种类型或一组密切相关的类型放入它们自己的模块中，因此每种部件类型都应该有自己的模块。

## Cargo 设置

由于 Rust playground 仅支持一个文件，因此你需要在本地文件系统中创建一个 Cargo 项目：

```shell
cargo init gui-modules
cd gui-modules
cargo run
```

编辑生成的 `src/main.rs` 文件以添加 `mod` 声明，并在 `src` 目录中添加额外的文件。

## 源码

以下是 GUI 库的单模块实现：

```rust
{{#include exercise.rs:single-module}}
```

<details>

鼓励学生以对他们自然的方式划分代码，并习惯 `mod`、`use` 和 `pub` 声明。之后，讨论哪种组织方式最为惯用。

</details>
