---
minutes: 10
translated_at: '2024-03-26T10:10:29.909Z'
---

# 比较

这些特性支持值之间的比较。所有特性均可为包含实现这些特性的字段的类型派生。

## `PartialEq` 和 `Eq`

`PartialEq` 是一个部分等价关系，要求实现方法 `eq` 并提供方法 `ne`。`==` 和 `!=` 运算符将调用这些方法。

```rust,editable
struct Key {
    id: u32,
    metadata: Option<String>,
}
impl PartialEq for Key {
    fn eq(&self, other: &Self) -> bool {
        self.id == other.id
    }
}
```

`Eq` 是一个完全等价关系（自反、对称和传递）并且蕴含 `PartialEq`。需要完全等价的函数会使用 `Eq` 作为特性界限。

## `PartialOrd` 和 `Ord`

`PartialOrd` 定义了一个部分排序，带有 `partial_cmp` 方法。它用于实现 `<`、`<=`、`>=` 和 `>` 运算符。

```rust,editable
use std::cmp::Ordering;
#[derive(Eq, PartialEq)]
struct Citation {
    author: String,
    year: u32,
}
impl PartialOrd for Citation {
    fn partial_cmp(&self, other: &Self) -> Option<Ordering> {
        match self.author.partial_cmp(&other.author) {
            Some(Ordering::Equal) => self.year.partial_cmp(&other.year),
            author_ord => author_ord,
        }
    }
}
```

`Ord` 是一个全排序，`cmp` 方法返回 `Ordering`。

<details>

`PartialEq` 可以在不同类型之间实现，但 `Eq` 不可以，因为它是自反的：

```rust,editable
struct Key {
    id: u32,
    metadata: Option<String>,
}
impl PartialEq<u32> for Key {
    fn eq(&self, other: &u32) -> bool {
        self.id == *other
    }
}
```

在实践中，通常会派生这些特性，但不常自行实现它们。

</details>
