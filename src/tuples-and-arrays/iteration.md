---
minutes: 3
translated_at: '2024-03-26T09:59:31.527Z'
---

# 数组迭代

`for` 语句支持迭代数组（但不支持元组）。

```rust,editable
fn main() {
    let primes = [2, 3, 5, 7, 11, 13, 17, 19];
    for prime in primes {
        for i in 2..prime {
            assert_ne!(prime % i, 0);
        }
    }
}
```

<details>

这个功能使用了 `IntoIterator` 特征，但我们还没有覆盖到这一点。

这里新出现的宏是 `assert_ne!`。还有 `assert_eq!` 和 `assert!` 这些宏。这些都是始终会检查的，而像 `debug_assert!` 这样的仅在 debug 模式下会检查的变体，在发布构建中会编译成无内容。

</details>
