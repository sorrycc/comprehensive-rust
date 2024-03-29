---
translated_at: '2024-03-26T11:44:50.735Z'
---

# vmbase

对于在 aarch64 上运行 crosvm 的虚拟机，[vmbase][1] 库提供了一个链接脚本和有用的构建规则默认值，以及一个入口点、UART 控制台日志记录等功能。

<!-- mdbook-xgettext: skip -->

```rust,compile_fail
#![no_main]
#![no_std]

use vmbase::{main, println};

main!(main);

pub fn main(arg0: u64, arg1: u64, arg2: u64, arg3: u64) {
    println!("Hello world");
}
```

<details>

- `main!` 宏标记了你的主函数，以便从 `vmbase` 入口点调用。
- `vmbase` 入口点处理控制台初始化，并在你的主函数返回时发出 PSCI_SYSTEM_OFF 以关闭虚拟机。

</details>

[1]: https://android.googlesource.com/platform/packages/modules/Virtualization/+/refs/heads/master/vmbase/
