---
minutes: 8
translated_at: '2024-03-26T10:24:34.757Z'
---

# 解构

像元组一样，结构体和枚举也可以通过匹配来进行解构：

## 结构体

```rust,editable
{{#include ../../third_party/rust-by-example/destructuring-structs.rs}}
```

## 枚举

模式也可以用来将变量绑定到值的部分。这是检查类型结构的方式。我们从一个简单的 `enum` 类型开始：

```rust,editable
enum Result {
    Ok(i32),
    Err(String),
}

fn divide_in_two(n: i32) -> Result {
    if n % 2 == 0 {
        Result::Ok(n / 2)
    } else {
        Result::Err(format!("无法将 {n} 平分为两个相等的部分"))
    }
}

fn main() {
    let n = 100;
    match divide_in_two(n) {
        Result::Ok(half) => println!("{n} 平分为两部分是 {half}"),
        Result::Err(msg) => println!("抱歉，发生了错误：{msg}"),
    }
}
```

在这里，我们使用分支来 _解构_ `Result` 值。在第一个分支中，`half` 绑定到 `Ok` 变体内的值。在第二个分支中，`msg` 绑定到错误消息。

<details>

# 结构体

- 更改 `foo` 中的字面值，使其与其他模式匹配。
- 向 `Foo` 添加一个新字段，并根据需要对模式进行更改。
- 捕获与常量表达式之间的区别可能难以辨认。尝试将第二个分支中的 `2` 改为一个变量，并发现它微妙地无法工作。将其更改为 `const` 然后看它再次工作。

# 枚举

关键点：

- `if`/`else` 表达式返回一个稍后将使用 `match` 解包的枚举。
- 可以尝试向枚举定义中添加第三个变体，并显示运行代码时的错误。指出代码现在哪里是不详尽的，以及编译器如何尝试给你提示。
- 枚举变体中的值只有在模式匹配后才能被访问。
- 演示当搜索不详尽时会发生什么。注意 Rust 编译器确认所有情况都已处理的优势。
- 将 `divide_in_two` 的结果保存在 `result` 变量中并在其中 `match`

```markdown
一个循环。这段代码无法编译，因为在匹配时 `msg` 被消耗了。要解决这个问题，
应该匹配 `&result` 而不是 `result`。这将会使 `msg` 成为一个引用，因此它不会被消耗。
这种 ["匹配优雅"](https://rust-lang.github.io/rfcs/2005-match-ergonomics.html)
在 Rust 2018 中出现。如果你想要支持更旧版本的 Rust，那么在模式中替换 `msg` 为
`ref msg`。

</details>
```
