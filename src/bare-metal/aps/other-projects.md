---
translated_at: '2024-03-26T11:39:43.907Z'
---

# 其他项目

- [oreboot](https://github.com/oreboot/oreboot)
  - “没有 C 语言的 coreboot”
  - 支持 x86、aarch64 和 RISC-V。
  - 依赖于 LinuxBoot 而不是自身拥有许多驱动。
- [Rust RaspberryPi OS 教程](https://github.com/rust-embedded/rust-raspberrypi-OS-tutorials)
  - 初始化、UART 驱动、简单的引导程序、JTAG、异常级别、
    异常处理、页表
  - Rust 中关于缓存维护和初始化的一些疑问，不一定是生产代码的好榜样。
- [`cargo-call-stack`](https://crates.io/crates/cargo-call-stack)
  - 静态分析以确定最大栈使用量。

<details>

- RaspberryPi OS 教程在 MMU 和缓存启用前就运行 Rust 代码。这将会读写内存（例如堆栈）。然而：
  - 没有 MMU 和缓存，未对齐的访问将会出错。它使用 `aarch64-unknown-none` 编译，这会设置 `+strict-align` 来防止编译器生成未对齐的访问，所以应该没问题，但通常情况下这并不一定适用。
  - 如果在虚拟机中运行，这可能导致缓存一致性问题。问题在于虚拟机在缓存禁用的情况下直接访问内存，而宿主机对同一内存有可缓存的别名。即使宿主机没有显式地访问内存，推测性访问也可以导致缓存填充，然后一方或另一方的更改会丢失。再次强调，在这个特定的情况下（直接在硬件上运行，没有虚拟机管理程序），这是没问题的，但通常这不是一个好模式。

</details>
