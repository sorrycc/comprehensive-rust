---
minutes: 5
translated_at: '2024-03-26T10:01:18.579Z'
---

# 单元测试

Rust 和 Cargo 提供了一个简单的单元测试框架：

- 你的代码中支持单元测试。

- 通过 `tests/` 目录支持集成测试。

测试使用 `#[test]` 标记。单元测试通常放在一个嵌套的 `tests` 模块中，使用 `#[cfg(test)]` 来有条件地编译它们，仅在构建测试时编译。

```rust,editable,ignore
fn first_word(text: &str) -> &str {
    match text.find(' ') {
        Some(idx) => &text[..idx],
        None => &text,
    }
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_empty() {
        assert_eq!(first_word(""), "");
    }

    #[test]
    fn test_single_word() {
        assert_eq!(first_word("Hello"), "Hello");
    }

    #[test]
    fn test_multiple_words() {
        assert_eq!(first_word("Hello World"), "Hello");
    }
}
```

- 这允许你对私有辅助函数进行单元测试。
- 当你运行 `cargo test` 时，`#[cfg(test)]` 属性才会激活。

<details>

在 playground 中运行测试，以显示它们的结果。

</details>
