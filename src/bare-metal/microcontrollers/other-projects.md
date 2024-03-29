---
translated_at: '2024-03-26T11:37:24.559Z'
---

# 其他项目

- [RTIC](https://rtic.rs/)
  - “实时中断驱动的并发”
  - 共享资源管理、消息传递、任务调度、定时器队列
- [Embassy](https://embassy.dev/)
  - 带有优先级、定时器、网络、USB 的 `async` 执行器
- [TockOS](https://www.tockos.org/documentation/getting-started)
  - 专注于安全性的 RTOS，具有抢占式调度和内存保护单元支持
- [Hubris](https://hubris.oxide.computer/)
  - 来自 Oxide 计算机公司的微内核 RTOS，具有内存保护、非特权驱动程序、IPC
- [FreeRTOS 的绑定](https://github.com/lobaro/FreeRTOS-rust)
- 一些平台有 `std` 实现，例如
  [esp-idf](https://esp-rs.github.io/book/overview/using-the-standard-library.html)。

<details>

- RTIC 可以被视为 RTOS 或并发框架。
  - 它不包括任何 HALs。
  - 它使用 Cortex-M NVIC（嵌套虚拟中断控制器）进行调度，而不是一个真正的内核。
  - 仅适用于 Cortex-M。
- 谷歌在 Haven 微控制器上使用 TockOS，用于 Titan 安全密钥。
- FreeRTOS 主要是用 C 编写的，但是有 Rust 绑定用于编写应用程序。

</details>
