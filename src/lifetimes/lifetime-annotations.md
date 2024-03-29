---
minutes: 10
translated_at: '2024-03-26T10:40:11.925Z'
---

# 生命周期注解

引用有一个 _生命周期_，它不能 "超过" 引用的值的存在时长。
这一点由借用检查器进行验证。

生命周期可以是隐含的——到目前为止，我们看到的都是这样。生命周期也可以是显式的：`&'a Point`，`&'document str`。生命周期以 `'` 开头，`'a` 是一个典型的默认名称。将 `&'a Point` 理解为 "至少在生命周期 `'a` 期间有效的借用 `Point`"。

生命周期总是由编译器推断出来的：你不能自己指定生命周期。
在存在模糊性时，显式生命周期注解创建约束；编译器验证是否存在一个有效的解决方案。

当考虑将值传递给函数并从函数返回值时，生命周期变得更为复杂。

<!-- rustfmt 在 left_most 中使用多行格式的方式，显然是有意的：https://github.com/rust-lang/rustfmt/issues/1908 -->

```rust,editable,compile_fail
#[derive(Debug)]
struct Point(i32, i32);

fn left_most(p1: &Point, p2: &Point) -> &Point {
    if p1.0 < p2.0 {
        p1
    } else {
        p2
    }
}

fn main() {
    let p1: Point = Point(10, 10);
    let p2: Point = Point(20, 20);
    let p3 = left_most(&p1, &p2); // p3 的生命周期是什么？
    println!("p3: {p3:?}");
}
```

<details>

在这个例子中，编译器不知道该为 `p3` 推断出什么生命周期。
查看函数体内部可以看出，它只能安全地假设 `p3` 的生命周期是 `p1` 和 `p2` 中较短的那个。但就像类型一样，Rust 要求在函数参数和返回值上显式注解生命周期。

适当地向 `left_most` 添加 `'a`：

```rust,ignore
fn left_most<'a>(p1: &'a Point, p2: &'a Point) -> &'a Point {
```

这意味着，“给定 p1 和 p2，它们都超过了 `'a` 的生命周期，返回值至少活跃 `'a` 的时间。

在常见情况下，生命周期可以省略，如下一张幻灯片所述。

</details>
