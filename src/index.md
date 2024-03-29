---
translated_at: '2024-03-26T09:38:07.138Z'
---

# 欢迎来到全面的 Rust 语言课程 🦀

[![构建工作流](https://img.shields.io/github/actions/workflow/status/google/comprehensive-rust/build.yml?style=flat-square)](https://github.com/google/comprehensive-rust/actions/workflows/build.yml?query=branch%3Amain)
[![GitHub 贡献者](https://img.shields.io/github/contributors/google/comprehensive-rust?style=flat-square)](https://github.com/google/comprehensive-rust/graphs/contributors)
[![GitHub 星标](https://img.shields.io/github/stars/google/comprehensive-rust?style=flat-square)](https://github.com/google/comprehensive-rust/stargazers)

这是由 Google 的 Android 团队开发的免费 Rust 语言课程。课程涵盖了 Rust 的整个光谱，从基础语法到高级主题，如泛型和错误处理。

> 课程的最新版本可在
> <https://google.github.io/comprehensive-rust/> 找到。如果您在其他地方阅读，请在那里检查更新。
>
> 课程还提供了 [PDF 版本](comprehensive-rust.pdf)。

本课程的目标是教您学习 Rust。我们假设您对 Rust 一无所知，并希望能够：

- 给您一个全面的 Rust 语法和语言理解。
- 使您能够修改现有程序并用 Rust 编写新程序。
- 向您展示常见的 Rust 习惯用法。

我们将课程的前四天称为 Rust 基础。

在此基础上，我们邀请您深入研究一个或多个专门话题：

- [Android](android.md)：半天的关于使用 Rust 进行 Android 平台开发（AOSP）的课程。这包括与 C、C++ 和 Java 的互操作性。
- [Chromium](chromium.md)：半天的关于在基于 Chromium 的浏览器中使用 Rust 的课程。这包括与 C++ 的互操作性，以及如何在 Chromium 中包含第三方 crate。
- [裸机](bare-metal.md)：关于使用 Rust 进行裸机（嵌入式）开发的一整天课程。涵盖了微控制器和应用处理器。
- [并发](concurrency.md)：一整天关于 Rust 中并发的课程。我们

## 本课程覆盖的内容

本课程将同时涵盖传统的并发（使用线程和互斥锁的抢占式调度）以及异步/等待并发（使用 Future 的协作式多任务处理）。

## 非目标

Rust 是一种庞大的语言，我们不可能在几天内涵盖其全部内容。本课程的一些非目标包括：

- 学习如何开发宏：请参阅
  [Rust 书籍中的第 19.5 章](https://doc.rust-lang.org/book/ch19-06-macros.html)
  以及 [Rust by Example](https://doc.rust-lang.org/rust-by-example/macros.html)。

## 假设

本课程假定你已经知道如何编程。Rust 是一种静态类型语言，我们有时会与 C 和 C++ 做比较，以更好地解释或对比 Rust 的方法。

如果你知道如何使用动态类型语言（如 Python 或 JavaScript）编程，那么你也会很容易跟上课程的内容。

<details>

这是一个 _演讲者笔记_ 的示例。我们将使用这些笔记来为幻灯片添加额外的信息。这可能是讲师应该覆盖的要点，以及课堂上常见问题的答案。

</details>
