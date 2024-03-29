---
minutes: 3
translated_at: '2024-03-26T10:27:19.706Z'
---

# 模块

我们已经看到 `impl` 块是如何让我们将函数命名空间设置到一个类型上的。

同样地，`mod` 让我们能够为类型和函数设置命名空间：

```rust,editable
mod foo {
    pub fn do_something() {
        println!("在 foo 模块中");
    }
}

mod bar {
    pub fn do_something() {
        println!("在 bar 模块中");
    }
}

fn main() {
    foo::do_something();
    bar::do_something();
}
```

<details>

- 包提供功能，并包含一个 `Cargo.toml` 文件，描述如何构建一个或多个 crate 的捆绑。
- Crates 是模块的树结构，其中二进制 crate 创建一个可执行文件，库 crate 编译成一个库。
- 模块定义组织、范围，并且是本节的重点。

</details>
