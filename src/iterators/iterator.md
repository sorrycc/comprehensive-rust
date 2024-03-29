---
minutes: 5
translated_at: '2024-03-26T10:42:02.211Z'
---

# `Iterator`

[`Iterator`][1] 特性支持在集合中遍历值。它要求一个 `next` 方法并提供许多方法。许多标准库类型实现了 `Iterator`，你也可以自己实现：

```rust,editable
struct Fibonacci {
    curr: u32,
    next: u32,
}

impl Iterator for Fibonacci {
    type Item = u32;

    fn next(&mut self) -> Option<Self::Item> {
        let new_next = self.curr + self.next;
        self.curr = self.next;
        self.next = new_next;
        Some(self.curr)
    }
}

fn main() {
    let fib = Fibonacci { curr: 0, next: 1 };
    for (i, n) in fib.enumerate().take(5) {
        println!("fib({i}): {n}");
    }
}
```

<details>

- `Iterator` 特性实现了许多常见的函数式编程操作，如遍历集合（例如 `map`，`filter`，`reduce` 等）。你可以在这个特性中找到所有有关它们的文档。在 Rust 中，这些函数应该产生与等效的命令式实现一样高效的代码。

- `IntoIterator` 是一个使 for 循环工作的特性。它由诸如 `Vec<T>` 以及对它们的引用（如 `&Vec<T>` 和 `&[T]`）的集合类型实现。范围（Ranges）也实现了它。这就是为什么你可以使用 `for i in some_vec { .. }` 遍历一个向量，但 `some_vec.next()` 却不存在。

</details>

[1]: https://doc.rust-lang.org/std/iter/trait.Iterator.html
