---
translated_at: '2024-03-26T11:45:37.168Z'
---

# 任务

Rust 有一个任务系统，这是一种轻量级线程的形式。

任务有一个单一的顶层 future，执行器轮询以取得进展。
那个 future 可能有一个或多个嵌套的 future，它的 `poll` 方法会被轮询，
这大致对应于一个调用栈。通过轮询多个子 future，可以在任务内实现并发，
比如竞争定时器和 I/O 操作。

```rust,compile_fail
use tokio::io::{self, AsyncReadExt, AsyncWriteExt};
use tokio::net::TcpListener;

#[tokio::main]
async fn main() -> io::Result<()> {
    let listener = TcpListener::bind("127.0.0.1:0").await?;
    println!("监听端口 {}", listener.local_addr()?.port());

    loop {
        let (mut socket, addr) = listener.accept().await?;

        println!("来自 {addr:?} 的连接");

        tokio::spawn(async move {
            socket.write_all(b"你是谁？\n").await.expect("socket 错误");

            let mut buf = vec![0; 1024];
            let name_size = socket.read(&mut buf).await.expect("socket 错误");
            let name = std::str::from_utf8(&buf[..name_size]).unwrap().trim();
            let reply = format!("感谢你拨入，{name}！\n");
            socket.write_all(reply.as_bytes()).await.expect("socket 错误");
        });
    }
}
```

<details>

将此示例复制到你准备好的 `src/main.rs` 中并从那里运行。

尝试使用像 [nc](https://www.unix.com/man-page/linux/1/nc/) 或 [telnet](https://www.unix.com/man-page/linux/1/telnet/) 这样的 TCP 连接工具连接到它。

- 要求学生想象一下，如果有几个已连接的客户端，示例服务器的状态将会是什么样的。存在哪些任务？它们的 Futures 是什么？

- 这是我们第一次看到 `async` 块。这类似于闭包，但不接受任何参数。它的返回值是一个 Future，类似于一个 `async fn`。

- 将 async 块重构为函数，并使用 `?` 改进错误处理。

</details>
