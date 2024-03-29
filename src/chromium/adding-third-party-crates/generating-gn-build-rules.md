---
translated_at: '2024-03-26T11:22:44.044Z'
---

# 生成 `gn` 构建规则

下载完 crate 之后，像这样生成 `BUILD.gn` 文件：

```shell
vpython3 tools/crates/run_gnrt.py -- gen
```

现在运行 `git status`。你应该会发现：

- 在 `third_party/rust/chromium_crates_io/vendor` 中至少有一个新的 crate 源代码
- 在 `third_party/rust/<crate name>/v<major semver version>` 中至少有一个新的 `BUILD.gn`
- 一个合适的 `README.chromium`

“major semver version” 是一个 [Rust “semver” 版本号][0]。

仔细查看，尤其是在 `third_party/rust` 中生成的东西。

<details>

简单谈一谈 semver——特别是在 Chromium 中，它是为了允许一个 crate 的多个不兼容版本，这在 Cargo 生态系统中是不鼓励但有时又是必要的。

</detail>

[0]: https://doc.rust-lang.org/cargo/reference/semver.html
