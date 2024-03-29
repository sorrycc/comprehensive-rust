---
translated_at: '2024-03-26T11:24:45.682Z'
---

# 构建脚本，用于构建 C++ 或执行任意操作

一些 crate 使用 [`cc`][1] crate 来构建和链接 C/C++ 库。其他 crate 在其构建脚本中使用 [`bindgen`][2] 来解析 C/C++ 。这些操作在 Chromium 环境中无法被支持 --- 我们的 gn、ninja 和 LLVM 构建系统在表达构建动作之间的关系时非常具体。

因此，你的选项有：

- 避免使用这些 crate
- 对 crate 应用补丁。

补丁应该保存在
`third_party/rust/chromium_crates_io/patches/<crate>` 中 - 参见 [`cxx` crate 针对的补丁][3] 的例子 - 并且会在每次通过 `gnrt` 升级 crate 时自动应用。

[1]: https://crates.io/crates/cc
[2]: https://crates.io/crates/bindgen
[3]: https://source.chromium.org/chromium/chromium/src/+/main:third_party/rust/chromium_crates_io/patches/cxx/
