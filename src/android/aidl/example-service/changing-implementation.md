---
translated_at: '2024-03-26T12:10:59.062Z'
---

# 更新客户端和服务

更新客户端和服务器代码以适应新的 API。

_birthday_service/src/lib.rs_：

```rust,ignore
impl IBirthdayService for BirthdayService {
    fn wishHappyBirthday(
        &self,
        name: &str,
        years: i32,
        text: &[String],
    ) -> binder::Result<String> {
        let mut msg = format!(
            "Happy Birthday {name}, congratulations with the {years} years!",
        );

        for line in text {
            msg.push('\n');
            msg.push_str(line);
        }

        Ok(msg)
    }
}
```

_birthday_service/src/client.rs_：

```rust,ignore
let msg = service.wishHappyBirthday(
    &name,
    years,
    &[
        String::from("Habby birfday to yuuuuu"),
        String::from("And also: many more"),
    ],
)?;
```

<details>

- TODO: 将代码片段移入项目文件中，这样才会真正构建？

</details>
