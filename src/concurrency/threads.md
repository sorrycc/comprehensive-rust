---
translated_at: '2024-03-26T11:05:10.499Z'
---

# 线程

Rust 线程的工作原理与其他语言中的线程类似：

```rust,editable
use std::thread;
use std::time::Duration;

fn main() {
    thread::spawn(|| {
        for i in 1..10 {
            println!("子线程计数：{i}!");
            thread::sleep(Duration::from_millis(5));
        }
    });

    for i in 1..5 {
        println!("主线程：{i}");
        thread::sleep(Duration::from_millis(5));
    }
}
```

- 所有线程都是守护线程，主线程不会等待它们。
- 线程崩溃是独立的。
  - 崩溃可以带有负载（payload），可用 `downcast_ref` 解包。

<details>

- Rust 线程 API 与其他语言（例如 C++）看起来没有太大不同。

- 运行示例。
  - 5 毫秒的间隔足够宽松，以至于主线程和生成的线程大致同步执行。
  - 注意到程序在生成的线程到达 10 之前就结束了！
  - 这是因为主线程结束了程序，生成的线程不能使程序持续运行。
    - 如有需要，可与 pthreads/C++ std::thread/boost::thread 相比较。

- 我们如何等待生成的线程完成？
- [`thread::spawn`] 返回一个 `JoinHandle`。查看文档。
  - `JoinHandle` 有一个阻塞的 [`.join()`] 方法。

- 使用 `let handle = thread::spawn(...)` 然后是 `handle.join()` 等待线程结束，让程序计数到 10。

- 如果我们想要返回一个值怎么办？
- 再次查看文档：
  - [`thread::spawn`] 的闭包返回 `T`
  - `JoinHandle` 的 [`.join()`] 返回 `thread::Result<T>`

- 使用 `handle.join()` 的 `Result` 返回值来访问返回的值。

- 那么，其他情况呢？
  - 在线程中触发一个崩溃。注意这不会使 `main` 崩溃。
  - 获取崩溃负载。现在是讨论 [`Any`] 的好时机。

- 现在我们可以从线程返回值了！那输入呢？
  - 在线程闭包中通过引用捕获某个值。
  - 错误信息表明我们必须移动它（move it）。
  - 将其移入，看看我们如何计算然后返回一个派生值。


- 如果我们想要借用？
  - 当主函数返回时，它会终止子线程，但另一个函数只是返回并让它们继续运行。
  - 那将会是栈使用后返回，这违反了内存安全！
  - 我们如何避免这个问题？见下一张幻灯片。

[`Any`]: https://doc.rust-lang.org/std/any/index.html
[`thread::spawn`]: https://doc.rust-lang.org/std/thread/fn.spawn.html
[`.join()`]: https://doc.rust-lang.org/std/thread/struct.JoinHandle.html#method.join

</details>
