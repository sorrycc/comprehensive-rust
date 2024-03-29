---
minutes: 10
translated_at: '2024-03-26T10:21:06.036Z'
---

# 独占引用

独占引用，也称为可变引用，允许改变它们引用的值。它们的类型为 `&mut T`。

<!-- mdbook-xgettext: skip -->

```rust,editable
fn main() {
    let mut point = (1, 2);
    let x_coord = &mut point.0;
    *x_coord = 20;
    println!("point: {point:?}");
}
```

<details>

关键点：

- “独占”意味着只有这个引用可以用来访问值。没有其他引用（共享或独占）可以同时存在，且在独占引用存在期间，被引用的值不能被访问。尝试创建一个 `&point.0` 或在 `x_coord` 存活时改变 `point.0`。

- 一定要注意 `let mut x_coord: &i32` 与 `let x_coord: &mut i32` 之间的区别。前者表示一个可以绑定到不同值的共享引用，而后者表示对可变值的独占引用。

</details>
