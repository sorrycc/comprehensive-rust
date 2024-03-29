---
minutes: 5
translated_at: '2024-03-26T09:59:06.877Z'
---

# 元组

<!-- mdbook-xgettext: skip -->

```rust,editable
fn main() {
    let t: (i8, bool) = (7, true);
    println!("t.0: {}", t.0);
    println!("t.1: {}", t.1);
}
```

<details>

- 像数组一样，元组具有固定的长度。

- 元组将不同类型的值组合在一起，形成复合类型。

- 可以通过点号和值的索引访问元组的字段，例如 `t.0`，`t.1`。

- 空元组 `()` 被称为“单元类型”，表示没有返回值，类似于其他语言中的 `void`。

</details>
