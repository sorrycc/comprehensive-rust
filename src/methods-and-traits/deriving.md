---
minutes: 3
translated_at: '2024-03-26T10:30:54.926Z'
---

# 派生

支持的特性可以自动为你的自定义类型实现，如下所示：

```rust,editable
#[derive(Debug, Clone, Default)]
struct Player {
    name: String,
    strength: u8,
    hit_points: u8,
}

fn main() {
    let p1 = Player::default(); // Default 特性增加了 `default` 构造器。
    let mut p2 = p1.clone(); // Clone 特性增加了 `clone` 方法。
    p2.name = String::from("EldurScrollz");
    // Debug 特性增加了使用 `{:?}` 打印的支持。
    println!("{:?} vs. {:?}", p1, p2);
}
```

<details>

派生是通过宏实现的，许多 crate 提供了有用的派生宏来添加有用的功能。例如，`serde` 可以使用 `#[derive(Serialize)]` 为结构体派生序列化支持。

</detail>
