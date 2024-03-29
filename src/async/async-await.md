---
translated_at: '2024-03-26T11:48:02.257Z'
---

# `async`/`await`

从高层次上来看，异步 Rust 代码看起来非常像“普通”的顺序代码：

```rust,editable,compile_fail
use futures::executor::block_on;

async fn count_to(count: i32) {
    for i in 1..=count {
        println!("数到：{i}！");
    }
}

async fn async_main(count: i32) {
    count_to(count).await;
}

fn main() {
    block_on(async_main(10));
}
```

<details>

关键点：

- 注意，这是一个简化的例子，用以展示语法。其中并没有长时间运行的操作，也没有真正的并发！

- 异步调用的返回类型是什么？
  - 在 `main` 中使用 `let future: () = async_main(10);` 来查看类型。

- “async” 关键字是语法糖。编译器将返回类型替换为 future。

- 你不能把 `main` 函数变成异步的，除非给编译器一些额外的指令来说明如何使用返回的 future。

- 你需要一个执行器来运行异步代码。`block_on` 阻塞当前线程，直到提供的 future 完成运行。

- `.await` 异步地等待另一个操作的完成。与 `block_on` 不同，`.await` 不会阻塞当前线程。

- 只能在 `async` 函数（或稍后介绍的块）内部使用 `.await`。

</details>
