---
translated_at: '2024-03-26T11:05:21.761Z'
---

# 共享状态

Rust 使用类型系统来强制同步共享数据。这主要通过两种类型完成：

- [`Arc<T>`][1]，原子引用计数 `T`：处理线程间的共享，并在最后一个引用被丢弃时负责释放 `T`，
- [`Mutex<T>`][2]：确保对 `T` 值的互斥访问。

[1]: https://doc.rust-lang.org/std/sync/struct.Arc.html
[2]: https://doc.rust-lang.org/std/sync/struct.Mutex.html
