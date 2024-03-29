---
translated_at: '2024-03-26T12:04:00.585Z'
---

# 在 Android 中构建

创建两个 genrules：一个用于生成 CXX 头文件，另一个用于生成 CXX 源文件。然后将它们用作 `cc_library_static` 的输入。

```javascript
// 生成包含对 lib.rs 中导出的 Rust 函数的 C++ 绑定的 C++ 头文件
genrule {
    name: "libcxx_test_bridge_header",
    tools: ["cxxbridge"],
    cmd: "$(location cxxbridge) $(in) --header > $(out)",
    srcs: ["lib.rs"],
    out: ["lib.rs.h"],
}

// 生成 Rust 调用的 C++ 代码。
genrule {
    name: "libcxx_test_bridge_code",
    tools: ["cxxbridge"],
    cmd: "$(location cxxbridge) $(in) > $(out)",
    srcs: ["lib.rs"],
    out: ["lib.rs.cc"],
}
```

<details>

- `cxxbridge` 工具是一个独立的工具，用于生成桥接模块的 C++ 侧。它被包含在 Android 中，并可作为 Soong 工具使用。
- 按照惯例，如果你的 Rust 源文件是 `lib.rs`，你的头文件将被命名为 `lib.rs.h`，你的源文件将被命名为 `lib.rs.cc`。虽然这个命名约定不是强制性的。

</details>
