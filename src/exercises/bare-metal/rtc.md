---
translated_at: '2024-03-26T10:56:16.399Z'
---

# RTC 驱动

QEMU aarch64 虚拟机有一个位于 0x9010000 的 [PL031][1] 实时时钟。为了这个练习，你应该为它编写一个驱动。

1. 使用它将当前时间打印到串行控制台。你可以使用 [`chrono`][2] 包进行日期 / 时间格式化。
2. 使用匹配寄存器和原始中断状态进行忙等待，直到给定的时间，例如未来的 3 秒。（在循环内调用 [`core::hint::spin_loop`][3]。）
3. _如果你有时间的话，可以扩展：_ 启用并处理由 RTC 匹配生成的中断。你可以使用 [`arm-gic`][4] 包提供的驱动来配置 Arm 通用中断控制器。
   - 使用 RTC 中断，它被连接到 GIC 作为 `IntId::spi(2)`。
   - 一旦中断被启用，你可以通过 `arm_gic::wfi()` 使核心进入睡眠状态，这将导致核心睡眠直到它接收到一个中断。

下载 [练习模板](../../comprehensive-rust-exercises.zip)，并在 `rtc` 目录中查看以下文件。

_src/main.rs_:

<!-- 文件 src/main.rs -->
<!-- mdbook-xgettext: skip -->

```rust,compile_fail
{{#include rtc/src/main.rs:top}}

{{#include rtc/src/main.rs:imports}}

{{#include rtc/src/main.rs:main}}

    // 待办事项：创建 RTC 驱动实例并打印当前时间。

    // 待办事项：等待 3 秒。

{{#include rtc/src/main.rs:main_end}}
```

_src/exceptions.rs_（你可能只需要为练习的第三部分更改此文件）:

<!-- 文件 src/exceptions.rs -->
<!-- mdbook-xgettext: skip -->

```rust,compile_fail
{{#include rtc/src/exceptions.rs}}
```

_src/logger.rs_（你不需要更改这个文件）:

<!-- 文件 src/logger.rs -->
<!-- mdbook-xgettext: skip -->

```rust,compile_fail
{{#include rtc/src/logger.rs}}
```

_src/pl011.rs_（你不需要更改这个文件）:

<!-- 文件 src/pl011.rs -->
<!-- mdbook-xgettext: skip -->

```rust,compile_fail
{{#include rtc/src/pl011.rs}}
```

_Cargo.toml_（你不需要更改这个文件）:

<!-- 文件 Cargo.toml -->

<!-- mdbook-xgettext: skip -->

```toml
{{#include rtc/Cargo.toml}}
```

_build.rs_（你不需要改变这个）：

<!-- 文件 build.rs -->
<!-- mdbook-xgettext: skip -->

```rust,compile_fail
{{#include rtc/build.rs}}
```

_entry.S_（你不需要改变这个）：

<!-- 文件 entry.S -->
<!-- mdbook-xgettext: skip -->

```armasm
{{#include rtc/entry.S}}
```

_exceptions.S_（你不需要改变这个）：

<!-- 文件 exceptions.S -->
<!-- mdbook-xgettext: skip -->

```armasm
{{#include rtc/exceptions.S}}
```

_idmap.S_（你不需要改变这个）：

<!-- 文件 idmap.S -->
<!-- mdbook-xgettext: skip -->

```armasm
{{#include rtc/idmap.S}}
```

_image.ld_（你不需要改变这个）：

<!-- 文件 image.ld -->
<!-- mdbook-xgettext: skip -->

```ld
{{#include rtc/image.ld}}
```

_Makefile_（你不需要改变这个）：

<!-- 文件 Makefile -->
<!-- mdbook-xgettext: skip -->

```makefile
{{#include rtc/Makefile}}
```

_.cargo/config.toml_（你不需要改变这个）：

<!-- 文件 .cargo/config.toml -->
<!-- mdbook-xgettext: skip -->

```toml
{{#include rtc/.cargo/config.toml}}
```

使用 `make qemu` 在 QEMU 中运行代码。

[1]: https://developer.arm.com/documentation/ddi0224/c
[2]: https://crates.io/crates/chrono
[3]: https://doc.rust-lang.org/core/hint/fn.spin_loop.html
[4]: https://docs.rs/arm-gic/
