---
minutes: 5
translated_at: '2024-03-26T10:25:19.909Z'
---

# 可见性

模块是一个隐私边界：

- 模块项默认是私有的（隐藏实现细节）。
- 父项和兄弟项总是可见的。
- 换句话说，如果某个项在模块 `foo` 中可见，那么它在 `foo` 的所有后代中都是可见的。

```rust,editable
mod outer {
    fn private() {
        println!("outer::private");
    }

    pub fn public() {
        println!("outer::public");
    }

    mod inner {
        fn private() {
            println!("outer::inner::private");
        }

        pub fn public() {
            println!("outer::inner::public");
            super::private();
        }
    }
}

fn main() {
    outer::public();
}
```

<details>

- 使用 `pub` 关键字使模块公开。

另外，有高级的 `pub(...)` 指定符用于限制公开可见性的范围。

- 参见 [Rust 参考](https://doc.rust-lang.org/reference/visibility-and-privacy.html#pubin-path-pubcrate-pubsuper-and-pubself)。
- 配置 `pub(crate)` 可见性是一个常见模式。
- 不那么常见的，你可以对特定路径授权可见性。
- 无论如何，必须授予一个祖先模块（及其所有后代）可见性。

</details>
