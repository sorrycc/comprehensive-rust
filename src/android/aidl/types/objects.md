---
translated_at: '2024-03-26T12:06:51.441Z'
---

# 发送对象

AIDL 对象可以作为具体的 AIDL 类型或者作为类型抹去的 `IBinder` 接口发送：

**birthday_service/aidl/com/example/birthdayservice/IBirthdayInfoProvider.aidl**：

```java
{{#include ../birthday_service/aidl/com/example/birthdayservice/IBirthdayInfoProvider.aidl:IBirthdayInfoProvider}}
```

**birthday_service/aidl/com/example/birthdayservice/IBirthdayService.aidl**：

```java
import com.example.birthdayservice.IBirthdayInfoProvider;

interface IBirthdayService {
{{#include ../birthday_service/aidl/com/example/birthdayservice/IBirthdayService.aidl:with_info_provider}}
}
```

**birthday_service/src/client.rs**：

```rust,ignore
{{#include ../birthday_service/src/client.rs:InfoProvider}}

fn main() {
    binder::ProcessState::start_thread_pool();
    let service = connect().expect("无法连接到 BirthdayService");
{{#include ../birthday_service/src/client.rs:wish_with_provider}}
}
```

<details>

- 注意使用 `BnBirthdayInfoProvider`。它和我们之前看到的 `BnBirthdayService` 有着相同的作用。

</details>
