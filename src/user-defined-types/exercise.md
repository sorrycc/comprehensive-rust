---
minutes: 15
translated_at: '2024-03-26T09:48:49.014Z'
---

# 练习：电梯事件

我们将创建一个数据结构来表示电梯控制系统中的一个事件。由你来定义类型和函数来构建各种事件。使用 `#[derive(Debug)]` 使得类型可以使用 `{:?}` 格式化。

这个练习只需要创建并填充数据结构，以便 `main` 运行时没有错误。课程的下一部分将涵盖如何从这些结构中获取数据。

```rust,editable,should_panic
{{#include exercise.rs:event}}
    // 待办：添加所需的变体
}

{{#include exercise.rs:direction}}

{{#include exercise.rs:car_arrived}}
    todo!()
}

{{#include exercise.rs:car_door_opened}}
    todo!()
}

{{#include exercise.rs:car_door_closed}}
    todo!()
}

{{#include exercise.rs:lobby_call_button_pressed}}
    todo!()
}

{{#include exercise.rs:car_floor_button_pressed}}
    todo!()
}

{{#include exercise.rs:main}}
```
