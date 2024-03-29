---
minutes: 10
translated_at: '2024-03-26T10:05:52.428Z'
---

# `HashMap`

具备 HashDoS 攻击保护的标准哈希映射：

```rust,editable
use std::collections::HashMap;

fn main() {
    let mut page_counts = HashMap::new();
    page_counts.insert("Adventures of Huckleberry Finn".to_string(), 207);
    page_counts.insert("Grimms' Fairy Tales".to_string(), 751);
    page_counts.insert("Pride and Prejudice".to_string(), 303);

    if !page_counts.contains_key("Les Misérables") {
        println!(
            "我们知道 {} 本书籍信息，但不包括 Les Misérables。",
            page_counts.len()
        );
    }

    for book in ["Pride and Prejudice", "Alice's Adventure in Wonderland"] {
        match page_counts.get(book) {
            Some(count) => println!("{book}: {count} 页"),
            None => println!("{book} 信息未知。"),
        }
    }

    // 如果找不到，则使用 .entry() 方法插入一个值。
    for book in ["Pride and Prejudice", "Alice's Adventure in Wonderland"] {
        let page_count: &mut i32 = page_counts.entry(book.to_string()).or_insert(0);
        *page_count += 1;
    }

    println!("{page_counts:#?}");
}
```

<details>

- `HashMap` 没有在预导入中定义，需要将其引入作用域。
- 尝试以下几行代码。第一行代码会检查 hashmap 中是否有某本书，如果没有，则返回一个备选值。如果书籍未找到，第二行代码会在 hashmap 中插入这个备选值。

  ```rust,ignore
  let pc1 = page_counts
      .get("Harry Potter and the Sorcerer's Stone")
      .unwrap_or(&336);
  let pc2 = page_counts
      .entry("The Hunger Games".to_string())
      .or_insert(374);
  ```
- 不幸的是，不像 `vec!`，没有一个标准的 `hashmap!` 宏。
  - 尽管如此，自 Rust 1.56 起，HashMap 实现了 [`From<[(K, V); N]>`][1]，
    这使得我们可以轻松地从字面量数组初始化一个哈希映射：

    ```rust,ignore
    let page_counts = HashMap::from([
      ("Harry Potter and the Sorcerer's Stone".to_string(), 336),
      ("The Hunger Games".to_string(), 374),
    ]);
    ```

- 另外，HashMap 也可以通过任何产生键值对元组的 `Iterator` 构建。
- 我们展示的是 `HashMap<String, i32>`，并避免使用 `&str` 作为键，以使示例简化。当然，集合中可以使用引用，但这可能会导致与借用检查器的复杂情况。
  - 尝试从上面的例子中移除 `to_string()`，看看它是否还能编译。你认为我们可能会在哪里遇到问题？

- 这种类型有几种“特定方法”的返回类型，例如 `std::collections::hash_map::Keys`。这些类型经常出现在 Rust 文档的搜索中。向学生展示这个类型的文档，以及返回到 `keys` 方法的有用链接。

[1]: https://doc.rust-lang.org/std/collections/hash_map/struct.HashMap.html#impl-From%3C%5B(K,+V);+N%5D%3E-for-HashMap%3CK,+V,+RandomState%3E

</details>
