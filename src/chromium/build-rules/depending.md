---
translated_at: '2024-03-26T11:20:55.609Z'
---

# 依赖 Chromium C++ 的 Rust 代码

只需将上述目标添加到某个 Chromium C++ 目标的 `deps` 中。

```gn
import("//build/rust/rust_static_library.gni")

rust_static_library("my_rust_lib") {
  crate_root = "lib.rs"
  sources = [ "lib.rs" ]
}

# 或 source_set、static_library 等。
component("preexisting_cpp") {
  deps = [ ":my_rust_lib" ]
}
```

<details>
我们将看到，这种关系只有在 Rust 代码暴露纯 C API，这些 API 能够被 C++ 调用，或者我们使用 C++/Rust 互操作工具时才有效。
</details>
