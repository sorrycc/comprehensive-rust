---
translated_at: '2024-03-26T11:15:52.131Z'
---

# `rust_gtest_interop` 库

[`rust_gtest_interop`][0] 库提供了以下方式：

- 将 Rust 函数作为 `gtest` 测试用例使用（使用 `#[gtest(...)]` 属性）
- 使用 `expect_eq!` 和类似宏（类似于 `assert_eq!`，但在断言失败时不会引发恐慌，也不会终止测试）。

示例：

```rust,ignore
use rust_gtest_interop::prelude::*;

#[gtest(MyRustTestSuite, MyAdditionTest)]
fn test_addition() {
    expect_eq!(2 + 2, 4);
}
```

[0]: https://chromium.googlesource.com/chromium/src/+/main/testing/rust_gtest_interop/README.md
