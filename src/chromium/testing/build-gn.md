---
translated_at: '2024-03-26T11:16:54.232Z'
---

# GN 规则用于 Rust 测试

构建 Rust `gtest` 测试的最简单方法是将它们添加到已经包含用 C++ 编写的测试的现有测试二进制文件中。例如：

```gn
test("ui_base_unittests") {
  ...
  sources += [ "my_rust_lib_unittest.rs" ]
  deps += [ ":my_rust_lib" ]
}
```

在一个单独的 `static_library` 中撰写 Rust 测试也是可行的，但需要手动声明对支持库的依赖：

```gn
rust_static_library("my_rust_lib_unittests") {
  testonly = true
  is_gtest_unittests = true
  crate_root = "my_rust_lib_unittest.rs"
  sources = [ "my_rust_lib_unittest.rs" ]
  deps = [
    ":my_rust_lib",
    "//testing/rust_gtest_interop",
  ]
}

test("ui_base_unittests") {
  ...
  deps += [ ":my_rust_lib_unittests" ]
}
```
