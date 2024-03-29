---
minutes: 10
translated_at: '2024-03-26T11:28:47.192Z'
---

# 借用一个值

如我们之前所见，当调用一个函数时，你可以让函数_借用_值，而不是转移所有权：

```rust,editable
#[derive(Debug)]
struct Point(i32, i32);

fn add(p1: &Point, p2: &Point) -> Point {
    Point(p1.0 + p2.0, p1.1 + p2.1)
}

fn main() {
    let p1 = Point(3, 4);
    let p2 = Point(10, 20);
    let p3 = add(&p1, &p2);
    println!("{p1:?} + {p2:?} = {p3:?}");
}
```

- `add` 函数_借用_了两个点并返回了一个新点。
- 调用者保持了输入的所有权。

<details>

这个幻灯片回顾了第一天关于引用的材料，并稍微扩展了包括函数参数和返回值。

# 更多探索

关于堆栈返回的注解：

- 示范 `add` 返回是低廉的，因为编译器可以消除复制操作。改变上面的代码以打印堆栈地址，并在 [Playground] 上运行它，或者在 [Godbolt](https://rust.godbolt.org/) 中查看汇编。在 "DEBUG" 优化级别下，地址应该会改变，而当改变到 "RELEASE" 设定时，它们保持不变：

  ```rust,editable
  #[derive(Debug)]
  struct Point(i32, i32);

  fn add(p1: &Point, p2: &Point) -> Point {
      let p = Point(p1.0 + p2.0, p1.1 + p2.1);
      println!("&p.0: {:p}", &p.0);
      p
  }

  pub fn main() {
      let p1 = Point(3, 4);
      let p2 = Point(10, 20);
      let p3 = add(&p1, &p2);
      println!("&p3.0: {:p}", &p3.0);
      println!("{p1:?} + {p2:?} = {p3:?}");
  }
  ```
- Rust 编译器可以做返回值优化（RVO）。
- 在 C++ 中，副本省略必须在语言规范中定义，因为构造函数可以有副作用。在 Rust 中，这根本不是问题。如果没有发生 RVO，Rust 总是会执行一个简单而高效的 `memcpy` 复制。

</details>

[Playground]: https://play.rust-lang.org/?version=stable&mode=release&edition=2021&gist=0cb13be1c05d7e3446686ad9947c4671
