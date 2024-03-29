---
minutes: 8
translated_at: '2024-03-26T10:35:49.720Z'
---

# `Drop` 特征

实现了 [`Drop`][1] 特征的值可以指定当它们离开作用域时运行的代码：

```rust,editable
struct Droppable {
    name: &'static str,
}

impl Drop for Droppable {
    fn drop(&mut self) {
        println!("Dropping {}", self.name);
    }
}

fn main() {
    let a = Droppable { name: "a" };
    {
        let b = Droppable { name: "b" };
        {
            let c = Droppable { name: "c" };
            let d = Droppable { name: "d" };
            println!("Exiting block B");
        }
        println!("Exiting block A");
    }
    drop(a);
    println!("Exiting main");
}
```

<details>

- 注意 `std::mem::drop` 和 `std::ops::Drop::drop` 不是同一个东西。
- 值会在离开作用域时自动被丢弃。
- 当一个值被丢弃时，如果它实现了 `std::ops::Drop`，那么其 `Drop::drop` 的实现将会被调用。
- 其所有字段接下来也会被丢弃，无论它是否实现了 `Drop`。
- `std::mem::drop` 只是一个空的函数，可以接受任何值。其重要性在于它取得了值的所有权，因此在其作用域结束时它会被丢弃。这使得它成为了一种便捷方式，可以显式地提前丢弃值，比它们原本的离开作用域更早。
  - 这对于在 `drop` 时进行一些工作的对象很有用：释放锁、关闭文件等。

讨论点：

- 为什么 `Drop::drop` 不取 `self`？
  - 简短答案：如果它这样做了，那么 `std::mem::drop` 将在块的结尾被调用，导致又一次调用 `Drop::drop`，进而引起栈溢出！
- 尝试将 `drop(a)` 替换为 `a.drop()`。

</details>

[1]: https://doc.rust-lang.org/std/ops/trait.Drop.html
