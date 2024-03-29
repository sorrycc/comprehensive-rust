---
minutes: 15
translated_at: '2024-03-26T11:03:05.876Z'
---

# 练习：Collatz 序列

[Collatz 序列](https://en.wikipedia.org/wiki/Collatz_conjecture) 如下定义，对于任意大于零的 n<sub>1</sub>：

- 如果 _n<sub>i</sub>_ 是 1，则序列在 _n<sub>i</sub>_ 处终止。
- 如果 _n<sub>i</sub>_ 是偶数，则 _n<sub>i+1</sub> = n<sub>i</sub> / 2_。
- 如果 _n<sub>i</sub>_ 是奇数，则 _n<sub>i+1</sub> = 3 * n<sub>i</sub> + 1_。

例如，从 _n<sub>1</sub>_ = 3 开始：

- 3 是奇数，所以 _n<sub>2</sub>_ = 3 * 3 + 1 = 10；
- 10 是偶数，所以 _n<sub>3</sub>_ = 10 / 2 = 5；
- 5 是奇数，所以 _n<sub>4</sub>_ = 3 * 5 + 1 = 16；
- 16 是偶数，所以 _n<sub>5</sub>_ = 16 / 2 = 8；
- 8 是偶数，所以 _n<sub>6</sub>_ = 8 / 2 = 4；
- 4 是偶数，所以 _n<sub>7</sub>_ = 4 / 2 = 2；
- 2 是偶数，所以 _n<sub>8</sub>_ = 1；然后
- 序列终止。

编写一个函数来计算给定初始 `n` 的 collatz 序列的长度。

```rust,editable,should_panic
{{#include exercise.rs:collatz_length}}
  todo!("Implement this")
}

{{#include exercise.rs:main}}
  todo!("Implement this")
}
```
