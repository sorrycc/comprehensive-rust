---
translated_at: '2024-03-26T11:08:32.029Z'
---

# `Send`

> 如果将类型 `T` 的值移动到另一个线程是安全的，则 `T` 是 [`Send`][1] 类型。

将所有权移动到另一线程的效果是，_析构函数_ 将在该线程中执行。所以问题在于你何时能够在一个线程分配一个值，并在另一个线程释放它。

[1]: https://doc.rust-lang.org/std/marker/trait.Send.html

<details>

举个例子，SQLite 库的连接必须只能从单个线程访问。

</details>
