---
minutes: 10
translated_at: '2024-03-26T10:05:09.545Z'
---

# 选项

我们已经见过一些 `Option<T>` 的用法。它存储类型为 `T` 的值或无。例如，[`String::find`](https://doc.rust-lang.org/stable/std/string/struct.String.html#method.find) 返回一个 `Option<usize>`。

```rust,editable,should_panic
fn main() {
    let name = "Löwe 老虎 Léopard Gepardi";
    let mut position: Option<usize> = name.find('é');
    println!("find 返回 {position:?}");
    assert_eq!(position.unwrap(), 14);
    position = name.find('Z');
    println!("find 返回 {position:?}");
    assert_eq!(position.expect("字符未找到"), 0);
}
```

<details>

- `Option` 广泛用于标准库之外。
- `unwrap` 会返回 `Option` 中的值，或触发 panic。`expect` 类似，但会带一个错误信息。
  - 你可以对 None 触发 panic，但你不能“意外地”忘记检查 None。
  - 当草拟一些东西时到处使用 `unwrap`/`expect` 是很常见的，但生产代码通常以更优雅的方式处理 `None`。
- 利基优化意味着 `Option<T>` 在内存中的大小往往与 `T` 相同。

</details>
