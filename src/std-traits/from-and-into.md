---
minutes: 10
translated_at: '2024-03-26T10:09:14.264Z'
---

# `From` 和 `Into`

类型实现 [`From`][1] 和 [`Into`][2] 来促进类型转换：

```rust,editable
fn main() {
    let s = String::from("hello");
    let addr = std::net::Ipv4Addr::from([127, 0, 0, 1]);
    let one = i16::from(true);
    let bigger = i32::from(123_i16);
    println!("{s}, {addr}, {one}, {bigger}");
}
```

当实现了 [`From`][1] 时，[`Into`][2] 会自动被实现：

```rust,editable
fn main() {
    let s: String = "hello".into();
    let addr: std::net::Ipv4Addr = [127, 0, 0, 1].into();
    let one: i16 = true.into();
    let bigger: i32 = 123_i16.into();
    println!("{s}, {addr}, {one}, {bigger}");
}
```

<details>

- 这就是为什么通常只需要实现 `From`，因为你的类型也会自动实现 `Into`。
- 当声明一个函数参数输入类型，如“可以转换成 `String` 的任何类型”时，规则是相反的，你应该使用 `Into`。你的函数将会接受实现了 `From` 的类型，以及那些_只_实现了 `Into` 的类型。

</details>

[1]: https://doc.rust-lang.org/std/convert/trait.From.html
[2]: https://doc.rust-lang.org/std/convert/trait.Into.html
