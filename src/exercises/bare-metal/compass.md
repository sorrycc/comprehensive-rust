---
translated_at: '2024-03-26T10:56:57.050Z'
---

# 罗盘

我们将从一个 I2C 罗盘读取方向，并将读数记录到串行端口。如果你有时间，尝试以某种方式在 LED 上显示它，或者以某种方式使用按钮。

提示：

- 检查 [`lsm303agr`](https://docs.rs/lsm303agr/latest/lsm303agr/) 和 [`microbit-v2`](https://docs.rs/microbit-v2/latest/microbit/) 库的文档，以及 [micro:bit 硬件](https://tech.microbit.org/hardware/)。
- LSM303AGR 惯性测量单元连接到内部的 I2C 总线上。
- TWI 是 I2C 的另一个名称，因此 I2C 主外设被称为 TWIM。
- LSM303AGR 驱动需要一个实现了 `embedded_hal::blocking::i2c::WriteRead` trait 的东西。[`microbit::hal::Twim`](https://docs.rs/microbit-v2/latest/microbit/hal/struct.Twim.html) 结构体实现了这个。
- 你有一个 [`microbit::Board`](https://docs.rs/microbit-v2/latest/microbit/struct.Board.html) 结构体，它有各种引脚和外设的字段。
- 你也可以查看 [nRF52833 数据手册](https://infocenter.nordicsemi.com/pdf/nRF52833_PS_v1.5.pdf) 如果你愿意，但这对于这个练习来说不是必需的。

下载 [练习模板](../../comprehensive-rust-exercises.zip) 并查看 `compass` 目录下的以下文件。

_src/main.rs_：

<!-- 文件 src/main.rs -->
<!-- mdbook-xgettext: skip -->

```rust,compile_fail
{{#include compass/src/main.rs:top}}
use microbit::{hal::uarte::{Baudrate, Parity, Uarte}, Board};

{{#include compass/src/main.rs:main}}
    // 待办事项

{{#include compass/src/main.rs:loop}}
        // 待办事项
    }
}
```

_Cargo.toml_（你不需要更改这个）：

<!-- 文件 Cargo.toml -->
<!-- mdbook-xgettext: skip -->

```toml
{{#include compass/Cargo.toml}}
```

_Embed.toml_（你不需要更改这个）：

<!-- 文件 Embed.toml -->
<!-- mdbook-xgettext: skip -->

```toml
{{#include compass/Embed.toml}}
```

_.cargo/config.toml_（你不需要更改这个）：

<!-- mdbook-xgettext: skip -->

```toml
{{#include compass/.cargo/config.toml}}
```

在 Linux 上查看串行输出：

<!-- mdbook-xgettext: skip -->

```sh
picocom --baud 115200 --imap lfcrlf /dev/ttyACM0
```

或者在 Mac OS 上类似以下操作（设备名称可能会略有不同）：

<!-- mdbook-xgettext: skip -->

```sh
picocom --baud 115200 --imap lfcrlf /dev/tty.usbmodem14502
```

使用 Ctrl+A Ctrl+Q 退出 picocom。
