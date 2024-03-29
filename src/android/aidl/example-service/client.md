---
translated_at: '2024-03-26T12:10:30.741Z'
---

# AIDL 客户端

最后，我们可以为我们的新服务创建一个 Rust 客户端。

_birthday_service/src/client.rs_：

```rust,ignore
use com_example_birthdayservice::aidl::com::example::birthdayservice::IBirthdayService::IBirthdayService;
use com_example_birthdayservice::binder;

{{#include ../birthday_service/src/client.rs:main}}
}
```

_birthday_service/Android.bp_：

```javascript
{{#include ../birthday_service/Android.bp:birthday_client}}
```

请注意，客户端并不依赖于 `libbirthdayservice`。

构建，推送，并在你的设备上运行客户端：

```shell
{{#include ../../build_all.sh:birthday_client}}
```

```text
Happy Birthday Charlie, congratulations with the 60 years!
```

<details>

- `Strong<dyn IBirthdayService>` 是代表客户端已连接到的服务的特征对象。
  - `Strong` 是 Binder 的一个自定义智能指针类型。它同时处理服务特征对象的进程内引用计数，以及跟踪有多少进程引用了该对象的全局 Binder 引用计数。
  - 请注意，客户端用于与服务通信的特征对象使用的是服务器实现的完全相同的特征。对于给定的 Binder 接口，会生成一个单一的 Rust 特征，客户端和服务器都会使用。
- 使用注册服务时使用的相同服务标识符。理想情况下，这应定义在一个共同的包中，客户端和服务器都可以依赖它。

</details>
