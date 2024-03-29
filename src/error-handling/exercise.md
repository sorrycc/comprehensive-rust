---
minutes: 30
translated_at: '2024-03-26T11:00:30.347Z'
---

# 练习：使用 Result 重写

下面实现了一个非常简单的表达式语言解析器。
然而，它通过触发 panic 来处理错误。改写它，使其使用惯用的错误处理，
并将错误传播到 `main` 从函数返回。可随意使用 `thiserror` 和 `anyhow`。

提示：从修复 `parse` 函数的错误处理开始。一旦那部分工作正确，更新 `Tokenizer` 以实现
`Iterator<Item=Result<Token, TokenizerError>>`，并在解析器中处理它。

```rust,editable
{{#include exercise.rs:types}}

{{#include exercise.rs:panics}}
```
