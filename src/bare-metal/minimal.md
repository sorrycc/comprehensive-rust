---
translated_at: '2024-03-26T11:31:54.629Z'
---

# 一个最简单的 `no_std` 程序

<!-- mdbook-xgettext: skip -->

```rust,editable,compile_fail
#![no_main]
#![no_std]

use core::panic::PanicInfo;

#[panic_handler]
fn panic(_panic: &PanicInfo) -> ! {
    loop {}
}
```

<details>

- 这将编译成一个空的二进制文件。
- `std` 提供一个 panic 处理函数；没有它我们必须自己提供。
- 它也可以被其它 crate 提供，比如 `panic-halt`。
- 根据目标平台，你可能需要使用 `panic = "abort"` 来编译，以避免关于 `eh_personality` 的错误。
- 注意这里没有 `main` 函数或者任何其它入口点；你需要自己定义入口点。这通常涉及到链接脚本和一些汇编代码来设置好一切，为 Rust 代码的运行做好准备。

</details>
