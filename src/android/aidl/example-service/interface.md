---
translated_at: '2024-03-26T12:09:07.359Z'
---

# AIDL 接口

你可以使用 AIDL 接口声明你的服务 API：

_birthday_service/aidl/com/example/birthdayservice/IBirthdayService.aidl_：

```java
{{#include ../birthday_service/aidl/com/example/birthdayservice/IBirthdayService.aidl:IBirthdayService}}
}
```

_birthday_service/aidl/Android.bp_：

```javascript
{{#include ../birthday_service/aidl/Android.bp}}
```

<details>

- 注意 `aidl/` 目录下的目录结构需要与 AIDL 文件中使用的包名匹配，即包名是
  `com.example.birthdayservice`，文件位于
  `aidl/com/example/IBirthdayService.aidl`。

</details>
