---
translated_at: '2024-03-26T10:54:48.650Z'
---

# 将一切整合在一起 --- 练习

在这个练习中，你将为 Chromium 添加一个全新的功能，整合你已经学到的所有知识。

## 产品管理的简报

在一个偏远的热带雨林中发现了一个小精灵社区。尽可能快地为他们提供专为小精灵开发的 Chromium 是很重要的。

要求是将所有 Chromium 的界面字符串翻译成小精灵语言。

没有时间等待正确的翻译，但幸运的是，小精灵语与英语非常接近，而且事实证明有一个 Rust 包可以进行翻译。

实际上，你已经在之前的练习中[导入了那个包][0]。

（很明显，真正的 Chrome 翻译需要极其谨慎和勤奋。不要发布这个！）

## 步骤

修改 `ResourceBundle::MaybeMangleLocalizedString`，使其在显示前将所有字符串转换成 uwuified 形式。在这个特殊版本的 Chromium 中，无论 `mangle_localized_strings_` 的设置如何，它都应该这样做。

如果你在所有这些练习中都做对了，恭喜你，你应该创建了适用于小精灵的 Chrome！

<img src="chwomium.png" alt="带有 uwu 语言的 Chromium 界面截图">

<details>
学生很可能需要一些提示。提示包括：

- UTF16 与 UTF8。学生应该知道 Rust 字符串始终是 UTF8 的，并且可能会决定在 C++ 端使用 `base::UTF16ToUTF8` 进行转换，并且回转。
- 如果学生决定在 Rust 端进行转换，他们需要考虑[`String::from_utf16`][1]，考虑错误处理，以及考虑哪些 [CXX 支持的类型可以传输大量 u16s][2]。
- 学生可能以几种不同的方式设计 C++/Rust 边界，例如，通过值传递字符串，或者对字符串使用可变引用。如果使用了可变引用，则 CXX 可能会告诉学生，他们需要使用[`Pin`][3]。你可能需要解释 `Pin` 的作用，然后解释为什么 CXX 需要它来处理对 C++ 数据的可变引用：答案是 C++ 数据不能像 Rust 数据那样被移动，因为它可能包含自引用指针。
- 包含 `ResourceBundle::MaybeMangleLocalizedString` 的 C++ 目标将

需要依赖一个 `rust_static_library` 目标。学生可能已经做到了。
- `rust_static_library` 目标将需要依赖于 `//third_party/rust/uwuify/v0_2:lib`。

</details>

[0]: https://crates.io/crates/uwuify
[1]: https://doc.rust-lang.org/std/string/struct.String.html#method.from_utf16
[2]: https://cxx.rs/binding/slice.html
[3]: https://doc.rust-lang.org/std/pin/
