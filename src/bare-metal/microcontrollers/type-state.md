---
translated_at: '2024-03-26T11:36:00.699Z'
---

# 类型状态模式

```rust,editable,compile_fail
{{#include examples/src/bin/typestate.rs:Example}}
```

<details>

- 引脚不实现 `Copy` 或 `Clone`，因此每个只能存在一个实例。一旦引脚从端口结构体中移出，就没有其他人能够获取它。
- 改变引脚的配置会消耗旧的引脚实例，因此你无法继续使用之前的实例。
- 一个值的类型指示了它所处的状态：例如在本例中，GPIO 引脚的配置状态。这将状态机编码进类型系统，确保你不会在没有适当配置的情况下错误地使用引脚。非法的状态转换在编译时就会被捕获。
- 你可以在输入引脚上调用 `is_high`，在输出引脚上调用 `set_high`，但反之则不行。
- 许多 HAL crates 都遵循这种模式。

</details>
