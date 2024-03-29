---
minutes: 8
translated_at: '2024-03-26T10:15:33.504Z'
---

# `Box<T>`

[`Box`](https://doc.rust-lang.org/std/boxed/struct.Box.html) 是指向堆上数据的所有权指针：

```rust,editable
fn main() {
    let five = Box::new(5);
    println!("five: {}", *five);
}
```

```bob
 堆栈                      堆
.- - - - - - -.     .- - - - - - -.
:             :     :             :
:    five     :     :             :
:   +-----+   :     :   +-----+   :
:   | o---|---+-----+-->|  5  |   :
:   +-----+   :     :   +-----+   :
:             :     :             :
:             :     :             :
`- - - - - - -'     `- - - - - - -'
```

`Box<T>` 实现了 `Deref<Target = T>`，这意味着你可以
[直接在 `Box<T>` 上调用 `T` 的方法](https://doc.rust-lang.org/std/ops/trait.Deref.html#on-deref-coercion)。

递归数据类型或动态大小的数据类型需要使用 `Box`：

```rust,editable
#[derive(Debug)]
enum List<T> {
    /// 非空列表：第一个元素和列表的剩余部分。
    Element(T, Box<List<T>>),
    /// 空列表。
    Nil,
}

fn main() {
    let list: List<i32> =
        List::Element(1, Box::new(List::Element(2, Box::new(List::Nil))));
    println!("{list:?}");
}
```

```bob
 堆栈                                 堆
.- - - - - - - - - - - - - - .     .- - - - - - - - - - - - - - - - - - - - - - - - -.
:                            :     :                                                 :
:    list                    :     :                                                 :
:   +---------+----+----+    :     :    +---------+----+----+    +------+----+----+  :
:   | Element | 1  | o--+----+-----+--->| Element | 2  | o--+--->| Nil  | // | // |  :
:   +---------+----+----+    :     :    +---------+----+----+    +------+----+----+  :
:                            :     :                                                 :
:                            :     :                                                 :
'- - - - - - - - - - - - - - '     '- - - - - - - - - - - - - - - - - - - - - - - - -'
```

<details>

- `Box` 类似于 C++ 中的 `std::unique_ptr`，不过它保证不会是空指针。
- 当你需要时，`Box` 可以非常有用：
  - 有一个在编译时大小未知的类型，但 Rust 编译器想要知道一个确切的大小。
  - 想要转移大量数据的所有权。为了避免在栈上复制大量数据，可以使用 `Box` 在堆上存储数据，这样只需要移动指针。

- 如果不使用 `Box` 并尝试直接在 `List` 中嵌入 `List`，编译器将无法为内存中的结构计算出固定大小（`List` 会是无限大小）。

- `Box` 解决了这个问题，因为它的大小与常规指针相同，只是在堆中指向 `List` 的下一个元素。

- 移除 `List` 定义中的 `Box` 并展示编译器错误。我们会得到消息 "递归无间接"，因为对于数据递归，我们必须使用间接手段，比如某种 `Box` 或引用，而不是直接存储值。

# 更多探索

## 别致的优化

```rust,editable
#[derive(Debug)]
enum List<T> {
    Element(T, Box<List<T>>),
    Nil,
}

fn main() {
    let list: List<i32> =
        List::Element(1, Box::new(List::Element(2, Box::new(List::Nil))));
    println!("{list:?}");
}
```

`Box` 不能是空的，所以指针总是有效且非空。这允许编译器优化内存布局：

```bob
 栈                             堆
.- - - - - - - - - - - - - - .     .- - - - - - - - - - - - - -.
:                            :     :                           :
:    list                    :     :                           :
:   +---------+----+----+    :     :    +---------+----+----+  :
:   | Element | 1  | o--+----+-----+--->| Element | 2  | // |  :
:   +---------+----+----+    :     :    +---------+----+----+  :
:                            :     :                           :
:                            :     :                           :
'- - - - - - - - - - - - - - '     '- - - - - - - - - - - - - -'
```

</details>
