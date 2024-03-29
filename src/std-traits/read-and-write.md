---
minutes: 10
translated_at: '2024-03-26T10:07:22.093Z'
---

# `Read` 和 `Write`

使用 [`Read`][1] 和 [`BufRead`][2]，你可以对 `u8` 源进行抽象：

```rust,editable
use std::io::{BufRead, BufReader, Read, Result};

fn count_lines<R: Read>(reader: R) -> usize {
    let buf_reader = BufReader::new(reader);
    buf_reader.lines().count()
}

fn main() -> Result<()> {
    let slice: &[u8] = b"foo\nbar\nbaz\n";
    println!("slice 中的行数：{}", count_lines(slice));

    let file = std::fs::File::open(std::env::current_exe()?)?;
    println!("文件中的行数：{}", count_lines(file));
    Ok(())
}
```

类似地，[`Write`][3] 允许你对 `u8` 汇进行抽象：

```rust,editable
use std::io::{Result, Write};

fn log<W: Write>(writer: &mut W, msg: &str) -> Result<()> {
    writer.write_all(msg.as_bytes())?;
    writer.write_all("\n".as_bytes())
}

fn main() -> Result<()> {
    let mut buffer = Vec::new();
    log(&mut buffer, "Hello")?;
    log(&mut buffer, "World")?;
    println!("已记录：{:?}", buffer);
    Ok(())
}
```

[1]: https://doc.rust-lang.org/std/io/trait.Read.html
[2]: https://doc.rust-lang.org/std/io/trait.BufRead.html
[3]: https://doc.rust-lang.org/std/io/trait.Write.html
