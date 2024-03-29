---
minutes: 5
translated_at: '2024-03-26T11:57:19.654Z'
---

# 模拟测试

在进行模拟测试时，[Mockall] 是一个广泛使用的库。您需要重构您的代码以使用特性（traits），然后可以快速进行模拟：

```rust,ignore
{{#include mockall.rs:simple_example}}
```

[Mockall]: https://docs.rs/mockall/

<details>

- Mockall 是在 Android (AOSP) 中推荐使用的模拟测试库。在 [crates.io](https://crates.io/keywords/mock) 上也有其它[可用的 mocking 库](https://crates.io/keywords/mock)，特别是在模拟 HTTP 服务的领域。其他模拟库的工作方式与 Mockall 相似，这意味着它们都可以容易地获得一个给定特性的模拟实现。

- 需要注意的是，模拟测试在某些人看来是有些 _争议的_：模拟允许您将测试完全与其依赖隔离开。直接的结果是测试执行更快且更稳定。另一方面，模拟配置可能会有误，返回与真实依赖不同的输出。

  如果可能，建议您使用真实的依赖关系。例如，许多数据库允许您配置一个内存中的后端。这意味着您在测试中获取到的行为是正确的，而且这些测试快速且会在结束后自动清理。

  类似地，许多网络框架允许您启动一个绑定在 `localhost` 的随机端口的进程内服务器。总是优先这样做，而不是模拟掉框架，因为它帮助您在真实环境中测试代码。

- Mockall 不是 Rust Playground 的一部分，因此您需要在本地环境中运行这个示例。使用 `cargo add mockall` 可以快速地将 Mockall 添加到现有的 Cargo 项目中。

- Mockall 还有更多功能。特别是，您可以设置取决于传递参数的期望。这里我们使用它来模拟一只猫，这只猫在最后一次喂食后 3 小时变得饥饿：

```rust,ignore
{{#include mockall.rs:extended_example}}
```

- 您可以使用 `.times(n)` 来限制一个模拟方法可以被调用的次数为 `n` —— 如果没有达到这个条件，模拟对象在被丢弃时将会自动触发 panic。

</details>
