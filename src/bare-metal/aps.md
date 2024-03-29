---
session: Afternoon
translated_at: '2024-03-26T11:32:37.165Z'
---

# 应用处理器

到目前为止，我们谈论了微控制器，例如 Arm Cortex-M 系列。现在
让我们尝试为 Cortext-A 编写一些东西。为了简便起见，我们将仅使用
QEMU 的 aarch64
['virt'](https://qemu-project.gitlab.io/qemu/system/arm/virt.html) 板。

<details>

- 通俗地说，微控制器没有 MMU 或多级特权（在 Arm CPU 上是异常级别，在 x86 上是环），而应用处理器则具备。
- QEMU 支持模拟每种体系结构的各种不同机器或板模型。'virt' 板并不对应任何特定的真实硬件，而是专门为虚拟机设计的。

</details>
