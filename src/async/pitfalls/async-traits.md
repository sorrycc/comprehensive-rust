---
translated_at: '2024-03-26T11:52:43.948Z'
---

# 异步特性

在特性中使用异步方法直至最近才被稳定化，在 1.75 版本中。这要求对特性使用返回位置的 `impl Trait`（RPIT）的支持，因为 `async fn` 的语法糖包括 `-> impl Future<Output = ...>`。

然而，即使在今天有了原生支持，围绕特性中的 `async fn` 和 RPIT 仍有一些陷阱：

- 返回位置的 impl Trait 捕获所有作用域生命周期（因此无法表达某些借用模式）
  
- 其方法使用返回位置的 `impl trait` 或 `async` 的特性不兼容 `dyn`。

如果我们确实需要 `dyn` 支持，crates [async_trait](https://docs.rs/async-trait/latest/async_trait/) 通过宏提供了一种解决方法，不过它有一些注意事项：

```rust,editable,compile_fail
use async_trait::async_trait;
use std::time::Instant;
use tokio::time::{sleep, Duration};

#[async_trait]
trait Sleeper {
    async fn sleep(&self);
}

struct FixedSleeper {
    sleep_ms: u64,
}

#[async_trait]
impl Sleeper for FixedSleeper {
    async fn sleep(&self) {
        sleep(Duration::from_millis(self.sleep_ms)).await;
    }
}

async fn run_all_sleepers_multiple_times(
    sleepers: Vec<Box<dyn Sleeper>>,
    n_times: usize,
) {
    for _ in 0..n_times {
        println!("正在运行所有的 sleeper..");
        for sleeper in &sleepers {
            let start = Instant::now();
            sleeper.sleep().await;
            println!("睡眠了 {}ms", start.elapsed().as_millis());
        }
    }
}

#[tokio::main]
async fn main() {
    let sleepers: Vec<Box<dyn Sleeper>> = vec![
        Box::new(FixedSleeper { sleep_ms: 50 }),
        Box::new(FixedSleeper { sleep_ms: 100 }),
    ];
    run_all_sleepers_multiple_times(sleepers, 5).await;
}
```

<details>

- `async_trait` 易于使用，但请注意，它使用堆分配来实现这一点。这种堆分配有性能开销。

- `async trait` 的语言支持挑战深入到 Rust 的深处，可能不值得深入描述。如果您有兴趣深入了解，Niko Matsakis 在 [这篇帖子](https://smallcultfollowing.com/babysteps/blog/2019/10/26/async-fn-in-traits-are-hard/) 中解释得很好。


- 尝试创建一个新的 sleeper 结构体，让它随机休眠一段时间，并将其添加到 Vec 中。

</details>
