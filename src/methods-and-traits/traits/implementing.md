---
translated_at: '2024-03-26T10:31:54.497Z'
---

# 实现 Traits

```rust,editable
trait Pet {
    fn talk(&self) -> String;

    fn greet(&self) {
        println!("Oh you're a cutie! What's your name? {}", self.talk());
    }
}

struct Dog {
    name: String,
    age: i8,
}

impl Pet for Dog {
    fn talk(&self) -> String {
        format!("Woof, my name is {}!", self.name)
    }
}

fn main() {
    let fido = Dog { name: String::from("Fido"), age: 5 };
    fido.greet();
}
```

<details>

- 要为 `Type` 实现 `Trait`，你需要使用一个 `impl Trait for Type { .. }` 块。

- 与 Go 接口不同，仅拥有匹配的方法是不够的：一个具有 `talk()` 方法的 `Cat` 类型不会自动满足 `Pet`，除非它在一个 `impl Pet` 块中。

- Traits 可能提供一些方法的默认实现。默认实现可以依赖于 trait 的所有方法。在这个例子中，`greet` 被提供，并依赖于 `talk`。

</details>
