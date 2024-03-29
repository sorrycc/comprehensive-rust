---
minutes: 10
translated_at: '2024-03-26T11:29:27.470Z'
---

# 内部可变性

在某些情况下，有必要修改共享（只读）引用后面的数据。例如，一个共享数据结构可能有一个内部缓存，并希望从只读方法中更新该缓存。

“内部可变性”模式允许在共享引用之后进行独占（可变）访问。标准库提供了几种方法来实现这一点，同时仍然确保安全性，通常通过执行运行时检查来实现。

## `RefCell`

```rust,editable
use std::cell::RefCell;
use std::rc::Rc;

#[derive(Debug, Default)]
struct Node {
    value: i64,
    children: Vec<Rc<RefCell<Node>>>,
}

impl Node {
    fn new(value: i64) -> Rc<RefCell<Node>> {
        Rc::new(RefCell::new(Node { value, ..Node::default() }))
    }

    fn sum(&self) -> i64 {
        self.value + self.children.iter().map(|c| c.borrow().sum()).sum::<i64>()
    }
}

fn main() {
    let root = Node::new(1);
    root.borrow_mut().children.push(Node::new(5));
    let subtree = Node::new(10);
    subtree.borrow_mut().children.push(Node::new(11));
    subtree.borrow_mut().children.push(Node::new(12));
    root.borrow_mut().children.push(subtree);

    println!("图形: {root:#?}");
    println!("图形总和: {}", root.borrow().sum());
}
```

## `Cell`

`Cell` 封装了一个值，并允许获取或设置该值，即使有一个共享引用指向 `Cell`。然而，它不允许对该值的任何引用。既然没有引用，借用规则就不能被打破。

<details>

这个幻灯片主要告诉我们的是，Rust 提供了 _安全的_ 方法来修改共享引用后的数据。确保安全性有多种方式，`RefCell` 和 `Cell` 是其中的两种。

- `RefCell` 用运行时检查来强制执行 Rust 的通常借用规则（要么是多个共享引用，要么是单个独占引用）。在这种情况下，所有的借用都非常短暂且从不重叠，因此检查总是成功的。

- `Rc` 只允许对其内容进行共享（只读）访问，因为它的目的是

允许（并计数）多个引用。但是我们想要修改值，所以我们需要内部可变性。

- `Cell` 是确保安全的更简单方法：它有一个 `set` 方法，接受 `&self`。这不需要运行时检查，但需要移动值，这可能有自己的成本。

- 通过向 `subtree.children` 添加 `root` 来展示可以创建引用循环。

- 为了演示运行时 panic，添加一个 `fn inc(&mut self)` 函数，该函数增加 `self.value` 并调用其子节点上的同样方法。在引用循环存在的情况下，这将会 panic，伴随着 `thread 'main' panicked at 'already borrowed: BorrowMutError'`。
