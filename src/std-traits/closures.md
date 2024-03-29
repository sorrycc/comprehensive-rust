---
minutes: 20
translated_at: '2024-03-26T10:11:21.110Z'
---

# 闭包

闭包或 lambda 表达式具有无法命名的类型。然而，它们实现了特殊的 [`Fn`](https://doc.rust-lang.org/std/ops/trait.Fn.html)、[`FnMut`](https://doc.rust-lang.org/std/ops/trait.FnMut.html) 和 [`FnOnce`](https://doc.rust-lang.org/std/ops/trait.FnOnce.html) 特质：

```rust,editable
fn apply_with_log(func: impl FnOnce(i32) -> i32, input: i32) -> i32 {
    println!("Calling function on {input}");
    func(input)
}

fn main() {
    let add_3 = |x| x + 3;
    println!("add_3: {}", apply_with_log(add_3, 10));
    println!("add_3: {}", apply_with_log(add_3, 20));

    let mut v = Vec::new();
    let mut accumulate = |x: i32| {
        v.push(x);
        v.iter().sum::<i32>()
    };
    println!("accumulate: {}", apply_with_log(&mut accumulate, 4));
    println!("accumulate: {}", apply_with_log(&mut accumulate, 5));

    let multiply_sum = |x| x * v.into_iter().sum::<i32>();
    println!("multiply_sum: {}", apply_with_log(multiply_sum, 3));
}
```

<details>

一个 `Fn`（例如 `add_3`）既不消耗也不更改所捕获的值，或者可能根本没有捕获任何值。它可以被多次并发调用。

一个 `FnMut`（例如 `accumulate`）可能会修改所捕获的值。您可以调用它多次，但不能同时调用。

如果你有一个 `FnOnce`（例如 `multiply_sum`），你只能调用它一次。它可能消耗所捕获的值。

`FnMut` 是 `FnOnce` 的子类型。`Fn` 是 `FnMut` 和 `FnOnce` 的子类型。即，你可以在需要 `FnOnce` 的地方使用 `FnMut`，并且可以在需要 `FnMut` 或 `FnOnce` 的地方使用 `Fn`。

当你定义一个接受闭包的函数时，如果你可以的话（即只调用它一次），就应该采用 `FnOnce`，否则就使用 `FnMut`，最后才是 `Fn`。这为调用者提供了最大的灵活性。

相比之下，当你有一个闭包时，最灵活的是 `Fn`（它可以在任何地方传递），然后是 `FnMut`，最后是 `FnOnce`。

编译器还会根据闭包所捕获的内容推断 `Copy`（例如 `add_3`）和 `Clone`（例如 `multiply_sum`）。

默认情况下，如果可能，闭包会通过引用来捕获。`move` 关键字使它们通过值来捕获。

```rust,editable
fn make_greeter(prefix: String) -> impl Fn(&str) {
    return move |name| println!("{} {}", prefix, name);
}

fn main() {
    let hi = make_greeter("Hi".to_string());
    hi("Greg");
}
```
