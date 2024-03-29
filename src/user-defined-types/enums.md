---
minutes: 5
translated_at: '2024-03-26T09:49:39.822Z'
---

# 枚举类型

`enum` 关键字允许创建一个拥有几种不同变体的类型：

```rust,editable
#[derive(Debug)]
enum Direction {
    Left,
    Right,
}

#[derive(Debug)]
enum PlayerMove {
    Pass,                        // 简单变体
    Run(Direction),              // 元组变体
    Teleport { x: u32, y: u32 }, // 结构体变体
}

fn main() {
    let m: PlayerMove = PlayerMove::Run(Direction::Left);
    println!("On this turn: {:?}", m);
}
```

<details>

关键点：

- 枚举类型允许你将一组值收集在一个类型下。
- `Direction` 是一个有变体的类型。`Direction` 有两个值：`Direction::Left` 和 `Direction::Right`。
- `PlayerMove` 是一个有三种变体的类型。除了负载外，Rust 会存储一个区分值，以便在运行时知道 `PlayerMove` 值中是哪个变体。
- 这可能是比较结构体和枚举的好时机：
  - 在两者中，你可以有没有字段的简单版本（单元结构体）或者有不同类型字段的版本（变体负载）。
  - 你甚至可以用不同的结构体实现枚举的不同变体，但那样它们就不会像定义在同一个枚举中那样是相同类型了。
- Rust 使用最小的空间来存储区分值。
  - 如果必要，它会存储最小所需大小的整数
  - 如果允许的变体值没有覆盖所有位模式，则它会使用无效位模式来编码区分值（"利基优化"）。例如，`Option<&u8>` 存储一个指向整数的指针或 `NULL` 以表示 `None` 变体。
  - 如果需要，你可以控制区分值（例如，为了与 C 兼容）：

    <!-- mdbook-xgettext: skip -->
    ```rust,editable
    #[repr(u32)]
    enum Bar {
        A, // 0
        B = 10000,
        C, // 10001
    }

    fn main() {
        println!("A: {}", Bar::A as u32);
        println!("B: {}", Bar::B as u32);
        println!("C: {}", Bar::C as u32);
    }
    ```

```markdown
如果没有 `repr` ，辨别类型占用 2 个字节，因为 10001 适合 2 个字节。

## 更多探索

Rust 有几种优化方式，可以让枚举占用更少的空间。

- 空指针优化：对于[某些类型](https://doc.rust-lang.org/std/option/#representation)，Rust 保证 `size_of::<T>()` 等于 `size_of::<Option<T>>()`。

  如果你想展示位表示在实践中_可能_是什么样子的示例代码。需要注意的是，编译器不保证这种表示，因此这完全不安全。

  <!-- mdbook-xgettext: skip -->
  ```rust,editable
  use std::mem::transmute;

  macro_rules! dbg_bits {
      ($e:expr, $bit_type:ty) => {
          println!("- {}: {:#x}", stringify!($e), transmute::<_, $bit_type>($e));
      };
  }

  fn main() {
      unsafe {
          println!("bool:");
          dbg_bits!(false, u8);
          dbg_bits!(true, u8);

          println!("Option<bool>:");
          dbg_bits!(None::<bool>, u8);
          dbg_bits!(Some(false), u8);
          dbg_bits!(Some(true), u8);

          println!("Option<Option<bool>>:");
          dbg_bits!(Some(Some(false)), u8);
          dbg_bits!(Some(Some(true)), u8);
          dbg_bits!(Some(None::<bool>), u8);
          dbg_bits!(None::<Option<bool>>, u8);

          println!("Option<&i32>:");
          dbg_bits!(None::<&i32>, usize);
          dbg_bits!(Some(&0i32), usize);
      }
  }
  ```

</details>
```
