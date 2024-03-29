---
translated_at: '2024-03-26T11:55:24.778Z'
---

# 日志记录

你应该使用 `log` 库自动记录到 `logcat`（设备上）或 `stdout`（主机上）：

_hello_rust_logs/Android.bp_：

```javascript
{{#include logging/Android.bp}}
```

_hello_rust_logs/src/main.rs_：

```rust,ignore
{{#include logging/src/main.rs:main}}
```

在你的设备上构建、推送并运行二进制文件：

```shell
{{#include build_all.sh:hello_rust_logs}}
```

日志会显示在 `adb logcat` 中：

```shell
adb logcat -s rust
```

```text
09-08 08:38:32.454  2420  2420 D rust: hello_rust_logs: 程序启动。
09-08 08:38:32.454  2420  2420 I rust: hello_rust_logs: 一切都很好。
09-08 08:38:32.454  2420  2420 E rust: hello_rust_logs: 出了点问题！
```
