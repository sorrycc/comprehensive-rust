---
minutes: 10
translated_at: '2024-03-26T10:47:58.253Z'
---

# 练习：泛型 `min`

在这个简短的练习中，你将实现一个泛型 `min` 函数，该函数使用 [`Ord`] 特征来确定两个值中的最小值。

```rust,compile_fail
use std::cmp::Ordering;

// 代办：实现用在 `main` 中的 `min` 函数。

{{#include exercise.rs:main}}
```

<details>

- 向学生们展示 [`Ord`] 特征和 [`Ordering`] 枚举类型。

</details>

[`Ord`]: https://doc.rust-lang.org/stable/std/cmp/trait.Ord.html
[`Ordering`]: https://doc.rust-lang.org/stable/std/cmp/enum.Ordering.html
