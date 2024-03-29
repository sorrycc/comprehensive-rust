---
minutes: 5
translated_at: '2024-03-26T10:01:45.265Z'
---

# 其他类型的测试

## 集成测试

如果你想作为客户端测试你的库，请使用集成测试。

在 `tests/` 下创建一个 `.rs` 文件：

```rust,ignore
// tests/my_library.rs
use my_library::init;

#[test]
fn test_init() {
    assert!(init().is_ok());
}
```

这些测试只能访问你的 crate 的公共 API。

## 文档测试

Rust 内置了对文档测试的支持：

````rust
/// 将字符串缩短到给定长度。
///
/// ```
/// # use playground::shorten_string;
/// assert_eq!(shorten_string("Hello World", 5), "Hello");
/// assert_eq!(shorten_string("Hello World", 20), "Hello World");
/// ```
pub fn shorten_string(s: &str, length: usize) -> &str {
    &s[..std::cmp::min(length, s.len())]
}
````

- 在 `///` 注释中的代码块会自动被视为 Rust 代码。
- 该代码将作为 `cargo test` 的一部分被编译和执行。
- 在代码中添加 `#` 会从文档中隐藏它，但仍然会编译/运行它。
- 在 [Rust Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&gist=3ce2ad13ea1302f6572cb15cd96becf0) 上测试上述代码。
