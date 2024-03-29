---
translated_at: '2024-03-26T11:37:51.334Z'
---

# HAL crates

[HAL crates](https://github.com/rust-embedded/awesome-embedded-rust#hal-implementation-crates)
对于许多微控制器来说提供了各种外围设备的封装。这些
通常实现来自
[`embedded-hal`](https://crates.io/crates/embedded-hal)
的 trait。

```rust,editable,compile_fail
{{#include examples/src/bin/hal.rs:Example}}
```

<details>

- `set_low` 和 `set_high` 是 `embedded_hal` 的 `OutputPin` trait 上的方法。
- 对于许多 Cortex-M 和 RISC-V 设备，包括各种
  STM32、GD32、nRF、NXP、MSP430、AVR 和 PIC 微控制器，都存在 HAL crates。

运行示例使用：

```sh
cargo embed --bin hal
```

</details>
