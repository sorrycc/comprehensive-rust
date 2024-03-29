---
minutes: 10
translated_at: '2024-03-26T09:48:18.791Z'
---

# 命名结构体

像 C 和 C++ 一样，Rust 支持自定义结构体：

```rust,editable
struct Person {
    name: String,
    age: u8,
}

fn describe(person: &Person) {
    println!("{} 是 {} 岁", person.name, person.age);
}

fn main() {
    let mut peter = Person { name: String::from("Peter"), age: 27 };
    describe(&peter);

    peter.age = 28;
    describe(&peter);

    let name = String::from("Avery");
    let age = 39;
    let avery = Person { name, age };
    describe(&avery);

    let jackie = Person { name: String::from("Jackie"), ..avery };
    describe(&jackie);
}
```

<details>

要点：

- 结构体的工作方式类似于 C 或 C++。
  - 像在 C++ 中，不同于 C，定义类型时不需要 typedef。
  - 不同于 C++，结构体之间没有继承关系。
- 现在可能是一个好时机，让人们知道有不同类型的结构体。
  - 零大小结构体（例如 `struct Foo;`）可能会在实现某类型的 trait 但不想在值本身存储任何数据时使用。
  - 下一张幻灯片将介绍元组结构体，用于字段名不重要的场合。
- 如果你已经有了正确名称的变量，那么你可以使用简写来创建结构体。
- 语法 `..avery` 允许我们从旧结构体复制大部分字段，无需显式地全部键入。它必须始终是最后一个元素。

</details>
