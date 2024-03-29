---
minutes: 8
translated_at: '2024-03-26T10:29:50.773Z'
---

# 方法

Rust 允许你将函数与你的新类型关联起来。你可以通过一个 `impl` 块来做到这一点：

```rust,editable
#[derive(Debug)]
struct Race {
    name: String,
    laps: Vec<i32>,
}

impl Race {
    // 没有接收者，一个静态方法
    fn new(name: &str) -> Self {
        Self { name: String::from(name), laps: Vec::new() }
    }

    // 对 self 的独占借用读写访问
    fn add_lap(&mut self, lap: i32) {
        self.laps.push(lap);
    }

    // 对 self 的共享和只读借用访问
    fn print_laps(&self) {
        println!("为 {} 记录了 {} 圈：", self.name, self.laps.len());
        for (idx, lap) in self.laps.iter().enumerate() {
            println!("第 {idx} 圈：{lap} 秒");
        }
    }

    // 对 self 的独占所有权
    fn finish(self) {
        let total: i32 = self.laps.iter().sum();
        println!("赛事 {} 结束，总圈数时间：{}", self.name, total);
    }
}

fn main() {
    let mut race = Race::new("摩纳哥大奖赛");
    race.add_lap(70);
    race.add_lap(68);
    race.print_laps();
    race.add_lap(71);
    race.print_laps();
    race.finish();
    // race.add_lap(42);
}
```

`self` 参数指定了方法作用的 “接收者” - 方法作用于的对象。
对于方法有几种常见的接收者：

- `&self`：使用共享且不可变的引用，从调用者那里借用对象。之后可以再次使用该对象。
- `&mut self`：使用独特且可变的引用，从调用者那里借用对象。之后可以再次使用该对象。
- `self`：获取对象的所有权并将其从调用者处移走。方法成为对象的所有者。当方法返回时，除非显式转移了所有权，否则对象将被丢弃（释放）。完全所有权并不自动意味着可变性。
- `mut self`：与上述相同，但方法可以修改对象。
- 无接收者：这变成了结构体上的一个静态方法。通常用于创建构造函数，按惯例这些函数被称为 `new`。

<details>

关键点：

- 将方法与函数进行比较引入方法的做法有助于理解。
  - 方法是在类型（如结构或枚举）的实例上调用的，第一个参数表示该实例为 `self`。
  - 开发者可能会选择使用方法来利用方法接收器语法，并帮助使代码更加有组织。通过使用方法，我们可以将所有的实现代码放在一个可预测的地方。
- 指出关键字 `self` 的使用，一个方法接收器。
  - 展示它是 `self: Self` 的简写形式，并且可能展示如何使用结构体名称。
  - 解释 `Self` 是 `impl` 块中类型的类型别名，并且可以在块的其他地方使用。
  - 注意如何像其他结构体一样使用 `self`，并且可以使用点符号来引用单个字段。
  - 这可能是展示 `&self` 与 `self` 不同的好时机，尝试运行 `finish` 两次。
  - 除了 `self` 的变体，还有允许作为接收器类型的[特殊包装类型](https://doc.rust-lang.org/reference/special-types-and-traits.html)，例如 `Box<Self>`。

</details>
