---
translated_at: '2024-03-26T11:59:35.012Z'
---

# 手写 FFI

我们可以手动声明外部函数：

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

我们在 [安全 FFI 包装器练习](../../exercises/day-3/safe-ffi-wrapper.md) 中已经看到了这个。

> 这假定了对目标平台的全面了解。不推荐用于生产环境。
