---
translated_at: '2024-03-26T11:36:32.223Z'
---

# `probe-rs` 和 `cargo-embed`

[probe-rs](https://probe.rs/) 是一套便捷的用于嵌入式调试的工具集，类似于 OpenOCD 但集成得更好。

- 通过 CMSIS-DAP、ST-Link 和 J-Link 探针实现 SWD（串行线调试）和 JTAG
- GDB 存根和微软 DAP（调试适配器协议）服务器
- Cargo 集成

`cargo-embed` 是一个用于构建和刷写二进制文件、记录 RTT（实时传输）输出和连接 GDB 的 cargo 子命令。它通过你的项目目录中的 `Embed.toml` 文件配置。

<details>

- [CMSIS-DAP](https://arm-software.github.io/CMSIS_5/DAP/html/index.html) 是 Arm 标准协议，通过 USB 让在电路中的调试器访问各种 Arm Cortex 处理器的 CoreSight 调试访问端口。它就是 BBC micro:bit 上的板载调试器所使用的协议。
- ST-Link 是意法半导体（ST Microelectronics）的一系列在电路调试器，J-Link 是 SEGGER 的一系列。
- 调试访问端口通常是一个 5 引脚的 JTAG 接口或 2 引脚的串行线调试。
- probe-rs 是一个你可以集成到你自己的工具中的库。
- [微软调试适配器协议](https://microsoft.github.io/debug-adapter-protocol/) 允许 VSCode 和其他 IDE 在任何支持的微控制器上调试代码。
- cargo-embed 是使用 probe-rs 库构建的二进制文件。
- RTT（实时传输）是一种在调试主机和目标设备之间通过一系列环形缓冲区传输数据的机制。

</details>
