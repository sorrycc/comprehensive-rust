---
translated_at: '2024-03-26T11:35:00.358Z'
---

# `spin`

`std::sync::Mutex` 和其他来自 `std::sync` 的同步原语在 `core` 或 `alloc` 中不可用。我们如何管理同步或内部可变性，例如在不同 CPU 之间共享状态？

[`spin`][1] crate 提供了许多这些原语的基于自旋锁的等价物。

<!-- mdbook-xgettext: skip -->

```rust,editable,compile_fail
use spin::mutex::SpinMutex;

static counter: SpinMutex<u32> = SpinMutex::new(0);

fn main() {
    println!("计数: {}", counter.lock());
    *counter.lock() += 2;
    println!("计数: {}", counter.lock());
}
```

<details>

- 如果您在中断处理程序中加锁，请小心避免死锁。
- `spin` 还有一个票据锁互斥体实现；`std::sync` 中的 `RwLock`、`Barrier` 和 `Once` 的等价物；以及用于懒惰初始化的 `Lazy`。
- [`once_cell`][2] crate 也为晚期初始化提供了一些有用的类型，采用与 `spin::once::Once` 略有不同的方法。
- Rust Playground 包含了 `spin`，因此这个示例能够很好地在线运行。

</details>

[1]: https://crates.io/crates/spin
[2]: https://crates.io/crates/once_cell
