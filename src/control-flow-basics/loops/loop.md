---
translated_at: '2024-03-26T11:03:37.474Z'
---

# `loop`

[`loop` 语句](https://doc.rust-lang.org/std/keyword.loop.html) 就是无限循环，直到遇到 `break`。

```rust,editable
fn main() {
    let mut i = 0;
    loop {
        i += 1;
        println!("{i}");
        if i > 100 {
            break;
        }
    }
}
```
