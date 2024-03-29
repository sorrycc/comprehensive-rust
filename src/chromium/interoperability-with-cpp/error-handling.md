---
translated_at: '2024-03-26T11:18:49.158Z'
---

# CXX 错误处理

CXX 对 `Result<T, E>` 的[支持][0]依赖于 C++ 异常，因此我们不能在 Chromium 中使用它。替代方案：

- `Result<T, E>` 的 `T` 部分可以是：
  - 通过输出参数返回（例如通过 `&mut T`）。这要求 `T` 可以跨越 FFI 边界传递 - 例如 `T` 必须是：
    - 原始类型（如 `u32` 或 `usize`）
    - `cxx` 原生支持的类型（如 `UniquePtr<T>`），在失败情况下有合适的默认值可用（_不像_ `Box<T>`）。
  - 保留在 Rust 一侧，并通过引用暴露。当 `T` 是一个 Rust 类型时，可能需要这样做，该类型不能跨越 FFI 边界传递，并且不能存储在 `UniquePtr<T>` 中。

- `Result<T, E>` 的 `E` 部分可以是：
  - 作为布尔值返回（例如，`true` 表示成功，`false` 表示失败）
  - 理论上可能保留错误细节，但到目前为止在实践中还没被需要。

[0]: https://cxx.rs/binding/result.html
