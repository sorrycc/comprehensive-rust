---
translated_at: '2024-03-26T11:38:11.362Z'
---

# `embedded-hal`

[`embedded-hal`](https://crates.io/crates/embedded-hal) 软件包提供了多个特性，涵盖了常见的微控制器外设。

- GPIO
- ADC
- I2C，SPI，UART，CAN
- RNG
- 计时器
- 看门狗

其他软件包随后会根据这些特性实现[驱动程序](https://github.com/rust-embedded/awesome-embedded-rust#driver-crates)，例如一个加速度计驱动可能需要 I2C 或 SPI 总线实现。

<details>

- 有许多微控制器的实现，以及像树莓派上的 Linux 这样的其他平台的实现。
- 一个 `async` 版本的 `embedded-hal` 正在开发中，但还没有稳定。

</details>
