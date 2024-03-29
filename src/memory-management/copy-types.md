---
minutes: 5
translated_at: '2024-03-26T10:36:38.385Z'
---

# 拷贝类型

虽然移动语义是默认选项，但某些类型默认是拷贝的：

<!-- mdbook-xgettext: skip -->

```rust,editable
fn main() {
    let x = 42;
    let y = x;
    println!("x: {x}"); // 如果不是 Copy，那么这里将无法访问
    println!("y: {y}");
}
```

这些类型实现了 `Copy` 特征。

你可以选择让你自己的类型使用拷贝语义：

<!-- mdbook-xgettext: skip -->

```rust,editable
#[derive(Copy, Clone, Debug)]
struct Point(i32, i32);

fn main() {
    let p1 = Point(3, 4);
    let p2 = p1;
    println!("p1: {p1:?}");
    println!("p2: {p2:?}");
}
```

- 赋值后，`p1` 和 `p2` 都拥有它们自己的数据。
- 我们也可以使用 `p1.clone()` 来显式拷贝数据。

<details>

拷贝和克隆并不相同：

- 拷贝指的是内存区域的位拷贝，并不适用于任意对象。
- 拷贝不允许自定义逻辑（与 C++ 中的拷贝构造函数不同）。
- 克隆是一个更通用的操作，通过实现 `Clone` 特征也允许自定义行为。
- 对于实现了 `Drop` 特征的类型，拷贝是不起作用的。

在上面的例子中，尝试以下操作：

- 给 `struct Point` 添加一个 `String` 类型的字段。它将无法编译，因为 `String` 不是 `Copy` 类型。
- 从 `derive` 属性中移除 `Copy`。编译器错误现在出现在 `p1` 的 `println!` 中。
- 展示如果你克隆 `p1` 将是可以工作的。

</details>
