---
minutes: 5
translated_at: '2024-03-26T10:39:20.378Z'
---

# 函数调用中的生命周期

函数参数和返回值的生命周期必须被完全指定，但 Rust 允许在大多数情况下省略生命周期，通过[一些简单的规则](https://doc.rust-lang.org/nomicon/lifetime-elision.html)。这不是推断——它只是一种语法简写。

- 没有生命周期注解的每个参数都会被赋予一个生命周期。
- 如果只有一个参数生命周期，它将被赋予所有未注解的返回值。
- 如果有多个参数生命周期，但第一个参数是 `self`，那个生命周期将被赋予所有未注解的返回值。

```rust,editable
#[derive(Debug)]
struct Point(i32, i32);

fn cab_distance(p1: &Point, p2: &Point) -> i32 {
    (p1.0 - p2.0).abs() + (p1.1 - p2.1).abs()
}

fn nearest<'a>(points: &'a [Point], query: &Point) -> Option<&'a Point> {
    let mut nearest = None;
    for p in points {
        if let Some((_, nearest_dist)) = nearest {
            let dist = cab_distance(p, query);
            if dist < nearest_dist {
                nearest = Some((p, dist));
            }
        } else {
            nearest = Some((p, cab_distance(p, query)));
        };
    }
    nearest.map(|(p, _)| p)
}

fn main() {
    println!(
        "{:?}",
        nearest(
            &[Point(1, 0), Point(1, 0), Point(-1, 0), Point(0, -1),],
            &Point(0, 2)
        )
    );
}
```

<details>

在这个示例中，`cab_distance` 的生命周期被轻松省略了。

`nearest` 函数提供了另一个需要显式注解的函数示例，该函数在其参数中包含多个引用。

尝试调整签名以“说谎”关于返回的生命周期：

```rust,ignore
fn nearest<'a, 'q>(points: &'a [Point], query: &'q Point) -> Option<&'q Point> {
```

这将无法编译，演示了注解会被编译器检查有效性。注意，对于原始指针（不安全）来说，情况并非如此，这是不安全 Rust 中的一个常见错误来源。

学生们可能会问何时使用生命周期。Rust 借用**始终**具有生命周期。

大多数情况下，省略和类型推导意味着这些无需明确写出。在更复杂的情形下，生命周期注释可以帮助解决歧义。通常，尤其是在原型阶段，使用克隆值来操作所拥有的数据会更简单。
