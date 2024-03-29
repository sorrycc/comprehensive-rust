---
minutes: 2
translated_at: '2024-03-26T10:36:52.723Z'
---

# 克隆

有时候你_想要_复制一个值。“Clone” 特性就是为了完成这个目的。

```rust,editable
#[derive(Default)]
struct Backends {
    hostnames: Vec<String>,
    weights: Vec<f64>,
}

impl Backends {
    fn set_hostnames(&mut self, hostnames: &Vec<String>) {
        self.hostnames = hostnames.clone();
        self.weights = hostnames.iter().map(|_| 1.0).collect();
    }
}
```

<details>

“Clone”的理念是为了让人更容易发现堆分配是在哪里发生的。寻找 `.clone()` 和一些其他的方法，比如 `Vec::new` 或 `Box::new`。

通常会通过“克隆出路”来解决借用检查器的问题，然后回过头来尝试优化这些克隆。

</details>
