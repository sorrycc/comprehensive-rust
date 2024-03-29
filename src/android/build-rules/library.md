---
translated_at: '2024-03-26T12:04:54.409Z'
---

# Rust 库

你可以使用 `rust_library` 为 Android 创建一个新的 Rust 库。

这里我们声明了对两个库的依赖：

- `libgreeting`，我们在下面定义，
- `libtextwrap`，这是一个已经在 [`external/rust/crates/`][crates] 中存放的包。

[crates]: https://cs.android.com/android/platform/superproject/+/master:external/rust/crates/

_hello_rust/Android.bp_：

```javascript
{{#include library/Android.bp}}
```

_hello_rust/src/main.rs_：

```rust,ignore
{{#include library/src/main.rs:main}}
```

_hello_rust/src/lib.rs_：

```rust,ignore
{{#include library/src/lib.rs:greeting}}
```

你可以像之前一样构建、推送并运行二进制文件：

```shell
{{#include ../build_all.sh:hello_rust_with_dep}}
```

```text
Hello Bob, it is very
nice to meet you!
```
