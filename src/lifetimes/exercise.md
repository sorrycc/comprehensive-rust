---
minutes: 30
translated_at: '2024-03-26T10:41:31.440Z'
---

# 练习：Protobuf 解析

在这个练习中，你将构建一个解析器来处理 [protobuf 二进制编码](https://protobuf.dev/programming-guides/encoding/)。别担心，它比看起来简单！这演示了一个常见的解析模式，传递数据切片。底层数据本身从未被复制。

完全解析一个 protobuf 消息需要知道字段的类型，这些字段通过它们的字段编号进行索引。这通常在 `proto` 文件中提供。在这个练习中，我们将这些信息编码到函数中的 `match` 语句中，这些函数会为每个字段调用。

我们将使用以下 proto：

```proto
message PhoneNumber {
  optional string number = 1;
  optional string type = 2;
}

message Person {
  optional string name = 1;
  optional int32 id = 2;
  repeated PhoneNumber phones = 3;
}
```

一个 proto 消息被编码为一系列一个接一个的字段。每个字段实现为一个“标签”后跟该值。标签包含一个字段编号（例如，`Person` 消息的 `id` 字段为 `2`）和一个线型类型，定义了如何从字节流中确定有效载荷。

整数，包括标签，使用一种称为 VARINT 的可变长度编码表示。幸运的是，`parse_varint` 已为您定义如下。给定的代码还定义了回调来处理 `Person` 和 `PhoneNumber` 字段，并将消息解析为一系列对这些回调的调用。

你需要做的是实现 `parse_field` 函数和为 `Person` 和 `PhoneNumber` 实现 `ProtoMessage` 特性。

<!-- compile_fail because `mdbook test` does not allow use of `thiserror` -->

```rust,editable,compile_fail
{{#include exercise.rs:preliminaries }}


{{#include exercise.rs:parse_field }}
        _ => todo!("根据线型类型，构建一个 Field，消耗尽可能多的字节。")
    };
    todo!("返回字段，以及任何未消耗的字节。")
}

{{#include exercise.rs:parse_message }}

{{#include exercise.rs:message_types}}

// TODO: 为 Person 和 PhoneNumber 实现 ProtoMessage。

{{#include exercise.rs:main }}
```
