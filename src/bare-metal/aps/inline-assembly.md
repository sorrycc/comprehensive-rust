---
translated_at: '2024-03-26T11:40:47.045Z'
---

# 内联汇编

有时我们需要使用汇编来完成 Rust 代码无法实现的事情。例如，进行 HVC（超级管理调用）以通知固件关闭系统：

```rust,editable,compile_fail
{{#include examples/src/main_psci.rs:main}}
```

（如果你真的想这么做，可以使用 [`smccc`][1] 库，它为所有这些功能提供了封装。）

<details>

- PSCI 是 Arm 电源状态协调接口，一套管理系统和 CPU 电源状态等事项的标准功能集。它由许多系统上的 EL3 固件和虚拟机实现。
- `0 => _` 语法表示在运行内联汇编代码之前将寄存器初始化为 0，并在之后忽略其内容。我们需要使用 `inout` 而不是 `in`，因为调用可能会破坏寄存器的内容。
- 这个 `main` 函数需要是 `#[no_mangle]` 和 `extern "C"`，因为它是从我们在 `entry.S` 中的入口点调用的。
- `_x0`–`_x3` 是寄存器 `x0`–`x3` 的值，按照惯例，这些值由引导程序用来传递诸如设备树指针之类的内容。根据标准 aarch64 调用约定（这是 `extern "C"` 指定使用的），寄存器 `x0`–`x7` 用于传递给函数的前 8 个参数，因此 `entry.S` 除了确保它不改变这些寄存器之外，不需要做任何特别的事情。
- 在 `src/bare-metal/aps/examples` 下使用 `make qemu_psci` 运行示例。

</details>

[1]: https://crates.io/crates/smccc
