---
minutes: 15
translated_at: '2024-03-26T09:57:49.402Z'
---

# 练习：斐波那契数

斐波那契数列的第一和第二个数字都是 `1`。对于 n>2，第 n 个斐波那契数是通过递归计算得到的，即第 n-1 个和第 n-2 个斐波那契数之和。

编写一个函数 `fib(n)` 来计算第 n 个斐波那契数。这个函数什么时候会 panic ？

```rust,editable,should_panic
{{#include exercise.rs:fib}}
    if n <= 2 {
        // 基本情况。
        todo!("实现这个")
    } else {
        // 递归情况。
        todo!("实现这个")
    }
}

{{#include exercise.rs:main}}
```
