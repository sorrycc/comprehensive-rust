---
translated_at: '2024-03-26T11:20:43.839Z'
---

# 包含 `unsafe` Rust 代码

默认情况下，`rust_static_library` 禁止使用 Unsafe Rust 代码 --- 它不会编译。如果你需要使用 Unsafe Rust 代码，请在 gn 目标中添加 `allow_unsafe = true`。（在课程的后面我们会看到需要这样做的情况。）

```gn
import("//build/rust/rust_static_library.gni")

rust_static_library("my_rust_lib") {
  crate_root = "lib.rs"
  sources = [
    "lib.rs",
    "hippopotamus.rs"
  ]
  allow_unsafe = true
}
```
