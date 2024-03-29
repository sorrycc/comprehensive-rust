---
translated_at: '2024-03-26T10:32:39.366Z'
---

# 关联类型

关联类型是占位符类型，由 trait 实现提供。

```rust,editable
#[derive(Debug)]
struct Meters(i32);
#[derive(Debug)]
struct MetersSquared(i32);

trait Multiply {
    type Output;
    fn multiply(&self, other: &Self) -> Self::Output;
}

impl Multiply for Meters {
    type Output = MetersSquared;
    fn multiply(&self, other: &Self) -> Self::Output {
        MetersSquared(self.0 * other.0)
    }
}

fn main() {
    println!("{:?}", Meters(10).multiply(&Meters(20)));
}
```

<details>

- 关联类型有时也被称为“输出类型”。关键的观察是，选择这种类型的是实现者，而不是调用者。

- 许多标准库的 traits 都有关联类型，包括算术运算符和 `Iterator`。

</details>
