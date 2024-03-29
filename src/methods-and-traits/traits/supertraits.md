---
translated_at: '2024-03-26T10:31:35.389Z'
---

# 超级特性

一个特性可以要求实现它的类型也实现其他特性，这称为 _超级特性_。这里，任何实现了 `Pet` 的类型必须也实现 `Animal`。

```rust,editable
trait Animal {
    fn leg_count(&self) -> u32;
}

trait Pet: Animal {
    fn name(&self) -> String;
}

struct Dog(String);

impl Animal for Dog {
    fn leg_count(&self) -> u32 {
        4
    }
}

impl Pet for Dog {
    fn name(&self) -> String {
        self.0.clone()
    }
}

fn main() {
    let puppy = Dog(String::from("Rex"));
    println!("{} 有 {} 条腿", puppy.name(), puppy.leg_count());
}
```

<details>

这有时被称为“特性继承”，但学生们不应该期望这像 OO 继承那样表现。它只是对特性的实现提出了额外的要求。

<details>
