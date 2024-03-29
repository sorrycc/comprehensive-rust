---
translated_at: '2024-03-26T11:36:55.753Z'
---

# 外设访问包

[`svd2rust`](https://crates.io/crates/svd2rust) 从 [CMSIS-SVD](https://www.keil.com/pack/doc/CMSIS/SVD/html/index.html) 文件生成大部分安全的 Rust 封装器，用于内存映射外设。

```rust,editable,compile_fail
{{#include examples/src/bin/pac.rs:Example}}
```

<details>

- SVD（系统视图描述）文件是由硅供应商提供的 XML 文件，通常描述了设备的内存映射。
  - 它们按外设、寄存器、字段和值组织，包括名称、描述、地址等信息。
  - SVD 文件通常存在错误和不完整，因此有多个项目致力于修正这些错误，补充缺失的细节，并发布生成的包。
- `cortex-m-rt` 提供向量表等内容。
- 如果你执行 `cargo install cargo-binutils`，然后运行 `cargo objdump --bin pac -- -d --no-show-raw-insn`，可以看到结果的二进制文件。

使用以下命令运行示例：

```sh
cargo embed --bin pac
```

</details>
