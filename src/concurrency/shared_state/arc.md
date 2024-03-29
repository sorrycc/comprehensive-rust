---
translated_at: '2024-03-26T11:07:55.669Z'
---

# `Arc`

[`Arc<T>`][1] 允许通过 `Arc::clone` 实现共享只读访问：

```rust,editable
use std::sync::Arc;
use std::thread;

fn main() {
    let v = Arc::new(vec![10, 20, 30]);
    let mut handles = Vec::new();
    for _ in 1..5 {
        let v = Arc::clone(&v);
        handles.push(thread::spawn(move || {
            let thread_id = thread::current().id();
            println!("{thread_id:?}: {v:?}");
        }));
    }

    handles.into_iter().for_each(|h| h.join().unwrap());
    println!("v: {v:?}");
}
```

[1]: https://doc.rust-lang.org/std/sync/struct.Arc.html

<details>

- `Arc` 代表 "原子引用计数"，一个使用原子操作的线程安全的 `Rc` 版本。
- `Arc<T>` 无论 `T` 是否实现了 `Clone` ，都实现了 `Clone`。只有当 `T` 同时实现了 `Send` 和 `Sync` 时，它们也才会实现。
- `Arc::clone()` 的代价在于执行的原子操作，但之后对 `T` 的使用是自由的。
- 注意避免引用循环，`Arc` 不使用垃圾回收器来检测它们。
  - `std::sync::Weak` 可以帮助解决这个问题。

</details>
