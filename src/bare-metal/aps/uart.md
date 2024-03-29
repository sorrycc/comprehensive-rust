---
translated_at: '2024-03-26T11:39:05.571Z'
---

# 来编写一个 UART 驱动程序

QEMU 'virt' 机器有一个 [PL011][1] UART，那么我们来为它编写一个驱动程序。

```rust,editable
{{#include examples/src/pl011_minimal.rs:Example}}
```

<details>

- 请注意，`Uart::new` 是不安全的，而其他方法是安全的。这是因为，只要调用 `Uart::new` 的代码保证其安全要求得到满足（即，对于给定的 UART，只有一个驱动实例，并且没有其他东西别名它的地址空间），那么以后调用 `write_byte` 总是安全的，因为我们可以假定所需的前提条件已经满足。
- 我们也可以做相反的处理（使 `new` 安全但 `write_byte` 不安全），但这样使用起来要不便多了，因为每一个调用 `write_byte` 的地方都需要推理安全性。
- 这是写安全包装非安全代码的常见模式：将正确性证明的负担从大量地方移动到较少的地方。

</details>

[1]: https://developer.arm.com/documentation/ddi0183/g
