---
minutes: 30
translated_at: '2024-03-26T10:09:28.021Z'
---

# 练习：ROT13

在这个例子中，你将实现经典的 ["ROT13" 密码](https://en.wikipedia.org/wiki/ROT13)。将这段代码复制到 playground 中，并实现缺失的部分。只旋转 ASCII 字母字符，以确保结果仍然是有效的 UTF-8。

```rust,compile_fail
{{#include exercise.rs:head }}

// 为 `RotDecoder` 实现 `Read` trait。

{{#include exercise.rs:main }}
```

如果你将两个 `RotDecoder` 实例链接在一起，每个都旋转 13 个字符，会发生什么？
