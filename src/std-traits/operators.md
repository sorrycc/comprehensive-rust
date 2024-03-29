---
minutes: 10
translated_at: '2024-03-26T10:08:15.980Z'
---

# 运算符

运算符重载通过 [`std::ops`][1] 中的特征来实现：

```rust,editable
#[derive(Debug, Copy, Clone)]
struct Point {
    x: i32,
    y: i32,
}

impl std::ops::Add for Point {
    type Output = Self;

    fn add(self, other: Self) -> Self {
        Self { x: self.x + other.x, y: self.y + other.y }
    }
}

fn main() {
    let p1 = Point { x: 10, y: 20 };
    let p2 = Point { x: 100, y: 200 };
    println!("{:?} + {:?} = {:?}", p1, p2, p1 + p2);
}
```

<details>

讨论要点：

- 你可以为 `&Point` 实现 `Add`。这在哪些情况下有用？
  - 回答：`Add:add` 消耗了 `self`。 如果你要重载的类型 `T` 不是 `Copy`，你应该考虑也为 `&T` 重载运算符。 这样可以避免在调用点上不必要的克隆。
- 为什么 `Output` 是一个关联类型？能否将其作为方法的类型参数？
  - 简答：函数类型参数由调用者控制，但关联类型（如 `Output`）由特征的实现者控制。
- 你可以为两个不同类型实现 `Add`，例如 `impl Add<(i32, i32)> for Point` 将会把一个元组添加到一个 `Point`。

</details>

[1]: https://doc.rust-lang.org/std/ops/index.html
