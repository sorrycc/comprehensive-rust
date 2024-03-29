---
translated_at: '2024-03-26T11:32:12.730Z'
---

# 微控制器

`cortex_m_rt` crate 提供了（除其他外）一个用于 Cortex M 微控制器的重置处理程序。

<!-- mdbook-xgettext: skip -->

```rust,editable,compile_fail
{{#include microcontrollers/examples/src/bin/minimal.rs:Example}}
```

接下来，我们将看看如何访问外设，并逐步提高抽象级别。

<details>

- `cortex_m_rt::entry` 宏要求该函数具有类型 `fn() -> !`，因为返回到重置处理程序是没有意义的。
- 使用 `cargo embed --bin minimal` 运行示例

</details>
