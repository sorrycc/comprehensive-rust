---
translated_at: '2024-03-26T11:48:31.843Z'
---

# Tokio

Tokio 提供：

- 一个用于执行异步代码的多线程运行时。
- 标准库的异步版本。
- 一个庞大的库生态系统。

```rust,editable,compile_fail
use tokio::time;

async fn count_to(count: i32) {
    for i in 1..=count {
        println!("Count in task: {i}!");
        time::sleep(time::Duration::from_millis(5)).await;
    }
}

#[tokio::main]
async fn main() {
    tokio::spawn(count_to(10));

    for i in 1..5 {
        println!("Main task: {i}");
        time::sleep(time::Duration::from_millis(5)).await;
    }
}
```

<details>

- 使用 `tokio::main` 宏，我们现在可以使 `main` 异步。

- `spawn` 函数创建一个新的，并发的“任务”。

- 注意：`spawn` 接受一个 `Future`，你不需要在 `count_to` 上调用 `.await`。

**进一步探索：**

- 为什么 `count_to` 通常不会计数到 10？这是异步取消的一个例子。`tokio::spawn` 返回一个句柄，可以等待它完成。

- 尝试用 `count_to(10).await` 替代生成。

- 尝试等待 `tokio::spawn` 返回的任务。

</details>
