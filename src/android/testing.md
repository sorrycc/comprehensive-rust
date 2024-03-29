---
translated_at: '2024-03-26T11:54:49.807Z'
---

# 在 Android 中进行测试

基于 [测试](../testing.md)，我们现在将查看 AOSP 中单元测试是如何工作的。使用 `rust_test` 模块来进行你的单元测试：

_testing/Android.bp_：

```javascript
{{#include testing/Android.bp}}
```

_testing/src/lib.rs_：

```rust
{{#include testing/src/lib.rs:leftpad}}
```

现在你可以使用以下命令运行测试：

```shell
{{#include build_all.sh:libleftpad_test}}
```

输出看起来是这样的：

```text
INFO: Elapsed time: 2.666s, Critical Path: 2.40s
INFO: 3 processes: 2 internal, 1 linux-sandbox.
INFO: Build completed successfully, 3 total actions
//comprehensive-rust-android/testing:libleftpad_test_host            PASSED in 2.3s
    PASSED  libleftpad_test.tests::long_string (0.0s)
    PASSED  libleftpad_test.tests::short_string (0.0s)
测试用例：完成 2 个测试用例的执行，2 个通过且 0 个失败
```

注意你只需提及库 crate 的根目录。测试会在嵌套模块中递归地被发现。
