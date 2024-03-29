---
minutes: 5
translated_at: '2024-03-26T10:28:01.947Z'
---

# 文件系统层次结构

省略模块内容会告诉 Rust 在其他文件中查找它：

```rust,editable,compile_fail
mod garden;
```

这告诉 rust `garden` 模块的内容位于 `src/garden.rs`。类似地，`garden::vegetables` 模块可以在 `src/garden/vegetables.rs` 找到。

`crate` 的根目录在：

- `src/lib.rs`（对于库 crate）
- `src/main.rs`（对于二进制 crate）

在文件中定义的模块也可以使用“内部文档注释”进行文档化。这些文档化了包含它们的项目 -- 在本例中，是一个模块。

```rust,editable,compile_fail
//! 此模块实现了花园，包括一个高性能的发芽实现。

// 从此模块重新导出类型。
pub use garden::Garden;
pub use seeds::SeedPacket;

/// 播种给定的种子包。
pub fn sow(seeds: Vec<SeedPacket>) {
    todo!()
}

/// 收获花园中准备好的产物。
pub fn harvest(garden: &mut Garden) {
    todo!()
}
```

<details>

- 在 Rust 2018 之前，模块需要位于 `module/mod.rs` 而不是 `module.rs`，而这在 2018 之后的版本中仍然是一个可行的选择。

- 引入 `filename.rs` 作为 `filename/mod.rs` 的替代方案的主要原因是，许多名为 `mod.rs` 的文件在 IDE 中难以区分。

- 更深层的嵌套可以使用文件夹，即使主模块是一个文件：

  ```ignore
  src/
  ├── main.rs
  ├── top_module.rs
  └── top_module/
      └── sub_module.rs
  ```

- Rust 查找模块的位置可以通过编译器指令更改：

  ```rust,ignore
  #[path = "some/path.rs"]
  mod some_module;
  ```

  例如，如果您希望将模块的测试放在名为 `some_module_test.rs` 的文件中，这非常有用，类似于 Go 中的约定。

</details>
