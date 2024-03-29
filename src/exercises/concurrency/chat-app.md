---
translated_at: '2024-03-26T10:50:59.572Z'
---

# 广播聊天应用

在这个练习中，我们想利用我们的新知识来实现一个广播聊天应用。我们有一个聊天服务器，客户端连接到这个服务器并发布他们的消息。客户端从标准输入读取用户消息，并将它们发送到服务器。聊天服务器接收到每条消息后，将其广播给所有客户端。

为此，我们在服务器上使用 [一个广播通道][1]，并使用 [`tokio_websockets`][2] 来处理客户端和服务器之间的通信。

创建一个新的 Cargo 项目并添加以下依赖：

_Cargo.toml_：

<!-- File Cargo.toml -->

```toml
{{#include chat-async/Cargo.toml}}
```

## 所需的 API

你将需要以下来自 `tokio` 和 [`tokio_websockets`][2] 的功能。花几分钟时间熟悉一下这些 API。

- [StreamExt::next()][3] 由 `WebSocketStream` 实现：用于从一个 Websocket 流中异步读取消息。
- [SinkExt::send()][4] 由 `WebSocketStream` 实现：用于在一个 Websocket 流上异步发送消息。
- [Lines::next_line()][5]：用于从标准输入异步读取用户消息。
- [Sender::subscribe()][6]：用于订阅一个广播频道。

## 两个二进制文件

通常在一个 Cargo 项目中，你只能有一个二进制文件和一个 `src/main.rs` 文件。在这个项目中，我们需要两个二进制文件。一个用于客户端，另一个用于服务器。你可以把它们做成两个独立的 Cargo 项目，但我们将把它们放在一个带有两个二进制文件的单一 Cargo 项目中。为了使它工作，客户端和服务器代码应该放在 `src/bin` 下（见[文档][7]）。

将以下服务器和客户端代码复制到 `src/bin/server.rs` 和 `src/bin/client.rs` 中，分别如下。你的任务是按照下面的描述完成这些文件。

_src/bin/server.rs_：

<!-- File src/bin/server.rs -->

```rust,compile_fail
{{#include chat-async/src/bin/server.rs:setup}}

{{#include chat-async/src/bin/server.rs:handle_connection}}

    // TODO: 有关提示，请参见下面的任务描述。

{{#include chat-async/src/bin/server.rs:main}}
```

_src/bin/client.rs_：

<!-- 文件 src/bin/client.rs -->

```rust,compile_fail
{{#include chat-async/src/bin/client.rs:setup}}

    // 待办事项：获取提示，请查看下面任务的描述。

}
```

## 运行二进制文件

使用以下命令运行服务器：

```shell
cargo run --bin server
```

然后使用以下命令运行客户端：

```shell
cargo run --bin client
```

## 任务

- 在 `src/bin/server.rs` 中实现 `handle_connection` 函数。
  - 提示：使用 `tokio::select!` 同时并发执行两个任务，
    在一个持续的循环中。一个任务从客户端接收消息并广播它们，
    另一个将服务器收到的消息发送给客户端。
- 在 `src/bin/client.rs` 中完成主函数。
  - 提示：像之前一样，使用 `tokio::select!` 在一个持续的循环中同时并发执行
    两个任务：（1）从标准输入读取用户消息并发送给服务器，（2）接收服务器的消息，并
    为用户显示它们。
- 可选：完成后，更改代码以广播消息给所有客户端，但消息发送者除外。

[1]: https://docs.rs/tokio/latest/tokio/sync/broadcast/fn.channel.html
[2]: https://docs.rs/tokio-websockets/
[3]: https://docs.rs/futures-util/0.3.28/futures_util/stream/trait.StreamExt.html#method.next
[4]: https://docs.rs/futures-util/0.3.28/futures_util/sink/trait.SinkExt.html#method.send
[5]: https://docs.rs/tokio/latest/tokio/io/struct.Lines.html#method.next_line
[6]: https://docs.rs/tokio/latest/tokio/sync/broadcast/struct.Sender.html#method.subscribe
[7]: https://doc.rust-lang.org/cargo/reference/cargo-targets.html#binaries
