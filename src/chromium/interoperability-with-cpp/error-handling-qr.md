---
translated_at: '2024-03-26T11:19:19.551Z'
---

# CXX 错误处理：QR 示例

QR 码生成器是 [一个例子][0]，在这个例子中，布尔值被用来表达成功与否，而成功的结果可以跨 FFI 边界传递：

```rust,ignore
#[cxx::bridge(namespace = "qr_code_generator")]
mod ffi {
    extern "Rust" {
        fn generate_qr_code_using_rust(
            data: &[u8],
            min_version: i16,
            out_pixels: Pin<&mut CxxVector<u8>>,
            out_qr_size: &mut usize,
        ) -> bool;
    }
}
```

<details>

学生可能对 `out_qr_size` 输出的语义感到好奇。这不是向量的大小，而是 QR 码的大小（并且它确实有点多余 - 这是向量大小的平方根）。

可能值得指出在调用 Rust 函数之前初始化 `out_qr_size` 的重要性。创建一个指向未初始化内存的 Rust 引用会导致未定义行为（不像在 C++ 中，只有解引用这样的内存时才会导致 UB）。

如果学生询问关于 `Pin` 的问题，那么解释 CXX 为什么需要它来修改对 C++ 数据的引用：答案是 C++ 数据不能像 Rust 数据那样移动，因为它可能包含自引用指针。

</details>

[0]: https://source.chromium.org/chromium/chromium/src/+/main:components/qr_code_generator/qr_code_generator_ffi_glue.rs;l=13-18;drc=7bf1b75b910ca430501b9c6a74c1d18a0223ecca
