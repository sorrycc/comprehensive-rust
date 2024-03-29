---
translated_at: '2024-03-26T10:48:20.726Z'
---

# 并发编程下午练习

## 哲学家就餐问题 --- 异步

（[回到练习](dining-philosophers-async.md)）

```rust,compile_fail
{{#include dining-philosophers-async.rs:solution}}
```

## 广播聊天应用

（[回到练习](chat-app.md)）

_src/bin/server.rs_：

```rust,compile_fail
{{#include chat-async/src/bin/server.rs:solution}}
```

_src/bin/client.rs_：

```rust,compile_fail
{{#include chat-async/src/bin/client.rs:solution}}
```
