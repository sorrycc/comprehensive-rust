---
translated_at: '2024-03-26T11:46:02.610Z'
---

# 运行时

_运行时_ 提供了异步执行操作的支持（一个 _反应器_）并负责执行 futures（一个 _执行器_）。Rust 没有 “内置”的运行时，但有几个选项可用：

- [Tokio](https://tokio.rs/)：性能强大，拥有发达的功能生态系统，如用于 HTTP 的 [Hyper](https://hyper.rs/) 或用于 gRPC 的 [Tonic](https://github.com/hyperium/tonic)。
- [async-std](https://async.rs/)：旨在成为 “async 的 std”，并在 `async::task` 中包含了一个基本的运行时。
- [smol](https://docs.rs/smol/latest/smol/)：简单轻量

几个较大的应用程序有他们自己的运行时。例如，[Fuchsia](https://fuchsia.googlesource.com/fuchsia/+/refs/heads/main/src/lib/fuchsia-async/src/lib.rs) 已经有了一个。

<details>

- 注意，在列出的运行时中，只有 Tokio 在 Rust playground 中得到支持。Playground 也不允许任何 I/O，所以大多数有趣的异步事物无法在 playground 中运行。

- Futures 是 “惰性的”，即它们不会做任何事情（甚至不开始 I/O 操作），除非有一个执行器在轮询它们。这与 JS Promises 不同，例如，即使它们永远不被使用，Promises 也会执行完毕。

</details>
