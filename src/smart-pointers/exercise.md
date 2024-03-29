---
minutes: 30
translated_at: '2024-03-26T10:14:15.781Z'
---

# 练习：二叉树

二叉树是一种树型数据结构，其中每个节点都有两个子节点（左和右）。我们将创建一棵树，每个节点存储一个值。对于给定的节点 N，N 的左子树中的所有节点包含较小的值，N 的右子树中的所有节点将包含较大的值。

实现以下类型，以便给定的测试通过。

加分项：实现一个遍历二叉树的迭代器，按顺序返回值。

```rust,editable
{{#include exercise.rs:types}}

// 实现 `new`、`insert`、`len` 以及 `has`。

{{#include exercise.rs:tests}}
```
