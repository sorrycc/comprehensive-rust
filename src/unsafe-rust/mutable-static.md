---
minutes: 5
translated_at: '2024-03-26T09:53:53.476Z'
---

# 可变静态变量

读取不可变静态变量是安全的：

```rust,editable
static HELLO_WORLD: &str = "Hello, world!";

fn main() {
    println!("HELLO_WORLD: {HELLO_WORLD}");
}
```

然而，由于数据竞争的可能，读写可变静态变量是不安全的：

```rust,editable
static mut COUNTER: u32 = 0;

fn add_to_counter(inc: u32) {
    unsafe {
        COUNTER += inc;
    }
}

fn main() {
    add_to_counter(42);

    unsafe {
        println!("COUNTER: {COUNTER}");
    }
}
```

<details>

- 这个程序是安全的，因为它是单线程的。然而，Rust 编译器是保守的，并会假设最坏情况。尝试移除 `unsafe` 并看看编译器如何解释从多个线程变更一个静态变量是未定义行为。

- 使用可变静态通常是一个坏主意，但在一些情况下，在底层 `no_std` 代码中使用它可能是有意义的，如实现堆分配器或与某些 C API 交互。

</details>
