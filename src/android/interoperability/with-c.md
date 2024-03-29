---
translated_at: '2024-03-26T11:58:22.840Z'
---

# 与 C 语言的互操作性

Rust 完全支持链接具有 C 调用约定的对象文件。
同样，你也可以导出 Rust 函数并从 C 中调用它们。

如果你愿意，你可以手动完成：

```rust
extern "C" {
    fn abs(x: i32) -> i32;
}

fn main() {
    let x = -42;
    let abs_x = unsafe { abs(x) };
    println!("{x}, {abs_x}");
}
```

我们已经在
[安全 FFI 包装器练习](../../exercises/day-3/safe-ffi-wrapper.md) 中看到了这个。

> 这假设你完全了解目标平台。不推荐用于生产环境。

我们接下来将查看更好的选择。
