---
minutes: 5
translated_at: '2024-03-26T10:14:01.365Z'
---

# `Rc`

[`Rc`][1] 是一个引用计数的共享指针。当你需要从多个地方引用同一数据时，请使用它：

```rust,editable
use std::rc::Rc;

fn main() {
    let a = Rc::new(10);
    let b = Rc::clone(&a);

    println!("a: {a}");
    println!("b: {b}");
}
```

- 如果你在多线程环境中，请参阅 [`Arc`][2] 和 [`Mutex`][3]。
- 你可以把共享指针 _降级为_ [`Weak`][4] 指针以创建循环引用，这将会被正确地释放。

[1]: https://doc.rust-lang.org/std/rc/struct.Rc.html
[2]: ../concurrency/shared_state/arc.md
[3]: https://doc.rust-lang.org/std/sync/struct.Mutex.html
[4]: https://doc.rust-lang.org/std/rc/struct.Weak.html

<details>

- `Rc` 的计数确保了只要有引用存在，其包含的值就是有效的。
- Rust 中的 `Rc` 类似于 C++ 中的 `std::shared_ptr`。
- `Rc::clone` 成本低廉：它创建一个指向同一内存分配的指针并增加引用计数。它不会进行深度克隆，在寻找代码性能问题时通常可以忽略。
- `make_mut` 在必要时实际上会克隆内部值（"写时克隆"）并返回一个可变引用。
- 使用 `Rc::strong_count` 来检查引用计数。
- `Rc::downgrade` 提供了一个 _弱引用计数_ 的对象，以创建能够被正确释放的循环引用（可能与 `RefCell` 结合使用）。

</details>
