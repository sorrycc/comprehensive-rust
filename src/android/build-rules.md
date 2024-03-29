---
translated_at: '2024-03-26T11:56:20.248Z'
---

# 构建规则

Android 构建系统（Soong）通过许多模块支持 Rust：

| 模块类型             | 描述                                                                                              |
| ------------------- | ------------------------------------------------------------------------------------------------ |
| `rust_binary`       | 生成 Rust 二进制文件。                                                                            |
| `rust_library`      | 生成 Rust 库文件，并提供 `rlib` 和 `dylib` 两种变体。                                            |
| `rust_ffi`          | 生成 Rust C 库文件以供 `cc` 模块使用，并提供静态和共享两种变体。                                |
| `rust_proc_macro`   | 生成 `proc-macro` Rust 库文件。这些与编译器插件类似。                                           |
| `rust_test`         | 生成使用标准 Rust 测试工具的 Rust 测试二进制文件。                                              |
| `rust_fuzz`         | 生成利用 `libfuzzer` 的 Rust 模糊测试二进制文件。                                                |
| `rust_protobuf`     | 生成源代码并生成提供特定 protobuf 接口的 Rust 库文件。                                           |
| `rust_bindgen`      | 生成源代码并生成包含 C 库 Rust 绑定的 Rust 库文件。                                              |

接下来我们将了解 `rust_binary` 和 `rust_library`。

<details>

附加可能会提及的事项：

- Cargo 不适用于多语言仓库，并且还会从互联网下载包。

- 为了合规和性能，Android 必须在代码树内拥有 crates。它还必须与 C/C++/Java 代码进行交互。Soong 填补了这个空白。

- Soong 与 Bazel 有许多相似之处，后者是 Blaze（在 google3 中使用）的开源变体。

- 有计划将 [Android](https://source.android.com/docs/setup/build/bazel/introduction)、[ChromeOS](https://chromium.googlesource.com/chromiumos/bazel/) 和 [Fuchsia](https://source.android.com/docs/setup/build/bazel/introduction) 过渡到 Bazel。
</details>

- 学习类似 Bazel 的构建规则对所有 Rust OS 开发者都很有用。

- 有趣的事实：《星际迷航》中的 Data 是索隆型安卓人。
