---
minutes: 10
translated_at: '2024-03-26T09:46:39.955Z'
---

<!-- NOTES:
元组结构体、单元素包装器、类单元结构体，包括初始化语法
-->

# 元组结构体

如果字段名称不重要，你可以使用元组结构体：

```rust,editable
struct Point(i32, i32);

fn main() {
    let p = Point(17, 23);
    println!("({}, {})", p.0, p.1);
}
```

这通常用于单字段包装器（称为 newtypes）：

```rust,editable,compile_fail
struct PoundsOfForce(f64);
struct Newtons(f64);

fn compute_thruster_force() -> PoundsOfForce {
    todo!("在 NASA 询问一个火箭科学家")
}

fn set_thruster_force(force: Newtons) {
    // ...
}

fn main() {
    let force = compute_thruster_force();
    set_thruster_force(force);
}
```

<details>

- Newtypes 是一种将额外信息编码到原始类型的值中的绝佳方式，例如：
  - 数字是以某种单位测量的：上述示例中的 `Newtons`。
  - 值在创建时通过了某种验证，因此你不再需要在每次使用时再次验证它：`PhoneNumber(String)` 或 `OddNumber(u32)`。
- 展示如何通过访问 newtype 中的单个字段，将 `f64` 值添加到 `Newtons` 类型中。
  - Rust 通常不喜欢不明确的事情，比如自动解包或者使用布尔值作为整数。
  - 操作符重载将在第 3 天（泛型）讨论。
- 该示例是对 [火星气候探测器](https://en.wikipedia.org/wiki/Mars_Climate_Orbiter) 失败的微妙引用。

</details>
