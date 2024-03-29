---
translated_at: '2024-03-26T12:08:52.307Z'
---

# AIDL 服务端

最后，我们可以创建一个暴露服务的服务器：

_birthday_service/src/server.rs_：

```rust,ignore
{{#include ../birthday_service/src/server.rs:main}}
```

_birthday_service/Android.bp_：

```javascript
{{#include ../birthday_service/Android.bp:birthday_server}}
```

<details>

将用户定义的服务实现（在本例中是实现了 `IBirthdayService` 的 `BirthdayService` 类型）开启为一个 Binder 服务的过程包含多个步骤，可能比学生们在 C++ 或其他语言中使用 Binder 时习惯的要复杂。向学生解释每个步骤为何必要。

1. 创建你的服务类型的实例（`BirthdayService`）。
2. 将服务对象包装在相应的 `Bn*` 类型中（本例中是 `BnBirthdayService`）。这个类型由 Binder 生成，提供了由 C++ 中的 `BnBinder` 基类提供的常见 Binder 功能。我们在 Rust 中没有继承，所以我们使用组合，把我们的 `BirthdayService` 放到生成的 `BnBinderService` 中。
3. 调用 `add_service`，给它一个服务标识符和你的服务对象（示例中的 `BnBirthdayService` 对象）。
4. 调用 `join_thread_pool` 将当前线程加入 Binder 的线程池并开始监听连接。

</details>
