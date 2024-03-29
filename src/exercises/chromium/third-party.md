---
translated_at: '2024-03-26T10:51:54.391Z'
---

# 练习

在 Chromium 中添加 [uwuify][0]，并关闭该 crate 的[默认特性][1]。
假设该 crate 将用于发布版的 Chromium，但不会用于处理不可信的输入。

（在下一个练习中，我们将在 Chromium 中使用 uwuify，但如果你愿意，也可以直接跳到那个练习。或者，你可以创建一个使用 `uwuify` 的新 [`rust_executable` 目标][2]）。

<details>

学生需要下载大量的传递依赖。

总共需要的 crates 包括：

- `instant`，
- `lock_api`，
- `parking_lot`，
- `parking_lot_core`，
- `redox_syscall`，
- `scopeguard`，
- `smallvec`，以及
- `uwuify`。

如果学生下载的内容比这还要多，那么他们可能忘记关闭默认特性了。

感谢 [Daniel Liu][3] 提供这个 crate！

</details>

[0]: https://crates.io/crates/uwuify
[1]: https://doc.rust-lang.org/cargo/reference/features.html#the-default-feature
[2]: https://source.chromium.org/chromium/chromium/src/+/main:build/rust/rust_executable.gni
[3]: https://github.com/Daniel-Liu-c0deb0t
