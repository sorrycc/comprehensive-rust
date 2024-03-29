---
translated_at: '2024-03-26T12:05:05.511Z'
---

# Rust 二进制文件

让我们从一个简单的应用开始。在 AOSP 检出的根目录下，创建以下文件：

_hello_rust/Android.bp_：

```javascript
{{#include binary/Android.bp}}
```

_hello_rust/src/main.rs_：

```rust
{{#include binary/src/main.rs:main}}
```

现在，您可以构建、推送并运行二进制文件了：

```shell
{{#include ../build_all.sh:hello_rust}}
```

```text
来自 Rust 的问候！
```
