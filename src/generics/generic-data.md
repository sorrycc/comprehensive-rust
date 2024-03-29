---
minutes: 10
translated_at: '2024-03-26T10:47:39.730Z'
---

# 泛型数据类型

您可以使用泛型来抽象出具体的字段类型：

```rust,editable
#[derive(Debug)]
struct Point<T> {
    x: T,
    y: T,
}

impl<T> Point<T> {
    fn coords(&self) -> (&T, &T) {
        (&self.x, &self.y)
    }

    // fn set_x(&mut self, x: T)
}

fn main() {
    let integer = Point { x: 5, y: 10 };
    let float = Point { x: 1.0, y: 4.0 };
    println!("{integer:?} 和 {float:?}");
    println!("coords: {:?}", integer.coords());
}
```

<details>

- _问题:_ 为什么在 `impl<T> Point<T> {}` 中 `T` 要指定两次？这不是多余的吗？
  - 这是因为它是泛型类型的泛型实现部分。
    它们是各自独立的泛型。
  - 这意味着这些方法被定义用于任何 `T`。
  - 你可以编写 `impl Point<u32> { .. }`。
    - `Point` 仍然是泛型的，你可以使用 `Point<f64>`，但在此代码块中的方法只会适用于 `Point<u32>`。

- 尝试声明一个新的变量 `let p = Point { x: 5, y: 10.0 };`。通过使用两个类型变量，比如 `T` 和 `U`，更新代码以允许点的元素具有不同的类型。

</details>
