---
translated_at: '2024-03-26T11:04:28.836Z'
---

# 作用域与遮蔽

一个变量的作用域限于封闭的块。

你可以遮蔽变量，包括来自外部作用域的变量和同一作用域内的变量：

```rust,editable
fn main() {
    let a = 10;
    println!("before: {a}");
    {
        let a = "hello";
        println!("inner scope: {a}");

        let a = true;
        println!("shadowed in inner scope: {a}");
    }

    println!("after: {a}");
}
```

<details>

- 通过在最后一个示例的内部块中添加一个 `b`，然后尝试在该块外部访问它，展示一个变量的作用域是受限的。
- 遮蔽不同于变异，因为遮蔽后，两个变量的内存位置同时存在。它们在相同的名称下可用，这取决于你在代码中的使用位置。
- 一个遮蔽变量可以有不同的类型。
- 虽然遮蔽起初看起来比较晦涩，但是在执行 `.unwrap()` 后持有值时很方便。

</details>
