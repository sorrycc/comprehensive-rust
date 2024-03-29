---
translated_at: '2024-03-26T12:08:19.649Z'
---

# 生成的服务 API

Binder 生成一个与接口定义相对应的 trait。此 trait 用于与服务进行通信。

_birthday_service/aidl/com/example/birthdayservice/IBirthdayService.aidl_：

```java
{{#include ../birthday_service/aidl/com/example/birthdayservice/IBirthdayService.aidl:IBirthdayService}}
}
```

_生成的 trait_：

```rust,ignore
trait IBirthdayService {
    fn wishHappyBirthday(&self, name: &str, years: i32) -> binder::Result<String>;
}
```

你的服务需要实现这个 trait，而你的客户端将使用这个 trait 与服务进行通信。

<details>

- 生成的绑定可以在 `out/soong/.intermediates/<模块路径>/` 找到。
- 指出生成的函数签名，特别是参数和返回类型，如何对应于接口定义。
  - 作为参数的 `String` 会导致与作为返回类型的 `String` 不同的 Rust 类型。

</details>
