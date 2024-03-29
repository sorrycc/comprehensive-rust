---
minutes: 10
translated_at: '2024-03-26T10:04:46.354Z'
---

# 结果

`Result` 类型与 `Option` 相似，但用于指示操作的成功或失败，每种情况都有不同的类型。这类似于在表达式练习中定义的 `Res`，但是它是泛型的：`Result<T, E>`，其中 `T` 用在 `Ok` 变体中，而 `E` 出现在 `Err` 变体中。

```rust,editable
use std::fs::File;
use std::io::Read;

fn main() {
    let file: Result<File, std::io::Error> = File::open("diary.txt");
    match file {
        Ok(mut file) => {
            let mut contents = String::new();
            if let Ok(bytes) = file.read_to_string(&mut contents) {
                println!("亲爱的日记：{contents}（{bytes} 字节）");
            } else {
                println!("无法读取文件内容");
            }
        }
        Err(err) => {
            println!("无法打开日记本：{err}");
        }
    }
}
```

<details>

- 就像 `Option` 一样，成功的值存在于 `Result` 内部，迫使开发人员显式提取它。这鼓励错误检查。在错误绝不应该发生的情况下，可以调用 `unwrap()` 或 `expect()`，这也是开发人员意图的一个标志。
- 建议阅读 `Result` 文档。虽然不是在课程期间，但值得一提。它包含许多便利的方法和函数，帮助进行函数式编程。
- `Result` 是实现错误处理的标准类型，我们将在第 4 天看到这一点。

</details>
