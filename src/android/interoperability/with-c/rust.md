---
translated_at: '2024-03-26T11:59:21.394Z'
---

# 调用 Rust

将 Rust 函数和类型导出到 C 中非常简单：

_interoperability/rust/libanalyze/analyze.rs_

```rust,editable
{{#include rust/libanalyze/analyze.rs:analyze_numbers}}
```

_interoperability/rust/libanalyze/analyze.h_

```c
{{#include rust/libanalyze/analyze.h:analyze_numbers}}
```

_interoperability/rust/libanalyze/Android.bp_

```javascript
{{#include rust/libanalyze/Android.bp}}
```

我们现在可以从一个 C 二进制文件中调用它：

_interoperability/rust/analyze/main.c_

```c
{{#include rust/analyze/main.c:main}}
```

_interoperability/rust/analyze/Android.bp_

```javascript
{{#include rust/analyze/Android.bp}}
```

构建、推送并在你的设备上运行二进制文件：

```shell
{{#include ../../build_all.sh:analyze_numbers}}
```

<details>

`#[no_mangle]` 禁用了 Rust 的常规名称改编，所以导出的符号将会是函数的名称。你也可以使用 `#[export_name = "some_name"]` 来指定任何你想要的名字。

</details>
