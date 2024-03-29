---
translated_at: '2024-03-26T11:21:33.123Z'
---

# 审核第三方 Crates

添加新库受到 Chromium 的标准[政策][0]限制，当然，也需要进行安全审查。由于您可能不仅仅引入一个 crate，而且还会引入传递依赖，因此可能需要审查大量代码。另一方面，安全的 Rust 代码可能会有限制的负面影响。您应该如何审查它呢？

随着时间的推移，Chromium 旨在移向基于 [cargo vet][1] 的流程。

与此同时，对于每个新添加的 crate，我们正在检查以下内容：

- 了解每个 crate 的用途。crates 之间的关系是什么？如果每个 crate 的构建系统包含 `build.rs` 或过程宏，找出它们的用途。它们是否与 Chromium 的正常构建方式兼容？
- 检查每个 crate 似乎是否维护得相当好
- 使用 `cd third-party/rust/chromium_crates_io; cargo audit` 来检查已知的漏洞（首先您需要执行 `cargo install cargo-audit`，这讽刺地涉及从互联网下载大量依赖项[2]）
- 确保任何 `unsafe` 代码足够符合[两条规则][3]
- 检查是否使用了 `fs` 或 `net` API
- 足够仔细地阅读所有代码，寻找可能被恶意插入的任何异常。 （在这里，您不能真实地期望达到 100% 的完美：代码量通常太多了。）

这些只是指导原则 --- 与 `security@chromium.org` 的审查者合作，找出对 crate 感到自信的正确方法。

[0]: https://chromium.googlesource.com/chromium/src/+/refs/heads/main/docs/rust.md#第三方审查
[1]: https://mozilla.github.io/cargo-vet/
[2]: ../cargo.md
[3]: https://chromium.googlesource.com/chromium/src/+/main/docs/security/rule-of-2.md#在安全语言中的 unsafe 代码
