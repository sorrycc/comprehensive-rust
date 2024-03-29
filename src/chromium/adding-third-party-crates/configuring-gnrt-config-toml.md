---
translated_at: '2024-03-26T11:23:48.931Z'
---

# 配置 `gnrt_config.toml`

在 `Cargo.toml` 旁边是 [`gnrt_config.toml`][0]。这包含了 Chromium 特定的拓展来处理 crate。

如果你添加了新的 crate，你至少应该指定 `group`。这包括：

```toml
#   'safe': 该库符合 2 条规则，可以在任何进程中使用。
#   'sandbox': 该库不符合 2 条规则，必须在 sandboxed 进程中使用，例如渲染器或实用程序进程。
#   'test': 该库仅在测试中使用。
```

例如，

```toml
[crate.my-new-crate]
group = 'test' # 仅在测试代码中使用
```

根据 crate 源码布局，你可能还需要使用这个文件来指定在哪里可以找到其 `LICENSE` 文件。

稍后，我们将看到一些其他你需要在这个文件中配置的事项，以解决问题。

[0]: https://source.chromium.org/chromium/chromium/src/+/main:third_party/rust/chromium_crates_io/gnrt_config.toml
