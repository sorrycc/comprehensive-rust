---
translated_at: '2024-03-26T12:00:37.477Z'
---

# 额外的类型

| Rust 类型         | C++ 类型             |
| ----------------- | -------------------- |
| `String`          | `rust::String`       |
| `&str`            | `rust::Str`          |
| `CxxString`       | `std::string`        |
| `&[T]`/`&mut [T]` | `rust::Slice`        |
| `Box<T>`          | `rust::Box<T>`       |
| `UniquePtr<T>`    | `std::unique_ptr<T>` |
| `Vec<T>`          | `rust::Vec<T>`       |
| `CxxVector<T>`    | `std::vector<T>`     |

<details>

- 这些类型可以用于共享结构的字段、外部函数的参数和返回值中。
- 注意，Rust 的 `String` 并不直接映射到 `std::string`。这是因为几个原因：
  - `std::string` 不维护 `String` 所要求的 UTF-8 不变性。
  - 两种类型在内存中的布局不同，因此不能直接在语言之间传递。
  - `std::string` 需要移动构造函数，这与 Rust 的移动语义不匹配，所以 `std::string` 不能按值传递给 Rust。

</details>
