---
translated_at: '2024-03-26T11:34:35.638Z'
---

# `tinyvec`

有时你想要一个像 `Vec` 那样可以调整大小的东西，但又不想进行堆分配。[`tinyvec`][1] 提供了这样的功能：一个由数组或切片支撑的向量，它可以是静态分配的或者储存在栈上的，这个向量跟踪使用了多少元素，并且如果你试图使用超过分配数量的元素，它会发生恐慌。

```rust,editable,compile_fail
use tinyvec::{array_vec, ArrayVec};

fn main() {
    let mut numbers: ArrayVec<[u32; 5]> = array_vec!(42, 66);
    println!("{numbers:?}");
    numbers.push(7);
    println!("{numbers:?}");
    numbers.remove(1);
    println!("{numbers:?}");
}
```

<details>

- `tinyvec` 要求元素类型实现 `Default` 以便初始化。
- Rust Playground 包含了 `tinyvec`，因此这个例子可以直接在线运行。

</details>

[1]: https://crates.io/crates/tinyvec
