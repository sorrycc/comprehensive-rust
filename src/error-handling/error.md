---
minutes: 5
translated_at: '2024-03-26T11:00:58.421Z'
---

# 动态错误类型

有时我们希望允许返回任何类型的错误，而不需要编写涵盖所有不同可能性的枚举。`std::error::Error` 特征使得创建一个可以包含任何错误的特征对象变得简单。

```rust,editable
use std::error::Error;
use std::fs;
use std::io::Read;

fn read_count(path: &str) -> Result<i32, Box<dyn Error>> {
    let mut count_str = String::new();
    fs::File::open(path)?.read_to_string(&mut count_str)?;
    let count: i32 = count_str.parse()?;
    Ok(count)
}

fn main() {
    fs::write("count.dat", "1i3").unwrap();
    match read_count("count.dat") {
        Ok(count) => println!("计数: {count}"),
        Err(err) => println!("错误: {err}"),
    }
}
```

<details>

`read_count` 函数可以返回 `std::io::Error`（来自文件操作）或 `std::num::ParseIntError`（来自 `String::parse`）。

封箱错误可以节省代码，但放弃了在程序中清晰地处理不同错误案例的能力。因此，通常不建议在库的公共 API 中使用 `Box<dyn Error>`，但如果你只是想在某处显示错误消息，它可能是一个好选择。

当定义自定义错误类型时，请确保实现 `std::error::Error` 特征，以便它可以被封箱。但是，如果您需要支持 `no_std` 属性，请记住 `std::error::Error` 特征目前仅在 [nightly](https://github.com/rust-lang/rust/issues/103765) 中与 `no_std` 兼容。

</details>
