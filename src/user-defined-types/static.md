---
minutes: 5
translated_at: '2024-03-26T09:47:19.998Z'
---

# `static`

静态变量会在程序的整个执行期间存活，因此不会被移动：

```rust,editable
static BANNER: &str = "Welcome to RustOS 3.14";

fn main() {
    println!("{BANNER}");
}
```

如 [Rust RFC 书][1]所述，这些变量在使用时不会被内联，并且具有实际的内存地址。这对于不安全和嵌入式代码很有用，变量会在程序执行的整个过程中存活。当全局作用域的值没有需要对象身份的理由时，通常更倾向于使用 `const`。

<details>

- `static` 类似于 C++ 中的可变全局变量。
- `static` 提供对象身份：内存中的地址以及类型所需的状态，例如具有内部可变性的 `Mutex<T>`。

# 更多探索

因为 `static` 变量可以从任何线程访问，它们必须是 `Sync`。可以通过 [`Mutex`](https://doc.rust-lang.org/std/sync/struct.Mutex.html)、原子操作或类似方式实现内部可变性。

可使用宏 `std::thread_local` 创建线程本地数据。

</details>

[1]: https://rust-lang.github.io/rfcs/0246-const-vs-static.html
