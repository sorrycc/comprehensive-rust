---
minutes: 5
translated_at: '2024-03-26T11:58:10.167Z'
---

# GoogleTest

[GoogleTest](https://docs.rs/googletest/) 包允许使用 _匹配器_ 进行灵活的测试断言：

```rust,ignore
{{#include googletest.rs:test_elements_are}}
```

如果我们将最后一个元素更改为 `"!"`，测试将失败，并带有指出错误的结构化错误消息：

<!-- mdbook-xgettext: skip -->

```text
---- test_elements_are stdout ----
值为：value
期望：具有元素：
  0. 等于 "foo"
  1. 小于 "xyz"
  2. 以前缀 "!" 开头
实际：["foo", "bar", "baz"]，
  其中元素 #2 为 "baz"，它不以 "!" 开头
  位于 src/testing/googletest.rs:6:5
错误：查看上面的失败输出
```

<details>

- GoogleTest 不是 Rust Playground 的一部分，因此你需要在本地环境中运行此示例。使用 `cargo add googletest` 可以快速将其添加到现有的 Cargo 项目中。

- `use googletest::prelude::*;` 行导入了许多[常用的宏和类型][prelude]。

- 这只是冰山一角，还有许多内置匹配器。

- 一个特别好的功能是，多行字符串中的不匹配以 diff 形式显示：

```rust,ignore
{{#include googletest.rs:test_multiline_string_diff}}
```

显示了一个颜色编码的 diff（这里未显示颜色）：

<!-- mdbook-xgettext: skip -->

```text
    值为：haiku
期望：等于 "Memory safety found,\nRust's silly humor guides the way,\nSecure code you'll write."
实际："Memory safety found,\nRust's strong typing guides the way,\nSecure code you'll write."，
  与 "Memory safety found,\nRust's silly humor guides the way,\nSecure code you'll write." 不等。
差异（-实际 / +期望）：
 Memory safety found,
-Rust's strong typing guides the way,
+Rust's silly humor guides the way,
 Secure code you'll write.
  位于 src/testing/googletest.rs:17:5
```

- 该包是 [C++ 的 GoogleTest](https://google.github.io/googletest/) 的 Rust 移植。

[prelude]: https://docs.rs/googletest/latest/googletest/prelude/index.html

</details>
