---
translated_at: '2024-03-26T11:06:22.107Z'
---

# 通道

Rust 通道有两部分：一个 `Sender<T>` 和一个 `Receiver<T>`。这两部分通过通道连接，但是你只能看到端点。

```rust,editable
use std::sync::mpsc;

fn main() {
    let (tx, rx) = mpsc::channel();

    tx.send(10).unwrap();
    tx.send(20).unwrap();

    println!("Received: {:?}", rx.recv());
    println!("Received: {:?}", rx.recv());

    let tx2 = tx.clone();
    tx2.send(30).unwrap();
    println!("Received: {:?}", rx.recv());
}
```

<details>

- `mpsc` 代表多生产者，单消费者。 `Sender` 和 `SyncSender`
  实现了 `Clone`（所以你可以创建多个生产者），但是 `Receiver` 没有。
- `send()` 和 `recv()` 返回 `Result`。如果它们返回 `Err`，意味着相对应的 `Sender` 或 `Receiver` 已经被丢弃，通道也就关闭了。

</details>
