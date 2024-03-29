---
translated_at: '2024-03-26T11:24:30.381Z'
---

# 将 Crates 检入 Chromium 源代码

`git status` 应该会显示：

- Crates 代码在 `//third_party/rust/chromium_crates_io`
- 元数据（`BUILD.gn` 和 `README.chromium`）在
  `//third_party/rust/<crate>/<version>`

请在后一个位置添加一个 `OWNERS` 文件。

你应该把所有这些，连同你的 `Cargo.toml` 和 `gnrt_config.toml`
改动一起，提交到 Chromium 仓库中。

**重要**：你需要使用 `git add -f`，否则 `.gitignore` 文件
可能导致某些文件被跳过。

当你这么做的时候，你可能会发现提交前检查失败，因为使用了非包容性语言。
这是因为 Rust crate 数据倾向于包含 git 分支的名称，而许多项目在那里仍然使用非包容性术语。
所以你可能需要运行：

```shell
infra/update_inclusive_language_presubmit_exempt_dirs.sh > infra/inclusive_language_presubmit_exempt_dirs.txt
git add -p infra/inclusive_language_presubmit_exempt_dirs.txt # 添加任何是你的改变
```
