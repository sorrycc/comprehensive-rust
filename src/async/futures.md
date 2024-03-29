---
translated_at: '2024-03-26T11:46:55.213Z'
---

# 未来

[`Future`](https://doc.rust-lang.org/std/future/trait.Future.html) 是一个特性，由表示尚未完成的操作的对象实现。一个 future 可以被轮询，而 `poll` 返回一个 [`Poll`](https://doc.rust-lang.org/std/task/enum.Poll.html)。

```rust
use std::pin::Pin;
use std::task::Context;

pub trait Future {
    type Output;
    fn poll(self: Pin<&mut Self>, cx: &mut Context<'_>) -> Poll<Self::Output>;
}

pub enum Poll<T> {
    Ready(T),
    Pending,
}
```

一个异步函数返回一个 `impl Future`。也可能（但不常见）为你自己的类型实现 `Future`。例如，`tokio::spawn` 返回的 `JoinHandle` 实现了 `Future` 来允许加入它。

`.await` 关键字，应用于一个 Future，使得当前异步函数暂停，直到该 Future 准备就绪，然后求值为其输出。

<details>

- `Future` 和 `Poll` 类型正如所示的那样实现；点击链接在文档中显示实现。

- 我们将不讨论 `Pin` 和 `Context`，因为我们将专注于编写异步代码，而不是构建新的异步原语。简要地说：

  - `Context` 允许一个 Future 将自己安排在发生某个事件时再次被轮询。

  - `Pin` 确保 Future 不会在内存中移动，以便指向该 future 的指针保持有效。这是必需的，以允许在 `.await` 之后引用保持有效。

</details>
