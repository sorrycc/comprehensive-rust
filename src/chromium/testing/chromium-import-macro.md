---
translated_at: '2024-03-26T11:16:33.251Z'
---

# `chromium::import!` 宏

在将 `:my_rust_lib` 添加到 GN `deps` 后，我们还需要学习如何从 `my_rust_lib_unittest.rs` 中导入并使用 `my_rust_lib`。我们没有为 `my_rust_lib` 提供一个显式的 `crate_name`，所以它的包名是基于完整的目标路径和名称计算得出的。幸运的是，我们可以使用自动导入的 `chromium` 包中的 `chromium::import!` 宏来避免处理这样一个笨重的名字：

```rust,ignore
chromium::import! {
    "//ui/base:my_rust_lib";
}

use my_rust_lib::my_function_under_test;
```

在底层，该宏展开为类似于：

```rust,ignore
extern crate ui_sbase_cmy_urust_ulib as my_rust_lib;

use my_rust_lib::my_function_under_test;
```

更多信息可以在 `chromium::import` 宏的 [文档注释][0] 中找到。

<details>

`rust_static_library` 支持通过 `crate_name` 属性指定一个显式的名字，但这样做是不鼓励的。这是因为包名必须是全局唯一的。crates.io 保证了其包名的唯一性，所以由 `gnrt` 工具生成的 `cargo_crate` GN 目标（在后面的部分中介绍）使用简短的包名。

</details>

[0]: https://source.chromium.org/chromium/chromium/src/+/main:build/rust/chromium_prelude/chromium_prelude.rs?q=f:chromium_prelude.rs%20pub.use.*%5Cbimport%5Cb;%20-f:third_party&ss=chromium%2Fchromium%2Fsrc
