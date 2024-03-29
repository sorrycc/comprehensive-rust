---
translated_at: '2024-03-26T11:09:07.493Z'
---

# 示例

## `Send + Sync`

你会遇到的大多数类型都是 `Send + Sync`：

- `i8`、`f32`、`bool`、`char`、`&str`，…
- `(T1, T2)`、`[T; N]`、`&[T]`、`struct { x: T }`，…
- `String`、`Option<T>`、`Vec<T>`、`Box<T>`，…
- `Arc<T>`：通过原子引用计数显式实现线程安全。
- `Mutex<T>`：通过内部锁实现显式线程安全。
- `mpsc::Sender<T>`：从 1.72.0 版本开始。
- `AtomicBool`、`AtomicU8`，…：使用特殊的原子指令。

泛型类型通常在类型参数是 `Send + Sync` 时，也是 `Send + Sync`。

## `Send + !Sync`

这些类型可以移到其他线程，但它们不是线程安全的。
通常是因为存在内部可变性：

- `mpsc::Receiver<T>`
- `Cell<T>`
- `RefCell<T>`

## `!Send + Sync`

这些类型是线程安全的，但它们不能被移到另一个线程：

- `MutexGuard<T: Sync>`：使用操作系统级原语，必须在创建它们的线程上释放。

## `!Send + !Sync`

这些类型不是线程安全的，也不能移动到其他线程：

- `Rc<T>`：每个 `Rc<T>` 都有一个引用 `RcBox<T>`，其中包含一个非原子的引用计数。
- `*const T`、`*mut T`：Rust 假设原始指针可能具有特殊的并发考虑因素。
