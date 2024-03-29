---
minutes: 30
translated_at: '2024-03-26T10:23:36.079Z'
---

# 练习：表达式求值

我们来编写一个简单的递归算术表达式求值器。

这里的 `Box` 类型是一个智能指针，将在课程后面详细介绍。可以使用 `Box::new` 来“装箱”一个表达式，如测试中所见。要求值一个装箱的表达式，使用解引用运算符（`*`）来“拆箱”它：`eval(*boxed_expr)`。

有些表达式无法求值并会返回错误。标准的 [`Result<Value, String>`](https://doc.rust-lang.org/std/result/enum.Result.html) 类型是一个枚举，表示要么是成功的值（`Ok(Value)`），要么是错误（`Err(String)`）。我们将在后面详细介绍这种类型。

将代码复制并粘贴到 Rust playground 中，开始实现 `eval`。最终产品应该通过测试。使用 `todo!()` 并逐一通过测试可能会有所帮助。你也可以用 `#[ignore]` 暂时跳过一个测试：

```none
#[test]
#[ignore]
fn test_value() { .. }
```

如果你提前完成，尝试编写一个导致除以零或整数溢出的测试。你如何利用 `Result` 而不是 panic 来处理这个问题？

```rust
{{#include exercise.rs:Operation}}

{{#include exercise.rs:Expression}}

{{#include exercise.rs:eval}}
    todo!()
}

{{#include exercise.rs:tests}}
```
