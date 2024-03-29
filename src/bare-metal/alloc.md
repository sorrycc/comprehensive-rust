---
translated_at: '2024-03-26T11:33:52.075Z'
---

# `alloc`

要使用 `alloc`，你必须实现一个[全局（堆）分配器](https://doc.rust-lang.org/stable/std/alloc/trait.GlobalAlloc.html)。

```rust,editable,compile_fail
{{#include alloc-example/src/main.rs:Alloc}}
```

<details>

- `buddy_system_allocator` 是一个第三方 crate，实现了一个基本的伙伴系统分配器。还有其他 crate 可用，或者你可以编写自己的分配器，或者接入你现有的分配器。
- `LockedHeap` 的常量参数是分配器的最大阶数；即在这个例子中，它可以分配最大到 2**32 字节的区域。
- 如果你的依赖树中的任何 crate 依赖于 `alloc`，那么你的二进制文件中必须只定义一个全局分配器。通常这在顶级二进制 crate 中完成。
- `extern crate panic_halt as _` 是必要的，以确保 `panic_halt` crate 被链接进去，这样我们才能获得其 panic 处理程序。
- 这个例子能编译，但不会运行，因为它没有入口点。

</details>
