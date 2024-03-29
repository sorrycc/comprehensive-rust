---
translated_at: '2024-03-26T11:50:22.614Z'
---

# 取消

放弃一个 future 意味着它将不再被轮询。这被称为 _取消_，它可以在任何 `await` 点发生。需要小心确保即使 future 被取消，系统也能正确工作。例如，它不应该死锁或丢失数据。

```rust,editable,compile_fail
use std::io::{self, ErrorKind};
use std::time::Duration;
use tokio::io::{AsyncReadExt, AsyncWriteExt, DuplexStream};

struct LinesReader {
    stream: DuplexStream,
}

impl LinesReader {
    fn new(stream: DuplexStream) -> Self {
        Self { stream }
    }

    async fn next(&mut self) -> io::Result<Option<String>> {
        let mut bytes = Vec::new();
        let mut buf = [0];
        while self.stream.read(&mut buf[..]).await? != 0 {
            bytes.push(buf[0]);
            if buf[0] == b'\n' {
                break;
            }
        }
        if bytes.is_empty() {
            return Ok(None);
        }
        let s = String::from_utf8(bytes)
            .map_err(|_| io::Error::new(ErrorKind::InvalidData, "not UTF-8"))?;
        Ok(Some(s))
    }
}

async fn slow_copy(source: String, mut dest: DuplexStream) -> std::io::Result<()> {
    for b in source.bytes() {
        dest.write_u8(b).await?;
        tokio::time::sleep(Duration::from_millis(10)).await
    }
    Ok(())
}

#[tokio::main]
async fn main() -> std::io::Result<()> {
    let (client, server) = tokio::io::duplex(5);
    let handle = tokio::spawn(slow_copy("hi\nthere\n".to_owned(), client));

    let mut lines = LinesReader::new(server);
    let mut interval = tokio::time::interval(Duration::from_millis(60));
    loop {
        tokio::select! {
            _ = interval.tick() => println!("tick!"),
            line = lines.next() => if let Some(l) = line? {
                print!("{}", l)
            } else {
                break
            },
        }
    }
    handle.await.unwrap()?;
    Ok(())
}
```

<details>

- 编译器并不帮助确保取消安全性。你需要阅读 API 文档，并考虑你的 `async fn` 保持什么状态。

- 与 `panic` 和 `?` 不同，取消（cancellation）是正常控制流的一部分（相对于错误处理而言）。

- 该示例丢失了字符串的部分。

  - 无论何时 `tick()` 分支首先结束，`next()` 和它的 `buf` 都会被丢弃。

  - 通过将 `buf` 作为结构体的一部分，可以使 `LinesReader` 对取消操作安全：
    ```rust,compile_fail
    struct LinesReader {
        stream: DuplexStream,
        bytes: Vec<u8>,
        buf: [u8; 1],
    }

    impl LinesReader {
        fn new(stream: DuplexStream) -> Self {
            Self { stream, bytes: Vec::new(), buf: [0] }
        }
        async fn next(&mut self) -> io::Result<Option<String>> {
            // 使用 self. 前缀 buf 和 bytes。
            // ...
            let raw = std::mem::take(&mut self.bytes);
            let s = String::from_utf8(raw)
            // ...
        }
    }
    ```

- [`Interval::tick`](https://docs.rs/tokio/latest/tokio/time/struct.Interval.html#method.tick)
  是对取消操作安全的，因为它会跟踪是否有 tick 被“送达”。

- [`AsyncReadExt::read`](https://docs.rs/tokio/latest/tokio/io/trait.AsyncReadExt.html#method.read)
  是对取消操作安全的，因为它要么返回数据，要么不读取数据。

- [`AsyncBufReadExt::read_line`](https://docs.rs/tokio/latest/tokio/io/trait.AsyncBufReadExt.html#method.read_line)
  与示例类似，并且_不是_对取消操作安全的。有关详细信息和替代方案，请参阅其文档。

</details>
