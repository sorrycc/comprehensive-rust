---
minutes: 5
translated_at: '2024-03-26T10:58:26.081Z'
---

# 尝试转换

有效展开 `?` 的方式比先前指出的要稍微复杂一些：

```rust,ignore
expression?
```

工作原理相同于

```rust,ignore
match expression {
    Ok(value) => value,
    Err(err)  => return Err(From::from(err)),
}
```

这里的 `From::from` 调用意味着我们尝试将错误类型转换成函数返回的类型。这使得将错误封装进更高层的错误变得容易。

## 示例

```rust,editable
use std::error::Error;
use std::fmt::{self, Display, Formatter};
use std::fs::File;
use std::io::{self, Read};

#[derive(Debug)]
enum ReadUsernameError {
    IoError(io::Error),
    EmptyUsername(String),
}

impl Error for ReadUsernameError {}

impl Display for ReadUsernameError {
    fn fmt(&self, f: &mut Formatter) -> fmt::Result {
        match self {
            Self::IoError(e) => write!(f, "IO 错误：{e}"),
            Self::EmptyUsername(path) => write!(f, "在 {path} 中找不到用户名"),
        }
    }
}

impl From<io::Error> for ReadUsernameError {
    fn from(err: io::Error) -> Self {
        Self::IoError(err)
    }
}

fn read_username(path: &str) -> Result<String, ReadUsernameError> {
    let mut username = String::with_capacity(100);
    File::open(path)?.read_to_string(&mut username)?;
    if username.is_empty() {
        return Err(ReadUsernameError::EmptyUsername(String::from(path)));
    }
    Ok(username)
}

fn main() {
    // fs::write("config.dat", "").unwrap();
    let username = read_username("config.dat");
    println!("用户名或错误：{username:?}");
}
```

<details>

`?` 操作符必须返回与函数的返回类型兼容的值。对于 `Result`，这意味着错误类型必须兼容。一个返回 `Result<T, ErrorOuter>` 的函数只能在类型为 `Result<U, ErrorInner>` 的值上使用 `?`，如果 `ErrorOuter` 和 `ErrorInner` 是相同的类型，或者 `ErrorOuter` 实现了 `From<ErrorInner>`。

一种常见的替代 `From` 实现的策略是使用 `Result::map_err`，尤其是

当转换只在一个地方发生时。

对于 `Option` 并没有兼容性要求。返回 `Option<T>` 的函数可以对任意 `T` 和 `U` 类型的 `Option<U>` 使用 `?` 操作符。

返回 `Result` 的函数不能在 `Option` 上使用 `?`，反之亦然。然而，`Option::ok_or` 可以将 `Option` 转换为 `Result`，而 `Result::ok` 则可以将 `Result` 转化为 `Option`。

</details>
