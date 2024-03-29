---
translated_at: '2024-03-26T11:46:12.340Z'
---

# async / await 的陷阱

Async / await 为并发异步编程提供了方便且高效的抽象。然而，Rust 中的 async / await 模型也伴随着一些陷阱和隐患。我们在这一章中举例说明了其中的一些：

- [阻塞执行器](pitfalls/blocking-executor.md)
- [Pin](pitfalls/pin.md)
- [异步 Trait](pitfalls/async-traits.md)
- [取消](pitfalls/cancellation.md)
