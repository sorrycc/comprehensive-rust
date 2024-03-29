---
translated_at: '2024-03-26T12:04:29.248Z'
---

# 在 Android 中构建

创建一个 `cc_library_static` 来构建 C++ 库，包括生成的 CXX 头文件和源文件。

```javascript
cc_library_static {
    name: "libcxx_test_cpp",
    srcs: ["cxx_test.cpp"],
    generated_headers: [
        "cxx-bridge-header",
        "libcxx_test_bridge_header"
    ],
    generated_sources: ["libcxx_test_bridge_code"],
}
```

<details>

- 指出 `libcxx_test_bridge_header` 和 `libcxx_test_bridge_code` 是 CXX 生成的 C++ 绑定的依赖项。我们将在下一张幻灯片中展示这些是如何设置的。
- 注意，您还需要依赖 `cxx-bridge-header` 库以引入通用的 CXX 定义。
- 使用 CXX 在 Android 中的完整文档可以在 [Android 文档] 中找到。您可能想与班上的学生分享该链接，以便他们将来能再次找到这些指令。

[Android 文档]: https://source.android.com/docs/setup/build/rust/building-rust-modules/android-rust-patterns#rust-cpp-interop-using-cxx

</details>
