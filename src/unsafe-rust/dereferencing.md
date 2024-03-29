---
minutes: 10
translated_at: '2024-03-26T09:55:43.425Z'
---

# 解引用原始指针

创建指针是安全的，但解引用它们需要 `unsafe`：

```rust,editable
fn main() {
    let mut s = String::from("careful!");

    let r1 = &mut s as *mut String;
    let r2 = r1 as *const String;

    // 安全，因为 r1 和 r2 是从引用中获得的，因此保证非空且对齐正确，
    // 且在整个 unsafe 块期间，它们所基于的引用对象是存活的，
    // 并且它们不会通过引用或其他任何指针并发访问。
    unsafe {
        println!("r1 是：{}", *r1);
        *r1 = String::from("uhoh");
        println!("r2 是：{}", *r2);
    }

    // 不安全。不要这么做。
    /*
    let r3: &String = unsafe { &*r1 };
    drop(s);
    println!("r3 是：{}", *r3);
    */
}
```

<details>

根据 Android Rust 风格指南的要求（以及良好的实践），编写每个 `unsafe` 块的注释解释其中的代码是如何满足其进行的不安全操作的安全要求的是很好的。

在指针解引用的情况下，这意味着指针必须是[_有效的_](https://doc.rust-lang.org/std/ptr/index.html#safety)，即：

- 指针必须非空。
- 指针必须是_可解引用的_（在单个分配的对象的范围内）。
- 对象未被释放。
- 不能有对同一位置的并发访问。
- 如果指针是通过强制转换引用获得的，底层对象必须是存活的并且不能使用引用来访问内存。

在大多数情况下，指针还必须正确对齐。

“不安全”部分给出了一个常见的 UB（未定义行为）错误示例：`*r1` 有 `'static` 生命周期，所以 `r3` 的类型是 `&'static String`，因此比 `s` 拥有更长的生存期。从指针创建引用需要_极其小心_。

</details>
