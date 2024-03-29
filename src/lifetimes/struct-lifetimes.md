---
minutes: 5
translated_at: '2024-03-26T10:38:03.508Z'
---

# 数据结构中的生命周期

如果数据类型存储了借用的数据，它必须被标记上一个生命周期：

```rust,editable
#[derive(Debug)]
struct Highlight<'doc>(&'doc str);

fn erase(text: String) {
    println!("Bye {text}!");
}

fn main() {
    let text = String::from("The quick brown fox jumps over the lazy dog.");
    let fox = Highlight(&text[4..19]);
    let dog = Highlight(&text[35..43]);
    // erase(text);
    println!("{fox:?}");
    println!("{dog:?}");
}
```

<details>

- 在上述示例中，`Highlight` 上的标注强制要求包含的 `&str` 底层数据至少要和使用该数据的 `Highlight` 实例有相同的生命周期。
- 如果 `text` 在 `fox`（或 `dog`）的生命周期结束之前被消耗掉，借用检查器会抛出一个错误。
- 拥有借用数据的类型强迫用户持有原始数据。这对于创建轻量级视图可能很有用，但通常使它们更难以使用。
- 尽可能使数据结构直接拥有其数据。
- 一些内部含有多个引用的结构体可以有多于一个的生命周期标注。如果需要描述引用之间的生命周期关系，除了结构体本身的生命周期之外，这可能是必需的。这些是非常高级的用例。

</details>
