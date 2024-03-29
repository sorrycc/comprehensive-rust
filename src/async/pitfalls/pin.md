---
translated_at: '2024-03-26T11:49:35.979Z'
---

# `Pin`

异步块和函数返回实现了 `Future` trait 的类型。返回的类型是编译器转换的结果，将局部变量转换为存储在 future 内部的数据。

其中一些变量可能持有指向其他局部变量的指针。因此，future 绝不应该被移动到其他内存位置，因为这会使这些指针无效。

为了防止在内存中移动 future 类型，它只能通过一个固定的指针被调用。`Pin` 是一个围绕引用的封装器，它禁止所有会将其指向的实例移动到不同内存位置的操作。

```rust,editable,compile_fail
use tokio::sync::{mpsc, oneshot};
use tokio::task::spawn;
use tokio::time::{sleep, Duration};

// 一个工作项。在这种情况下，只是休眠给定的时间，然后在 `respond_on` 通道上响应消息。
#[derive(Debug)]
struct Work {
    input: u32,
    respond_on: oneshot::Sender<u32>,
}

// 一个工人，它监听队列上的工作并执行它。
async fn worker(mut work_queue: mpsc::Receiver<Work>) {
    let mut iterations = 0;
    loop {
        tokio::select! {
            Some(work) = work_queue.recv() => {
                sleep(Duration::from_millis(10)).await; // 假装工作。
                work.respond_on
                    .send(work.input * 1000)
                    .expect("发送响应失败");
                iterations += 1;
            }
            // TODO: 每 100ms 报告迭代次数
        }
    }
}

// 一个请求者，它请求工作并等待其完成。
async fn do_work(work_queue: &mpsc::Sender<Work>, input: u32) -> u32 {
    let (tx, rx) = oneshot::channel();
    work_queue
        .send(Work { input, respond_on: tx })
        .await
        .expect("发送到工作队列失败");
    rx.await.expect("等待响应失败")
}

#[tokio::main]
async fn main() {
    let (tx, rx) = mpsc::channel(10);
    spawn(worker(rx));
    for i in 0..100 {
        let resp = do_work(&tx, i).await;
        println!("迭代 {i} 的工作结果：{resp}");
    }
}
```

<details>

- 你可能认识到这是 actor 模式的一个例子。Actor 通常会在循环中调用 `select!`。

- 这是对之前几课内容的总结，所以请慢慢来。

  - 天真地在 `select!` 里添加一个 `_ = sleep(Duration::from_millis(100)) => { println!(..) }`。这将永远不会被执行。为什么？

  - 相反，在循环外面添加一个包含该 future 的 `timeout_fut`：

    ```rust,compile_fail
    let mut timeout_fut = sleep(Duration::from_millis(100));
    loop {
        select! {
            ..,
            _ = timeout_fut => { println!(..); },
        }
    }
    ```
  - 这仍然无法工作。跟随编译器错误，向 `select!` 中的 `timeout_fut` 添加 `&mut`，以解决移动问题，然后使用 `Box::pin`：

    ```rust,compile_fail
    let mut timeout_fut = Box::pin(sleep(Duration::from_millis(100)));
    loop {
        select! {
            ..,
            _ = &mut timeout_fut => { println!(..); },
        }
    }
    ```

  - 这样可以编译，但一旦超时到期，它在每次迭代时都是 `Poll::Ready`（融合 future 可以帮助解决这个问题）。更新代码以在 `timeout_fut` 过期时重置它。

- Box 在堆上分配。在某些情况下，`std::pin::pin!`（只是最近稳定下来，旧代码经常使用 `tokio::pin!`）也是一个选项，但这对于需要重新分配的 future 来说很难使用。

- 另一种选择是完全不使用 `pin`，而是启动另一个任务，该任务每 100 毫秒向 `oneshot` 频道发送一次。

- 包含指向自身指针的数据被称为自引用数据。通常，Rust 借用检查器会阻止自引用数据移动，因为引用不能比它们指向的数据活得更久。然而，异步代码块和函数的代码转换不受借用检查器的验证。

- `Pin` 是围绕引用的一个包装器。使用固定指针，对象不能从原地移动。然而，它仍然可以通过一个未固定的指针被移动。
</details>

- `Future` 特性的 `poll` 方法使用 `Pin<&mut Self>` 而不是 `&mut Self` 来引用实例。这就是为什么它只能在固定指针上被调用。

</details>
