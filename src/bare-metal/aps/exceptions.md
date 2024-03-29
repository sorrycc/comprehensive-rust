---
translated_at: '2024-03-26T11:41:18.496Z'
---

# 异常

AArch64 定义了一个具有 16 个条目的异常向量表，用于 4 种类型的异常（同步、IRQ、FIQ、SError）来自 4 种状态（当前 EL 与 SP0、当前 EL 与 SPx、使用 AArch64 的较低 EL、使用 AArch32 的较低 EL）。我们在汇编中实现它，以便在调用 Rust 代码之前将易失性寄存器保存到堆栈中：

<!-- mdbook-xgettext: skip -->

```rust,editable,compile_fail
{{#include examples/src/exceptions.rs:exceptions}}
```

<details>

- EL 是异常级别；我们所有的示例今天下午都在 EL1 中运行。
- 为了简单起见，我们不区分当前 EL 的异常的 SP0 和 SPx，或较低 EL 的异常的 AArch32 和 AArch64。
- 对于这个例子，我们只是记录异常并关闭电源，因为我们不希望它们实际发生。
- 我们可以将异常处理程序和我们的主执行上下文或多或少地视为不同的线程。[`Send` 和 `Sync`][1] 将控制我们可以在它们之间共享什么，就像线程一样。例如，如果我们想在异常处理程序和程序的其他部分之间共享一些值，并且它是 `Send` 但不是 `Sync`，那么我们将需要将它包装在像 `Mutex` 这样的东西中并将其放在静态中。

</details>

[1]: ../../concurrency/send-sync.md
