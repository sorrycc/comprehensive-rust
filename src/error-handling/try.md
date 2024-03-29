---
minutes: 5
translated_at: '2024-03-26T10:57:52.055Z'
---

# Try 操作符

像连接拒绝或文件未找到这样的运行时错误会使用 `Result` 类型来处理，但对每次调用都匹配这个类型可能会很繁琐。try 操作符 `?` 用于将错误返回给调用者。它让你能将常见的

```rust,ignore
match some_expression {
    Ok(value) => value,
    Err(err) => return Err(err),
}
```

转变为更简单的

```rust,ignore
some_expression?
```

我们可以用它来简化我们的错误处理代码：

```rust,editable
use std::io::Read;
use std::{fs, io};

fn read_username(path: &str) -> Result<String, io::Error> {
    let username_file_result = fs::File::open(path);
    let mut username_file = match username_file_result {
        Ok(file) => file,
        Err(err) => return Err(err),
    };

    let mut username = String::new();
    match username_file.read_to_string(&mut username) {
        Ok(_) => Ok(username),
        Err(err) => Err(err),
    }
}

fn main() {
    //fs::write("config.dat", "alice").unwrap();
    let username = read_username("config.dat");
    println!("username or error: {username:?}");
}
```

<details>

使用 `?` 简化 `read_username` 函数。

关键点：

- `username` 变量可以是 `Ok(string)` 或 `Err(error)`。
- 使用 `fs::write` 调用来测试不同的场景：无文件、空文件、带用户名的文件。
- 注意 `main` 可以返回 `Result<(), E>` 只要它实现了 `std::process::Termination`。在实践中，这意味着 `E` 实现了 `Debug`。可执行文件会在错误时打印 `Err` 变体并返回非零退出状态。

</details>
