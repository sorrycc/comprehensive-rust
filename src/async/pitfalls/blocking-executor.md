---
translated_at: '2024-03-26T11:51:34.492Z'
---

# 阻塞执行器

大多数异步运行时只允许 IO 任务并发运行。这意味着 CPU 阻塞任务将会阻塞执行器，阻止其他任务的执行。一个简单的解决办法是尽可能使用异步等效方法。

```rust,editable,compile_fail
use futures::future::join_all;
use std::time::Instant;

async fn sleep_ms(start: &Instant, id: u64, duration_ms: u64) {
    std::thread::sleep(std::time::Duration::from_millis(duration_ms));
    println!(
        "future {id} 睡眠了 {duration_ms}ms，完成于 {}ms",
        start.elapsed().as_millis()
    );
}

#[tokio::main(flavor = "current_thread")]
async fn main() {
    let start = Instant::now();
    let sleep_futures = (1..=10).map(|t| sleep_ms(&start, t, t * 10));
    join_all(sleep_futures).await;
}
```

<details>

- 运行代码并注意到 sleep 操作是连续发生的，而不是并发的。

- `"current_thread"` 模式将所有任务都放在单个线程上。这使得效果更加明显，但在多线程模式下，这个问题仍然存在。

- 将 `std::thread::sleep` 替换为 `tokio::time::sleep` 并等待它的结果。

- 另一个解决办法是使用 `tokio::task::spawn_blocking`，它会生成一个实际的线程，并将它的句柄转化为未来，而不会阻塞执行器。

- 你不应该将任务视为 OS 线程。它们之间没有 1 对 1 的映射，大多数执行器会允许许多任务在单个 OS 线程上运行。特别是在通过 FFI 与其他库交互时，这就成问题了，因为那些库可能依赖于线程本地存储或映射到特定的 OS 线程（例如 CUDA）。在这种情况下，推荐使用 `tokio::task::spawn_blocking`。

- 小心使用同步互斥锁。在 `.await` 上持有互斥锁可能会导致另一个任务阻塞，而且那个任务可能在同一个线程上运行。

</details>
