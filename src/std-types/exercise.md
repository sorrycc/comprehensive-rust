---
minutes: 20
translated_at: '2024-03-26T10:06:26.092Z'
---

# 练习：计数器

在这个练习中，你将取一个非常简单的数据结构，并使其泛型化。
它使用了 [`std::collections::HashMap`](https://doc.rust-lang.org/stable/std/collections/struct.HashMap.html) 来跟踪哪些值被看到以及每一个值出现的次数。

`Counter` 的初始版本被硬编码为只适用于 `u32` 值。
使结构体及其方法对正在跟踪的值的类型进行泛型化，这样 `Counter` 就可以跟踪任何类型的值了。

如果你提前完成了，尝试使用 [`entry`](https://doc.rust-lang.org/stable/std/collections/struct.HashMap.html#method.entry) 方法将实现 `count` 方法所需的哈希查找次数减半。

```rust,compile_fail,editable
use std::collections::HashMap;

/// Counter 统计每种类型 T 的值被看到的次数。
struct Counter<T> {
    values: HashMap<T, u64>,
}

impl<T: Eq + std::hash::Hash> Counter<T> {
    /// 创建一个新的 Counter。
    fn new() -> Self {
        Counter {
            values: HashMap::new(),
        }
    }

    /// 计数给定值的一个出现。
    fn count(&mut self, value: T) {
        if self.values.contains_key(&value) {
            *self.values.get_mut(&value).unwrap() += 1;
        } else {
            self.values.insert(value, 1);
        }
    }

    /// 返回给定值被看到的次数。
    fn times_seen(&self, value: T) -> u64 {
        self.values.get(&value).copied().unwrap_or_default()
    }
}

{{#include exercise.rs:main}}
```
