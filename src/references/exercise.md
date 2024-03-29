---
minutes: 15
translated_at: '2024-03-26T10:20:45.590Z'
---

# 练习：几何学

我们将创建几个三维几何的实用函数，用 `[f64;3]` 表示一个点。由你来确定函数的签名。

```rust,compile_fail
// 通过对坐标的平方求和来计算一个向量的大小，并取平方根。使用 `sqrt()` 方法来计算平方根，像这样 `v.sqrt()`。

{{#include exercise.rs:magnitude}}
fn magnitude(...) -> f64 {
    todo!()
}

// 通过计算向量的大小并将其所有坐标除以该大小来规范化一个向量。

{{#include exercise.rs:normalize}}
fn normalize(...) {
    todo!()
}

// 使用以下的 `main` 来测试你的工作。

{{#include exercise.rs:main}}
```
