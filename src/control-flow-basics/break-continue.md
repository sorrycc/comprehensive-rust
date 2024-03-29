---
minutes: 4
translated_at: '2024-03-26T11:03:16.452Z'
---

# `break` 和 `continue`

如果你想立即开始下一次迭代，请使用 [`continue`](https://doc.rust-lang.org/reference/expressions/loop-expr.html#continue-expressions)。

如果你想提前退出任何类型的循环，请使用 [`break`](https://doc.rust-lang.org/reference/expressions/loop-expr.html#break-expressions)。对于 `loop`，这可以带一个可选表达式，成为 `loop` 表达式的值。

```rust,editable
fn main() {
    let mut i = 0;
    loop {
        i += 1;
        if i > 5 {
            break;
        }
        if i % 2 == 0 {
            continue;
        }
        println!("{}", i);
    }
}
```
