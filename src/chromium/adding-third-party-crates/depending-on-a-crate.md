---
translated_at: '2024-03-26T11:23:16.414Z'
---

# 依赖一个 Crate

一旦您添加了第三方 crate 并生成了构建规则，依赖一个 crate 就变得很简单。找到您的 `rust_static_library` 目标，并在您的 crate 中添加一个对 `:lib` 目标的 `dep`。

具体来说，

```bob
                     +------------+      +----------------------+
"//third_party/rust" | crate 名称 | "/v" | 主 semver 版本号 | ":lib"
                     +------------+      +----------------------+
```

例如，

```gn
rust_static_library("my_rust_lib") {
  crate_root = "lib.rs"
  sources = [ "lib.rs" ]
  deps = [ "//third_party/rust/example_rust_crate/v1:lib" ]
}
```
