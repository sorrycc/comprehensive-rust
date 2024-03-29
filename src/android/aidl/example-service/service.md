---
translated_at: '2024-03-26T12:08:00.688Z'
---

# 服务实现

我们现在可以实现 AIDL 服务了：

_birthday_service/src/lib.rs_：

```rust,ignore
use com_example_birthdayservice::aidl::com::example::birthdayservice::IBirthdayService::IBirthdayService;
use com_example_birthdayservice::binder;

{{#include ../birthday_service/src/lib.rs:IBirthdayService}}
}
```

_birthday_service/Android.bp_：

```javascript
{{#include ../birthday_service/Android.bp:libbirthdayservice}}
```

<details>

- 指出生成的 `IBirthdayService` 特性的路径，并解释每个段落的必要性。
- 待办：`binder::Interface` 特性做什么？有方法要重写吗？源代码在哪里？

</details>
