---
translated_at: '2024-03-26T11:07:32.029Z'
---

# 示例

让我们看看 `Arc` 和 `Mutex` 的实际应用：

```rust,editable,compile_fail
use std::thread;
// use std::sync::{Arc, Mutex};

fn main() {
    let v = vec![10, 20, 30];
    let handle = thread::spawn(|| {
        v.push(10);
    });
    v.push(1000);

    handle.join().unwrap();
    println!("v: {v:?}");
}
```

<details>

可能的解决方案：

```rust,editable
use std::sync::{Arc, Mutex};
use std::thread;

fn main() {
    let v = Arc::new(Mutex::new(vec![10, 20, 30]));

    let v2 = Arc::clone(&v);
    let handle = thread::spawn(move || {
        let mut v2 = v2.lock().unwrap();
        v2.push(10);
    });

    {
        let mut v = v.lock().unwrap();
        v.push(1000);
    }

    handle.join().unwrap();

    println!("v: {v:?}");
}
```

值得注意的地方：

- `v` 被同时包裹在 `Arc` 和 `Mutex` 中，因为它们解决的问题是正交的。
  - 将 `Mutex` 包裹在 `Arc` 中是一个常见的模式，用于在多线程间共享可变状态。
- `v: Arc<_>` 需要被克隆为 `v2`，之后才能被移动到另一个线程中。注意 `move` 被添加到了 lambda 函数签名中。
- 引入块以尽可能缩小 `LockGuard` 的作用域。

</details>
