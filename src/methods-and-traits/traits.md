---
minutes: 15
translated_at: '2024-03-26T10:28:55.714Z'
---

# 特性

Rust 允许你使用特性（traits）来抽象不同的类型。它们类似于接口：

```rust,editable
trait Pet {
    /// 返回这个宠物的一句话。
    fn talk(&self) -> String;

    /// 向终端打印一句问候这个宠物的话。
    fn greet(&self);
}
```

<details>

- 特性定义了类型必须具备的一些方法，才能实现该特性。

- 在接下来的 “泛型” 环节中，我们将看到如何构建对所有实现了特性的类型通用的功能。

</details>
