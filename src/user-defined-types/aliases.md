---
minutes: 2
translated_at: '2024-03-26T09:50:38.834Z'
---

# 类型别名

类型别名为另一个类型创建一个名字。这两个类型可以互换使用。

```rust,editable
enum CarryableConcreteItem {
    Left,
    Right,
}

type Item = CarryableConcreteItem;

// 别名在长的、复杂的类型中更有用：
use std::cell::RefCell;
use std::sync::{Arc, RwLock};
type PlayerInventory = RwLock<Vec<Arc<RefCell<Item>>>>;
```

<details>

C 程序员会认出这和 `typedef` 相似。

</details>
