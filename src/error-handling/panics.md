---
minutes: 3
translated_at: '2024-03-26T11:00:16.752Z'
---

# 恐慌

Rust 用 “恐慌 (panic)” 来处理致命错误。

如果在运行时发生了致命错误，Rust 将触发恐慌：

```rust,editable,should_panic
fn main() {
    let v = vec![10, 20, 30];
    println!("v[100]: {}", v[100]);
}
```

- 恐慌用于不可恢复且意外的错误。
  - 恐慌是程序中缺陷的症状。
  - 像边界检查失败这样的运行时故障可以引发恐慌
  - 断言（例如 `assert!`）在失败时会触发恐慌
  - 可以使用 `panic!` 宏来进行特定目的的恐慌。
- 恐慌会“展开 (unwind)”堆栈，丢弃值，就像函数已经返回一样。
- 如果崩溃不可接受，请使用非恐慌 API（例如 `Vec::get`）。

<details>

默认情况下，恐慌会导致堆栈展开。展开过程是可以捕获的：

```rust,editable
use std::panic;

fn main() {
    let result = panic::catch_unwind(|| "No problem here!");
    println!("{result:?}");

    let result = panic::catch_unwind(|| {
        panic!("oh no!");
    });
    println!("{result:?}");
}
```

- 捕获是不常见的；不要尝试用 `catch_unwind` 来实现异常！
- 在服务器中，即便单个请求崩溃，服务器应该继续运行，这时它可能是有用的。
- 如果在 `Cargo.toml` 中设置了 `panic = 'abort'`，这不会起作用。

</details>
