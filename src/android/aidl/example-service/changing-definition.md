---
translated_at: '2024-03-26T12:11:20.362Z'
---

# 更改 API

让我们扩展 API，增加更多功能：我们希望允许客户指定一系列生日卡片上的文字：

```java
package com.example.birthdayservice;

/** 生日服务接口。*/
interface IBirthdayService {
    /** 生成一个生日快乐消息。*/
    String wishHappyBirthday(String name, int years, in String[] text);
}
```

这导致了 `IBirthdayService` 特征定义的更新：

```rust,ignore
trait IBirthdayService {
    fn wishHappyBirthday(
        &self,
        name: &str,
        years: i32,
        text: &[String],
    ) -> binder::Result<String>;
}
```

<details>

- 注意，AIDL 定义中的 `String[]` 如何被翻译为 Rust 中的 `&[String]`，即在生成的绑定中尽可能使用惯用的 Rust 类型：
  - `in` 数组参数被翻译为切片。
  - `out` 和 `inout` 参数被翻译为 `&mut Vec<T>`。
  - 返回值被翻译为返回一个 `Vec<T>`。

</details>
