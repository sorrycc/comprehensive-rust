---
minutes: 5
translated_at: '2024-03-26T09:51:40.083Z'
---

# 实现不安全特质

就像函数一样，如果实现必须保证特定条件以避免未定义行为，你可以将特质标记为 `unsafe`。

例如，`zerocopy` crate 有一个不安全特质，看起来像[这样](https://docs.rs/zerocopy/latest/zerocopy/trait.AsBytes.html)：

```rust,editable
use std::mem::size_of_val;
use std::slice;

/// ...
/// # 安全性
/// 类型必须有一个定义的表示形式且没有填充。
pub unsafe trait AsBytes {
    fn as_bytes(&self) -> &[u8] {
        unsafe {
            slice::from_raw_parts(
                self as *const Self as *const u8,
                size_of_val(self),
            )
        }
    }
}

// 因为 u32 有一个定义的表示形式且没有填充，所以安全。
unsafe impl AsBytes for u32 {}
```

<details>

在 Rustdoc 中应该有一个 `# 安全性` 部分，解释安全实现特质的要求。

实际上，`AsBytes` 的安全性部分要长得多，也更复杂。

内置的 `Send` 和 `Sync` 特质是不安全的。

</details>
