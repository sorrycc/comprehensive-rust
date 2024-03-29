---
minutes: 10
translated_at: '2024-03-26T10:22:58.785Z'
---

# 让控制流转

Rust 有一些与其他语言不同的控制流结构。它们用于模式匹配：

- `if let` 表达式
- `while let` 表达式
- `match` 表达式

# `if let` 表达式

[`if let` 表达式](https://doc.rust-lang.org/reference/expressions/if-expr.html#if-let-expressions) 允许您根据值是否与模式匹配来执行不同的代码：

```rust,editable
fn sleep_for(secs: f32) {
    let dur = if let Ok(dur) = std::time::Duration::try_from_secs_f32(secs) {
        dur
    } else {
        std::time::Duration::from_millis(500)
    };
    std::thread::sleep(dur);
    println!("睡眠了 {:?}", dur);
}

fn main() {
    sleep_for(-10.0);
    sleep_for(0.8);
}
```

# `let else` 表达式

对于匹配模式并返回函数的常见情况，请使用 [`let else`](https://doc.rust-lang.org/rust-by-example/flow_control/let_else.html)。"else" 情况必须发散（`return`、`break` 或 panic——只是不会落在代码块的末端）。

```rust,editable
fn hex_or_die_trying(maybe_string: Option<String>) -> Result<u32, String> {
    let s = if let Some(s) = maybe_string {
        s
    } else {
        return Err(String::from("得到 None"));
    };

    let first_byte_char = if let Some(first_byte_char) = s.chars().next() {
        first_byte_char
    } else {
        return Err(String::from("得到空字符串"));
    };

    if let Some(digit) = first_byte_char.to_digit(16) {
        Ok(digit)
    } else {
        Err(String::from("不是十六进制数字"))
    }
}

fn main() {
    println!("结果: {:?}", hex_or_die_trying(Some(String::from("foo"))));
}
```

像 `if let` 一样，还有一个 [`while let`](https://doc.rust-lang.org/reference/expressions/loop-expr.html#predicate-pattern-loops) 变体，它会反复将值与模式进行测试：

<!-- mdbook-xgettext: skip -->

```rust,editable
fn main() {
    let mut name = String::from("Comprehensive Rust 🦀");
    while let Some(c) = name.pop() {
        println!("字符: {c}");
    }
    // （有更高效的方法来反转字符串！）
}
```

<details>

## if-let

- 与 `match` 不同，`if let` 不需要覆盖所有分支。这使得它比 `match` 更简洁。
- 常见用法是在使用 `Option` 时处理 `Some` 值。
- 与 `match` 不同的是，`if let` 不支持模式匹配的守卫子句。

## let-else

如所示，`if-let` 可能会堆积。`let-else` 结构支持展平这些嵌套代码。为学生们改写那个笨拙的版本，让他们看到转换后的效果。

改写后的版本是：

```rust
fn hex_or_die_trying(maybe_string: Option<String>) -> Result<u32, String> {
    let Some(s) = maybe_string else {
        return Err(String::from("got None"));
    };

    let Some(first_byte_char) = s.chars().next() else {
        return Err(String::from("got empty string"));
    };

    let Some(digit) = first_byte_char.to_digit(16) else {
        return Err(String::from("not a hex digit"));
    };

    return Ok(digit);
}
```

# while-let

- 指出 `while let` 循环将持续进行，只要值与模式匹配。
- 你可以将 `while let` 循环重写为一个无限循环，使用一个 `if` 语句在 `name.pop()` 没有值可解包时中断循环。`while let` 为上述场景提供了语法糖。

</details>
