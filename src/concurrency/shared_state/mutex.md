---
translated_at: '2024-03-26T11:07:00.477Z'
---

# `Mutex`

[`Mutex<T>`][1] 保证了互斥访问，并允许在只读接口背后对 `T` 进行可变访问（这是
[内部可变性](../../borrowing/interior-mutability) 的另一种形式）：

```rust,editable
use std::sync::Mutex;

fn main() {
    let v = Mutex::new(vec![10, 20, 30]);
    println!("v: {:?}", v.lock().unwrap());

    {
        let mut guard = v.lock().unwrap();
        guard.push(40);
    }

    println!("v: {:?}", v.lock().unwrap());
}
```

注意我们有一个 [`impl<T: Send> Sync for Mutex<T>`][2] 的 blanket 实现。

[1]: https://doc.rust-lang.org/std/sync/struct.Mutex.html
[2]: https://doc.rust-lang.org/std/sync/struct.Mutex.html#impl-Sync-for-Mutex%3CT%3E
[3]: https://doc.rust-lang.org/std/sync/struct.Arc.html

<details>

- Rust 中的 `Mutex` 就像一个只有一个元素的集合 --- 被保护的数据。
  - 在访问被保护的数据之前忘记获取互斥锁是不可能的。
- 通过锁定，你可以从 `&Mutex<T>` 获取一个 `&mut T`。`MutexGuard` 确保 `&mut T` 不会比持有锁的时间长。
- 当且仅当 `T` 实现了 `Send`，`Mutex<T>` 才同时实现 `Send` 和 `Sync`。
- 读写锁的对应物：`RwLock`。
- 为什么 `lock()` 返回一个 `Result`？
  - 如果持有 `Mutex` 的线程发生了恐慌，`Mutex` 会变成 “中毒” 状态，以示它保护的数据可能处于不一致状态。在中毒的互斥锁上调用 `lock()` 会失败，并返回一个 [`PoisonError`]。你可以调用错误的 `into_inner()` 来无论如何恢复数据。

[`PoisonError`]: https://doc.rust-lang.org/std/sync/struct.PoisonError.html

</details>
