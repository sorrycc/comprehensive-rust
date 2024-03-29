---
translated_at: '2024-03-26T12:07:14.636Z'
---

# 发送文件

使用 `ParcelFileDescriptor` 类型，可以在 Binder 客户端/服务器之间发送文件：

**birthday_service/aidl/com/example/birthdayservice/IBirthdayService.aidl**：

```java
interface IBirthdayService {
{{#include ../birthday_service/aidl/com/example/birthdayservice/IBirthdayService.aidl:with_file}}
}
```

**birthday_service/src/client.rs**：

```rust,ignore
fn main() {
    binder::ProcessState::start_thread_pool();
    let service = connect().expect("Failed to connect to BirthdayService");
{{#include ../birthday_service/src/client.rs:wish_with_file}}
}
```

**birthday_service/src/lib.rs**：

```rust,ignore
impl IBirthdayService for BirthdayService {
{{#include ../birthday_service/src/lib.rs:wishFromFile}}
}
```

<details>

- `ParcelFileDescriptor` 包装了一个 `OwnedFd`，因此可以从 `File`
  （或任何其他包装了 `OwnedFd` 的类型）创建，并且可以用来在另一侧创建一个新的
  `File` 句柄。
- 其他类型的文件描述符也可以被包装和发送，例如 TCP、UDP 和
  UNIX 套接字。

</details>
