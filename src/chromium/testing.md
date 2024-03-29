---
translated_at: '2024-03-26T11:10:37.594Z'
---

# 测试

Rust 社区通常在与被测试代码相同的源文件中创建一个模块来编写单元测试。这在课程的 [早期](../testing.md) 已经介绍过，如下所示：

```rust
#[cfg(test)]
mod tests {
    #[test]
    fn my_test() {
        todo!()
    }
}
```

在 Chromium 中，我们将单元测试放在一个单独的源文件中，并且我们继续对 Rust 代码遵循这个实践 --- 这使得测试能够被一致地发现，并且有助于避免重新构建 `.rs` 文件第二次（在 `test` 配置中）。

这导致了以下几种在 Chromium 中测试 Rust 代码的选项：

- 原生的 Rust 测试（即 `#[test]`）。在 `//third_party/rust` 之外不推荐使用。
- 用 C++ 编写的 `gtest` 测试，并通过 FFI 调用来执行 Rust 代码。当 Rust 代码只是一个薄薄的 FFI 层，并且现有的单元测试为特性提供了足够的测试覆盖时足够使用。
- 用 Rust 编写的 `gtest` 测试，通过它的公开 API 使用被测试的 crate（如果需要，使用 `pub mod for_testing { ... }`）。这是接下来几个幻灯片的主题。

<details>

提到原生 Rust 测试的第三方 crate 最终应该被 Chromium 机器人执行。（这样的测试很少需要 --- 只有在添加或更新第三方 crate 后。）

一些例子可能有助于说明何时应该使用 C++ 的 `gtest` 与 Rust 的 `gtest`：

- QR 在第一方 Rust 层几乎无任何功能（它只是一个薄薄的 FFI 粘合剂），因此它使用现有的 C++ 单元测试来测试 C++ 和 Rust 实现（通过参数化测试，以便它们使用 `ScopedFeatureList` 来启用或禁用 Rust）。

- 假设/WIP 的 PNG 集成可能需要实现 `libpng` 提供但在 `png` crate 中缺失的像素转换的内存安全的实现 - 例如，RGBA => BGRA 或伽玛校正。这样的功能可能会从用 Rust 编写的单独测试中受益。

</details>
