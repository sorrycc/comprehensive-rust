---
translated_at: '2024-03-26T11:12:33.464Z'
---

# Chromium Rust 政策

Chromium 目前还不允许使用第一方 Rust，除非在罕见的情况下得到 Chromium 的[领域技术负责人](https://source.chromium.org/chromium/chromium/src/+/main:ATL_OWNERS)的批准。

Chromium 对第三方库的政策概述在[此处](https://chromium.googlesource.com/chromium/src/+/main/docs/adding_to_third_party.md#rust) - 在各种情况下允许使用 Rust 作为第三方库，包括如果它们是性能或安全性最佳的选择。

很少有 Rust 库直接公开 C/C++ API，这意味着几乎所有这些库都需要少量的第一方胶水代码。

```bob
"C++"                           Rust
.- - - - - - - - - -.           .- - - - - - - - - - - - - - - - - - - - - - -.
:                   :           :                                             :
: 现有的 Chromium   :           :  Chromium Rust              现有的 Rust     :
: "C++"             :           :  "包装器"                    crate           :
: +---------------+ :           : +----------------+          +-------------+ :
: |               | :           : |                |          |             | :
: |         o-----+-+-----------+-+->            o-+----------+-->          | :
: |               | : 语言边界  : |                | Crate    |             | :
: +---------------+ :           : +----------------+ API      +-------------+ :
:                   :           :                                             :
`- - - - - - - - - -'           `- - - - - - - - - - - - - - - - - - - - - - -'
```

> 针对特定第三方 crate 的第一方 Rust 胶水代码通常应该保存在 `third_party/rust/<crate>/<version>/wrapper` 中。

因此，今天的课程将重点放在以下内容：

- 引入第三方 Rust 库（“crates”）
- 编写胶水代码以便能够从 Chromium C++ 使用这些 crate。

如果这项政策随着时间的推移而变化，课程将发展以保持同步。
