---
translated_at: '2024-03-26T11:58:58.253Z'
---

# 与 Java 的互操作性

Java 可以通过 [Java 原生接口 (JNI)](https://zh.wikipedia.org/wiki/Java%E5%8E%9F%E7%94%9F%E6%8E%A5%E5%8F%A3) 加载共享对象。[`jni` 包](https://docs.rs/jni/) 允许你创建一个兼容的库。

首先，我们创建一个 Rust 函数以供 Java 调用：

_interoperability/java/src/lib.rs_：

```rust,compile_fail
{{#include java/src/lib.rs:hello}}
```

_interoperability/java/Android.bp_：

```javascript
{{#include java/Android.bp:libhello_jni}}
```

然后我们从 Java 调用这个函数：

_interoperability/java/HelloWorld.java_：

```java
{{#include java/HelloWorld.java:HelloWorld}}
```

_interoperability/java/Android.bp_：

```javascript
{{#include java/Android.bp:helloworld_jni}}
```

最后，你可以构建、同步并运行该二进制文件：

```shell
{{#include ../build_all.sh:helloworld_jni}}
```
