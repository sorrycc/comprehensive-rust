---
minutes: 20
translated_at: '2024-03-26T10:35:14.469Z'
---

# 练习：构造器类型

在这个例子中，我们将实现一个复杂的数据类型，它拥有自己的所有数据。我们将使用“构造器模式”来支持逐步构建一个新值，使用便利函数。

填写缺失的部分。

```rust,should_panic,editable
{{#include exercise.rs:Package}}
{{#include exercise.rs:as_dependency}}
        todo!("1")
    }
}

{{#include exercise.rs:PackageBuilder}}
{{#include exercise.rs:new}}
        todo!("2")
    }

{{#include exercise.rs:version}}

{{#include exercise.rs:authors}}
        todo!("3")
    }

{{#include exercise.rs:dependency}}
        todo!("4")
    }

{{#include exercise.rs:language}}
        todo!("5")
    }

{{#include exercise.rs:build}}

{{#include exercise.rs:main}}
```
