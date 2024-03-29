---
minutes: 5
translated_at: '2024-03-26T10:58:59.795Z'
---

# `thiserror` 和 `anyhow`

[`thiserror`](https://docs.rs/thiserror/) 和 [`anyhow`](https://docs.rs/anyhow/) 是两个用于简化错误处理的广泛使用的库。

- `thiserror` 经常用在库中，用于创建实现 `From<T>` 的自定义错误类型。
- `anyhow` 经常被应用程序用来帮助函数中的错误处理，包括为你的错误添加上下文信息。

```rust,editable,compile_fail
use anyhow::{bail, Context, Result};
use std::fs;
use std::io::Read;
use thiserror::Error;

#[derive(Clone, Debug, Eq, Error, PartialEq)]
#[error("在 {0} 中找不到用户名")]
struct EmptyUsernameError(String);

fn read_username(path: &str) -> Result<String> {
    let mut username = String::with_capacity(100);
    fs::File::open(path)
        .with_context(|| format!("打开 {path} 失败"))?
        .read_to_string(&mut username)
        .context("读取失败")?;
    if username.is_empty() {
        bail!(EmptyUsernameError(path.to_string()));
    }
    Ok(username)
}

fn main() {
    //fs::write("config.dat", "").unwrap();
    match read_username("config.dat") {
        Ok(username) => println!("用户名：{username}"),
        Err(err) => println!("错误：{err:?}"),
    }
}
```

<details>

## `thiserror`

- `Error` 导出宏由 `thiserror` 提供，并具有许多有用的属性，以帮助以紧凑的方式定义错误类型。
- `std::error::Error` 特性会自动实现。
- 从 `#[error]` 中获取的信息被用来派生 `Display` 特性。

## `anyhow`

- `anyhow::Error` 本质上是 `Box<dyn Error>` 的包装器。因此，它通常不是库的公共 API 的好选择，但在应用中被广泛使用。
- `anyhow::Result<V>` 是 `Result<V, anyhow::Error>` 的类型别名。
- 其内部的实际错误类型可以被提取出来进行检查。
- `anyhow::Result<T>` 提供的功能对 Go 开发者来说可能会感觉熟悉，因为它提供了与 Go 中的 `(T, error)` 类似的使用模式和舒适度。
- `anyhow::Context` 是为标准 `Result` 和

`Option` 类型。 `use anyhow::Context` 是必需的，以便在这些类型上启用 `.context()` 和
`.with_context()`。

</details>
