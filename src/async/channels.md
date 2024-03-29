---
translated_at: '2024-03-26T11:47:36.778Z'
---

# 异步通道

若干个 crate 支持异步通道。例如 `tokio`：

```rust,editable,compile_fail
use tokio::sync::mpsc::{self, Receiver};

async fn ping_handler(mut input: Receiver<()>) {
    let mut count: usize = 0;

    while let Some(_) = input.recv().await {
        count += 1;
        println!("Received {count} pings so far.");
    }

    println!("ping_handler complete");
}

#[tokio::main]
async fn main() {
    let (sender, receiver) = mpsc::channel(32);
    let ping_handler_task = tokio::spawn(ping_handler(receiver));
    for i in 0..10 {
        sender.send(()).await.expect("Failed to send ping.");
        println!("Sent {} pings so far.", i + 1);
    }

    drop(sender);
    ping_handler_task.await.expect("Something went wrong in ping handler task.");
}
```

<details>

- 将通道大小改为 `3`，看看它如何影响执行过程。

- 总体而言，接口与 [早课](concurrency/channels.md) 中看到的 `sync` 通道类似。

- 尝试移除 `std::mem::drop` 调用。会发生什么？为什么？

- [Flume](https://docs.rs/flume/latest/flume/) crate 有实现了 `sync` 和 `async` 的 `send` 和 `recv` 的通道。这对于同时涉及 IO 和繁重 CPU 处理任务的复杂应用程序来说非常方便。

- 使用 `async` 通道的优势在于能够将它们与其它 `future` 结合起来，创造出复杂的控制流程。

</details>
