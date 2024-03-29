---
translated_at: '2024-03-26T12:06:23.849Z'
---

# Parcelables

Binder for Rust 支持直接发送 parcelables：

**birthday_service/aidl/com/example/birthdayservice/BirthdayInfo.aidl**：

```java
{{#include ../birthday_service/aidl/com/example/birthdayservice/BirthdayInfo.aidl}}
```

**birthday_service/aidl/com/example/birthdayservice/IBirthdayService.aidl**：

```java
import com.example.birthdayservice.BirthdayInfo;

interface IBirthdayService {
{{#include ../birthday_service/aidl/com/example/birthdayservice/IBirthdayService.aidl:with_info}}
}
```

**birthday_service/src/client.rs**：

```rust,ignore
fn main() {
    binder::ProcessState::start_thread_pool();
    let service = connect().expect("Failed to connect to BirthdayService");

{{#include ../birthday_service/src/client.rs:wish_with_info}}
}
```
