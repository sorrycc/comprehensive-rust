---
translated_at: '2024-03-26T11:38:40.364Z'
---

# 板级支持包

板级支持包为特定的板子提供了进一步的封装，以方便使用。

<!-- mdbook-xgettext: skip -->

```rust,editable,compile_fail
{{#include examples/src/bin/board_support.rs:Example}}
```

<details>

- 在这个案例中，板级支持包只是提供了更有用的名字和一些初始化操作。
- 该包也可能包含一些板载设备（非微控制器本身）的驱动程序。
  - `microbit-v2` 包含了一个 LED 矩阵的简单驱动程序。

使用以下命令运行示例：

```sh
cargo embed --bin board_support
```

</details>
