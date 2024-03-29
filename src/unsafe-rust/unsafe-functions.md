---
minutes: 5
translated_at: '2024-03-26T09:53:04.375Z'
---

# 不安全函数

## 调用不安全函数

如果一个函数或方法需要额外的前提条件来避免未定义行为，那么它可以被标记为 `unsafe`：

```rust,editable
extern "C" {
    fn abs(input: i32) -> i32;
}

fn main() {
    let emojis = "🗻∈🌏";

    // 安全，因为索引顺序正确，且位于字符串切片的边界内，
    // 且位于 UTF-8 序列边界上。
    unsafe {
        println!("emoji: {}", emojis.get_unchecked(0..4));
        println!("emoji: {}", emojis.get_unchecked(4..7));
        println!("emoji: {}", emojis.get_unchecked(7..11));
    }

    println!("字符计数: {}", count_chars(unsafe { emojis.get_unchecked(0..7) }));

    unsafe {
        // 如果 abs 表现异常，将会导致未定义行为。
        println!("C 语言中 -3 的绝对值: {}", abs(-3));
    }

    // 不遵守 UTF-8 编码要求会破坏内存安全！
    // println!("emoji: {}", unsafe { emojis.get_unchecked(0..3) });
    // println!("字符计数: {}", count_chars(unsafe {
    // emojis.get_unchecked(0..3) }));
}

fn count_chars(s: &str) -> usize {
    s.chars().count()
}
```

## 编写不安全函数

如果你的函数需要特定条件来避免未定义行为，你可以将它标记为 `unsafe`。

```rust,editable
/// 交换给定指针所指向的值。
///
/// # 安全性
///
/// 指针必须是有效的并且正确对齐。
unsafe fn swap(a: *mut u8, b: *mut u8) {
    let temp = *a;
    *a = *b;
    *b = temp;
}

fn main() {
    let mut a = 42;
    let mut b = 66;

    // 安全，因为 ...
    unsafe {
        swap(&mut a, &mut b);
    }

    println!("a = {}, b = {}", a, b);
}
```

<details>

## 调用不安全函数

`get_unchecked`，像大多数 `_unchecked` 函数一样，是不安全的，因为如果范围不正确，它可能引起 UB（未定义行为）。`abs` 的不正确之处在于它是一个外部函数（FFI）。当这些函数执行可能违反 Rust 的指针操作时，通常只有在调用外部函数时才会出现问题。

内存模型，但通常任何 C 函数在任意情况下都可能有未定义行为。

这里的 `"C"` 是指 ABI；[还有其他的 ABI 可用](https://doc.rust-lang.org/reference/items/external-blocks.html)。

## 编写不安全函数

我们实际上不会用指针来做 `swap` 函数——这可以通过引用安全地完成。

注意，不安全代码在不安全函数中无需 `unsafe` 块即可使用。我们可以通过 `#[deny(unsafe_op_in_unsafe_fn)]` 来禁止这种做法。尝试添加它并看看会发生什么。这在未来的 Rust 版本中很可能会有所变化。

</details>
