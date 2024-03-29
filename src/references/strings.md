---
minutes: 10
translated_at: '2024-03-26T10:18:48.042Z'
---

<!-- NOTES:
包括 `&str` 作为表示有效 utf-8 切片的一种方式
-->

# 字符串

我们现在可以理解 Rust 中的两种字符串类型：

- `&str` 是 UTF-8 编码字节的切片，类似于 `&[u8]`。
- `String` 是一个拥有的、堆分配的 UTF-8 字节缓冲区。

```rust,editable
fn main() {
    let s1: &str = "World";
    println!("s1: {s1}");

    let mut s2: String = String::from("Hello ");
    println!("s2: {s2}");
    s2.push_str(s1);
    println!("s2: {s2}");

    let s3: &str = &s2[6..];
    println!("s3: {s3}");
}
```

<details>

- `&str` 引入了字符串切片，这是对存储在内存块中的 UTF-8 编码字符串数据的不可变引用。字符串字面量（`"Hello"`）被存储在程序的二进制中。

- Rust 的 `String` 类型是字节向量的一个包装。与 `Vec<T>` 一样，它是拥有的。

- 像很多其他类型一样，`String::from()` 从字符串字面量创建字符串；`String::new()` 创建一个新的空字符串，可以使用 `push()` 和 `push_str()` 方法添加字符串数据。

- `format!()` 宏是从动态值生成拥有的字符串的一种便捷方式。它接受与 `println!()` 相同的格式规范。

- 你可以通过 `&` 和可选的范围选择从 `String` 借用 `&str` 切片。如果你选择的字节范围不与字符边界对齐，表达式将会恐慌。`chars` 迭代器迭代字符，并且比尝试获得正确的字符边界更受推荐。

- 对于 C++ 程序员来说：把 `&str` 想象成 C++ 中的 `std::string_view`，但它总是指向内存中的一个有效字符串。Rust `String` 与 C++ 中的 `std::string` 大致相当（主要区别：它只能包含 UTF-8 编码的字节，永远不会使用小字符串优化）。

- 字节字符串字面量允许你直接创建一个 `&[u8]` 值：

  <!-- mdbook-xgettext: skip -->
  ```rust,editable
  fn main() {
      println!("{:?}", b"abc");
      println!("{:?}", &[97, 98, 99]);
  }
  ```

- 原生字符串允许你创建一个禁用转义的 `&str` 值：`r"\n" == "\\n"`。你可以通过在双引号两边使用相同数量的 `#` 来嵌入双引号：

  <!-- mdbook-xgettext: skip -->
  ```rust,editable
  fn main() {
      println!(r#"<a href="link.html">link</a>"#);
      println!("<a href=\"link.html\">link</a>");
  }
  ```
