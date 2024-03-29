---
translated_at: '2024-03-26T11:03:51.148Z'
---

# `for`

[`for` 循环](https://doc.rust-lang.org/std/keyword.for.html) 用于迭代值的范围或集合中的元素：

```rust,editable
fn main() {
    for x in 1..5 {
        println!("x: {x}");
    }

    for elem in [1, 2, 3, 4, 5] {
        println!("elem: {elem}");
    }
}
```

<details>

- 在底层，`for` 循环使用了一个名为 “迭代器” 的概念来处理不同类型的范围 / 集合的迭代。迭代器稍后会更详细地讨论。
- 注意 `for` 循环只迭代到 `4`。展示 `1..=5` 语法来进行包含终值的范围。

</details>
