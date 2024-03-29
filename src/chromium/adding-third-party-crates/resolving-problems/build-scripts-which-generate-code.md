---
translated_at: '2024-03-26T11:25:03.383Z'
---

# 构建生成代码的脚本

如果 `ninja` 抱怨缺少文件，请检查 `build.rs` 来看它是否写了源代码文件。

如果是这样，请修改 [`gnrt_config.toml`][1] 来给 crate 添加 `build-script-outputs`。如果这是一个传递依赖，也就是 Chromium 代码不应该直接依赖的依赖项，还要添加 `allow-first-party-usage=false`。在该文件中已有若干示例：

```toml
[crate.unicode-linebreak]
allow-first-party-usage = false
build-script-outputs = ["tables.rs"]
```

现在重新运行 [`gnrt.py -- gen`][2] 来重新生成 `BUILD.gn` 文件，以通知 ninja 这个特定的输出文件是后续构建步骤的输入。

[1]: ../configuring-gnrt-config-toml.md
[2]: ../generating-gn-build-rules.md
