---
minutes: 5
translated_at: '2024-03-26T09:53:26.011Z'
---

# 联合体

联合体与枚举类似，但你需要自己跟踪活动字段：

```rust,editable
#[repr(C)]
union MyUnion {
    i: u8,
    b: bool,
}

fn main() {
    let u = MyUnion { i: 42 };
    println!("int: {}", unsafe { u.i });
    println!("bool: {}", unsafe { u.b }); // 未定义行为！
}
```

<details>

在 Rust 中，极少需要使用联合体，因为你通常可以使用枚举。它们偶尔需要用于与 C 库 API 交互。

如果你只是想将字节重新解释为不同的类型，你可能想要 [`std::mem::transmute`](https://doc.rust-lang.org/stable/std/mem/fn.transmute.html) 或者一个安全的包装器，如 [`zerocopy`](https://crates.io/crates/zerocopy) 包。

</details>
