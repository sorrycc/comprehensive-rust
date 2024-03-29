---
translated_at: '2024-03-26T11:38:28.581Z'
---

# 调试

_Embed.toml_：

<!-- mdbook-xgettext: skip -->

```toml
[default.general]
chip = "nrf52833_xxAA"

[debug.gdb]
enabled = true
```

在 `src/bare-metal/microcontrollers/examples/` 目录下的一个终端中：

<!-- mdbook-xgettext: skip -->

```sh
cargo embed --bin board_support debug
```

在同一目录下的另一个终端中：

在 gLinux 或 Debian 上：

<!-- mdbook-xgettext: skip -->

```sh
gdb-multiarch target/thumbv7em-none-eabihf/debug/board_support --eval-command="target remote :1337"
```

在 MacOS 上：

<!-- mdbook-xgettext: skip -->

```sh
arm-none-eabi-gdb target/thumbv7em-none-eabihf/debug/board_support --eval-command="target remote :1337"
```

<details>

在 GDB 中，尝试运行：

<!-- mdbook-xgettext: skip -->

```gdb
b src/bin/board_support.rs:29
b src/bin/board_support.rs:30
b src/bin/board_support.rs:32
c
c
c
```

</details>
