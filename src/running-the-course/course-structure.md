---
translated_at: '2024-03-26T10:17:58.941Z'
---

# 课程结构

> 本页面供课程讲师使用。

## Rust 基础

前四天是 [Rust 基础](../welcome-day-1.md)。这几天节奏快，我们将覆盖很多内容！

{{%课程大纲 基础知识%}}

## 深入探讨

除了为期 4 天的 Rust 基础课程，我们还会涉及一些更专业的主题：

### Rust 在安卓中的应用

[Rust 在安卓中的应用](../android.md) 深入探讨是一个半天的课程，内容涉及 Rust 在安卓平台开发中的使用。这包括与 C、C++ 和 Java 的互操作性。

你将需要一个 [AOSP 检出][1]。在同一台机器上检出
[课程仓库][2] 并将 `src/android/` 目录移至您的 AOSP 检出的根目录。这可以确保安卓构建系统能够识别 `src/android/` 中的 `Android.bp` 文件。

确保 `adb sync` 能够与你的模拟器或真实设备正常工作，并使用 `src/android/build_all.sh` 预构建所有安卓示例。阅读脚本以查看它运行的命令，并确保在你手动运行时它们能够正常工作。

[1]: https://source.android.com/docs/setup/download/downloading
[2]: https://github.com/google/comprehensive-rust

### Rust 在 Chromium 中的应用

[Rust 在 Chromium 中的应用](../chromium.md) 深入探讨是一个半天的课程，讲述如何在 Chromium 浏览器中使用 Rust。内容包括在 Chromium 的 `gn` 构建系统中使用 Rust、引入第三方库（“crates”）和 C++ 的互操作性。

你需要能够构建 Chromium ——出于速度考虑，建议进行[调试，组件构建](../chromium/setup.md)，但任何构建都可以工作。确保你可以运行你构建的 Chromium 浏览器。

### 裸机 Rust

[裸机 Rust](../bare-metal.md) 深入探讨是为期一整天的课程，讲述如何在裸机（嵌入式）开发中使用 Rust。课程内容涵盖了微控制器和应用处理器。

对于微控制器部分，你需要提前购买 [BBC micro:bit](https://microbit.org/) v2 开发板。
每个人都需要安装如下描述的一系列软件包：

[欢迎页面](../bare-metal.md)。

### Rust 中的并发

深入探索 [Rust 中的并发](../concurrency.md) 是一个全天候的课程，内容包括经典并发以及 `async`/`await` 并发。

你需要设置一个新的 crate，下载并准备好依赖。然后，你可以将例子复制/粘贴到 `src/main.rs` 中进行实验：

```shell
cargo init concurrency
cd concurrency
cargo add tokio --features full
cargo run
```

## 格式

本课程旨在非常互动，我们推荐让问题驱动对 Rust 的探索！
