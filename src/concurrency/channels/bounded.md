---
translated_at: '2024-03-26T11:09:59.770Z'
---

# 有界通道

使用有界（同步）通道时，`send` 可能会阻塞当前线程：

```rust,editable
use std::sync::mpsc;
use std::thread;
use std::time::Duration;

fn main() {
    let (tx, rx) = mpsc::sync_channel(3);

    thread::spawn(move || {
        let thread_id = thread::current().id();
        for i in 1..10 {
            tx.send(format!("Message {i}")).unwrap();
            println!("{thread_id:?}: 发送了消息 {i}");
        }
        println!("{thread_id:?}: 完成");
    });
    thread::sleep(Duration::from_millis(100));

    for msg in rx.iter() {
        println!("主线程：收到了 {msg}");
    }
}
```

<details>

- 调用 `send` 时，如果通道中没有新消息的空间，将会阻塞当前线程。如果没有其他线程从通道中读取，线程可能会被无限期地阻塞。
- 如果通道关闭，则调用 `send` 会因为错误而中止（这就是为什么它返回 `Result` 的原因）。当接收者被丢弃时，通道就会关闭。
- 容量为零的有界通道被称为“会合通道”。每一次发送都会阻塞当前线程，直到另一个线程调用 `recv`。

</details>
