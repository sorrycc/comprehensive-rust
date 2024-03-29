---
translated_at: '2024-03-26T11:23:02.539Z'
---

# 下载 Crates

一个称为 `gnrt` 的工具知道如何下载 crates 并且如何生成 `BUILD.gn` 规则。

首先，像这样下载你想要的 crate：

```shell
cd chromium/src
vpython3 tools/crates/run_gnrt.py -- vendor
```

> 虽然 `gnrt` 工具是 Chromium 源代码的一部分，通过运行这个命令，你将从 `crates.io` 下载并运行它的依赖。
> 见[前面的章节][0]讨论这个安全决策。

这个 `vendor` 命令可能会下载：

- 你的 crate
- 直接和传递依赖
- 新版本的其他 crates，如 `cargo` 所需，以解析 Chromium 所需的完整 crates 集。

Chromium 维护一些 crates 的补丁，存放在 `//third_party/rust/chromium_crates_io/patches`。这些补丁将会自动重新应用，但如果补丁应用失败，你可能需要采取手动操作。

[0]: ../cargo.md
