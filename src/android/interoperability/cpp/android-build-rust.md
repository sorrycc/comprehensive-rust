---
translated_at: '2024-03-26T12:04:06.881Z'
---

# 在 Android 中构建

创建一个依赖 `libcxx` 和你的 `cc_library_static` 的 `rust_binary`。

```javascript
rust_binary {
    name: "cxx_test",
    srcs: ["lib.rs"],
    rustlibs: ["libcxx"],
    static_libs: ["libcxx_test_cpp"],
}
```
