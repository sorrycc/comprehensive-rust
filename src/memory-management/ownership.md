---
minutes: 5
translated_at: '2024-03-26T10:33:57.607Z'
---

# 所有权

所有变量绑定都有一个它们有效的 _作用域_，在作用域之外使用变量是错误的：

<!-- mdbook-xgettext: skip -->

```rust,editable,compile_fail
struct Point(i32, i32);

fn main() {
    {
        let p = Point(3, 4);
        println!("x: {}", p.0);
    }
    println!("y: {}", p.1);
}
```

我们说变量 _拥有_ 该值。每个 Rust 值在任何时候都恰好有一个所有者。

在作用域结束时，变量被 _丢弃_（drop），数据也随之被释放。这里可以运行一个析构函数（destructor）来释放资源。

<details>

熟悉垃圾回收（garbage-collection）实现的学生会知道，垃圾收集器从一组“根”（roots）开始来查找所有可达的内存。
Rust 的“单一所有者”原则是一个类似的概念。

</details>
