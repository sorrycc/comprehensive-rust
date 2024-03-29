---
translated_at: '2024-03-26T11:19:55.258Z'
---

# CXX 错误处理：PNG 示例

一个 PNG 解码器的原型展示了当成功的结果无法通过 FFI 边界传递时可以做什么：

```rust,ignore
#[cxx::bridge(namespace = "gfx::rust_bindings")]
mod ffi {
    extern "Rust" {
        /// 这返回一个与 `Result<PngReader<'a>, ()>` 等效的 FFI 友好型。
        fn new_png_reader<'a>(input: &'a [u8]) -> Box<ResultOfPngReader<'a>>;

        /// C++ 绑定 `crate::png::ResultOfPngReader` 类型。
        type ResultOfPngReader<'a>;
        fn is_err(self: &ResultOfPngReader) -> bool;
        fn unwrap_as_mut<'a, 'b>(
            self: &'b mut ResultOfPngReader<'a>,
        ) -> &'b mut PngReader<'a>;

        /// C++ 绑定 `crate::png::PngReader` 类型。
        type PngReader<'a>;
        fn height(self: &PngReader) -> u32;
        fn width(self: &PngReader) -> u32;
        fn read_rgba8(self: &mut PngReader, output: &mut [u8]) -> bool;
    }
}
```

<details>

`PngReader` 和 `ResultOfPngReader` 是 Rust 类型 --- 这些类型的对象不能不通过 `Box<T>` 的间接方式跨越 FFI 边界。我们不能拥有一个 `out_parameter: &mut PngReader`，因为 CXX 不允许 C++ 按值存储 Rust 对象。

这个示例表明，即使 CXX 不支持任意泛型或模板，我们仍然可以通过手动专门化 / 单态化它们成非泛型类型，从而跨越 FFI 边界传递它们。在示例中，`ResultOfPngReader` 是一个非泛型类型，它转发到 `Result<T, E>` 的适当方法中（例如，进入 `is_err`、`unwrap` 和/或 `as_mut`）。

</details>
