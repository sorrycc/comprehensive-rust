---
minutes: 8
translated_at: '2024-03-26T10:26:58.347Z'
---

# use、super、self

模块可以通过 `use` 将其它模块中的符号引入作用域内。你通常会在每个模块的顶部看到类似这样的代码：

```rust,editable
use std::collections::HashSet;
use std::process::abort;
```

## 路径

路径解析如下：

1. 作为相对路径：
   - `foo` 或 `self::foo` 指当前模块中的 `foo`，
   - `super::foo` 指父模块中的 `foo`。

2. 作为绝对路径：
   - `crate::foo` 指当前包的根中的 `foo`，
   - `bar::foo` 指 `bar` 包中的 `foo`。

<details>

- 经常会“重新导出”符号到一个更短的路径。例如，一个包的顶层 `lib.rs` 可能会有

  ```rust,ignore
  mod storage;

  pub use storage::disk::DiskStorage;
  pub use storage::network::NetworkStorage;
  ```

  使得 `DiskStorage` 和 `NetworkStorage` 对其他包可用，且路径简短、便捷。

- 大多数情况下，只有出现在模块中的项目需要被 `use` 引用。然而，要调用某个 trait 的任何方法，即使已在作用域中有实现该 trait 的类型，该 trait 也必须在作用域中。例如，要使用实现了 `Read` trait 的类型上的 `read_to_string` 方法，你需要 `use std::io::Read`。

- `use` 语句可以有通配符：`use std::io::*`。这是不推荐的，因为不清楚导入了哪些项目，而且这些项目可能会随时间变化。

</details>
