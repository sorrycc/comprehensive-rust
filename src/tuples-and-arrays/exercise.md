---
minutes: 15
translated_at: '2024-03-26T09:59:52.571Z'
---

# 练习：嵌套数组

数组可以包含其他数组：

```rust
let array = [[1, 2, 3], [4, 5, 6], [7, 8, 9]];
```

这个变量的类型是什么？

使用类似上面的数组编写一个函数 `transpose`，它将转置一个矩阵（将行转为列）：

<!-- mdbook-xgettext: skip -->

```bob
           ⎛⎡1 2 3⎤⎞      ⎡1 4 7⎤
"transpose"⎜⎢4 5 6⎥⎟  "=="⎢2 5 8⎥
           ⎝⎣7 8 9⎦⎠      ⎣3 6 9⎦
```

硬编码这两个函数以操作 3 × 3 矩阵。

将下面的代码复制到 <https://play.rust-lang.org/> 并实现函数：

```rust,should_panic
// TODO: 在你完成实现后移除这个标记。
#![allow(unused_variables, dead_code)]

{{#include exercise.rs:transpose}}
    unimplemented!()
}

{{#include exercise.rs:tests}}

{{#include exercise.rs:main}}
```
