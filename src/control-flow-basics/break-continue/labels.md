---
translated_at: '2024-03-26T11:04:08.690Z'
---

# 标签

`continue` 和 `break` 都可以可选地使用一个标签参数，该参数用于跳出嵌套循环：

```rust,editable
fn main() {
    let s = [[5, 6, 7], [8, 9, 10], [21, 15, 32]];
    let mut elements_searched = 0;
    let target_value = 10;
    'outer: for i in 0..=2 {
        for j in 0..=2 {
            elements_searched += 1;
            if s[i][j] == target_value {
                break 'outer;
            }
        }
    }
    print!("elements searched: {elements_searched}");
}
```

<details>

- 注意，`loop` 是唯一一个返回非平凡值的循环结构。这是因为它保证至少进入一次（不像 `while` 和 `for` 循环）。

</details>
