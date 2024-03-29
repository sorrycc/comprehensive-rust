---
translated_at: '2024-03-26T11:35:40.830Z'
---

# `aarch64-paging`

[`aarch64-paging`][1] crate 允许你根据 AArch64 虚拟内存系统架构创建页面表。

```rust,editable,compile_fail
use aarch64_paging::{
    idmap::IdMap,
    paging::{Attributes, MemoryRegion},
};

const ASID: usize = 1;
const ROOT_LEVEL: usize = 1;

// 创建一个具有身份映射的新页面表。
let mut idmap = IdMap::new(ASID, ROOT_LEVEL);
// 将一个 2 MiB 的内存区域映射为只读。
idmap.map_range(
    &MemoryRegion::new(0x80200000, 0x80400000),
    Attributes::NORMAL | Attributes::NON_GLOBAL | Attributes::READ_ONLY,
).unwrap();
// 设置 `TTBR0_EL1` 以激活页面表。
idmap.activate();
```

<details>

- 目前它只支持 EL1，但添加对其他异常级别的支持应该很简单。
- 这在 Android 上用于 [保护 VM 固件][2]。
- 运行此示例没有简单的方法，因为它需要在真实硬件上或在 QEMU 下运行。

</details>

[1]: https://crates.io/crates/aarch64-paging
[2]: https://cs.android.com/android/platform/superproject/+/master:packages/modules/Virtualization/pvmfw/
