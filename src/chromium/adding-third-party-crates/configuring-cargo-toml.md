---
translated_at: '2024-03-26T11:24:07.223Z'
---

# 配置 `Cargo.toml` 文件以添加 crates

Chromium 有一套单一的、集中管理的直接 crate 依赖。这些依赖通过一个 [`Cargo.toml`][0] 管理：

```toml
[dependencies]
bitflags = "1"
cfg-if = "1"
cxx = "1"
# 还有很多...
```

如同任何其他的 `Cargo.toml`，你可以指定[更多关于依赖的详细信息][1] --- 最常见的，你会希望指定你希望在 crate 中启用的 `features`。

当在 Chromium 中添加一个 crate 时，你通常需要在另一个文件 `gnrt_config.toml` 中提供一些额外的信息，接下来我们将介绍这个文件。

[0]: https://source.chromium.org/chromium/chromium/src/+/main:third_party/rust/chromium_crates_io/Cargo.toml
[1]: https://doc.rust-lang.org/cargo/reference/specifying-dependencies.html
