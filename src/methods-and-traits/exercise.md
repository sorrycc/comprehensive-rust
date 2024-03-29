---
minutes: 20
translated_at: '2024-03-26T10:30:09.092Z'
---

# 练习：`Logger` 特性

让我们利用一个 `Logger` 特性和它的 `log` 方法来设计一个简单的日志工具。可能需要记录其进程的代码之后可以使用 `&impl Logger`。在测试中，这可能会将信息放到测试日志文件中，而在生产环境构建时它会将信息发送到日志服务器。

然而，下面给出的 `StderrLogger` 会记录所有信息，不管它们的详细程度如何。你的任务是编写一个 `VerbosityFilter` 类型，它会忽略超过最大详细程度的信息。

这是一个常见模式：一个结构体包装一个特性实现，并实现同样的特性，在此过程中增加行为。在日志工具中，还可能会有哪些其他类型的封装器是有用的？

```rust,compile_fail
{{#include exercise.rs:setup}}

// TODO: 定义并实现 `VerbosityFilter`。

{{#include exercise.rs:main}}
```
