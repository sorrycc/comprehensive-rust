---
minutes: 5
translated_at: '2024-03-26T10:33:27.318Z'
---

# 程序内存回顾

程序分配内存的两种方式：

- 栈：连续的内存区域用于局部变量。
  - 值的大小在编译时已知固定。
  - 极快：只需移动栈指针。
  - 容易管理：遵循函数调用。
  - 极佳的内存局部性。

- 堆：用于函数调用外的值存储。
  - 值的大小在运行时决定，具有动态性。
  - 比栈稍慢：需要一些簿记工作。
  - 无内存局部性保证。

## 示例

创建一个 `String` 会将固定大小的元数据放在栈上，而动态大小的数据（实际的字符串）放在堆上：

```rust,editable
fn main() {
    let s1 = String::from("Hello");
}
```

```bob
 栈
.- - - - - - - - - - - - - -.      堆
:                           :     .- - - - - - - - - - - - - - - -.
:    s1                     :     :                               :
:   +-----------+-------+   :     :                               :
:   | capacity  |     5 |   :     :   +----+----+----+----+----+  :
:   | ptr       |     o-+---+-----+-->| H  | e  | l  | l  | o  |  :
:   | len       |     5 |   :     :   +----+----+----+----+----+  :
:   +-----------+-------+   :     :                               :
:                           :     :                               :
`- - - - - - - - - - - - - -'     `- - - - - - - - - - - - - - - -'
```

<details>

- 提到 `String` 是由 `Vec` 支撑的，因此它有容量和长度，并且如果可变，可以通过在堆上重新分配来增长。

- 如果学生询问，你可以提到底层内存是使用 [系统分配器] 分配的，并且可以使用 [分配器 API] 实现自定义分配器。

## 更多探索

我们可以用 `unsafe` Rust 检查内存布局。不过，你应该指出这是正当的不安全操作！

```rust,editable
fn main() {
    let mut s1 = String::from("Hello");
    s1.push(' ');
    s1.push_str("world");
    // 千万不要在家里面这么做！仅供教育用途。
    // String 不提供关于其布局的任何保证，因此这可能导致未定义的行为。
    unsafe {
        let (capacity, ptr, len): (usize, usize, usize) = std::mem::transmute(s1);
        println!("capacity = {capacity}, ptr = {ptr:#x}, len = {len}");
    }
}
```

```markdown
</details>

[系统分配器]: https://doc.rust-lang.org/std/alloc/struct.System.html
[分配器 API]: https://doc.rust-lang.org/std/alloc/index.html
```
