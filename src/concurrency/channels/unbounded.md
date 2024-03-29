---
translated_at: '2024-03-26T11:09:25.423Z'
---

# 无界通道

您可以通过 `mpsc::channel()` 获取一个无界且异步的通道：

```rust,editable
use std::sync::mpsc;
use std::thread;
use std::time::Duration;

fn main() {
    let (tx, rx) = mpsc::channel();

    thread::spawn(move || {
        let thread_id = thread::current().id();
        for i in 1..10 {
            tx.send(format!("消息 {i}")).unwrap();
            println!("{thread_id:?}: 已发送消息 {i}");
        }
        println!("{thread_id:?}: 完成");
    });
    thread::sleep(Duration::from_millis(100));

    for msg in rx.iter() {
        println!("主线程: 收到 {msg}");
    }
}
```
