---
translated_at: '2024-03-26T11:06:05.966Z'
---

# 作用域线程

普通线程不能从其环境中借用：

```rust,editable,compile_fail
use std::thread;

fn foo() {
    let s = String::from("Hello");
    thread::spawn(|| {
        println!("Length: {}", s.len());
    });
}

fn main() {
    foo();
}
```

然而，你可以使用[作用域线程][1]来实现这一点：

```rust,editable
use std::thread;

fn main() {
    let s = String::from("Hello");

    thread::scope(|scope| {
        scope.spawn(|| {
            println!("Length: {}", s.len());
        });
    });
}
```

[1]: https://doc.rust-lang.org/std/thread/fn.scope.html

<details>

- 其原因在于当 `thread::scope` 函数完成时，所有线程都保证会被 join，所以它们能够返回借用的数据。
- 正常的 Rust 借用规则依然适用：你可以由一个线程可变借用，或者由任意数量的线程不可变借用。

</details>
