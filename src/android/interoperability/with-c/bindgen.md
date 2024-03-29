---
translated_at: '2024-03-26T12:00:05.442Z'
---

# 使用 Bindgen

[bindgen](https://rust-lang.github.io/rust-bindgen/introduction.html) 工具
可以从 C 头文件自动生成绑定。

首先创建一个小型的 C 库：

_interoperability/bindgen/libbirthday.h_：

```c
{{#include bindgen/libbirthday.h:card}}
```

_interoperability/bindgen/libbirthday.c_：

```c
{{#include bindgen/libbirthday.c:print_card}}
```

将以下内容添加到你的 `Android.bp` 文件中：

_interoperability/bindgen/Android.bp_：

```javascript
{{#include bindgen/Android.bp:libbirthday}}
```

为库创建一个包装头文件（在本例中并不严格需要）：

_interoperability/bindgen/libbirthday_wrapper.h_：

```c
{{#include bindgen/libbirthday_wrapper.h:include}}
```

你现在可以自动生成绑定：

_interoperability/bindgen/Android.bp_：

```javascript
{{#include bindgen/Android.bp:libbirthday_bindgen}}
```

最后，我们可以在我们的 Rust 程序中使用这些绑定：

_interoperability/bindgen/Android.bp_：

```javascript
{{#include bindgen/Android.bp:print_birthday_card}}
```

_interoperability/bindgen/main.rs_：

```rust,compile_fail
{{#include bindgen/main.rs:main}}
```

构建、推送并在设备上运行二进制文件：

```shell
{{#include ../../build_all.sh:print_birthday_card}}
```

最后，我们可以运行自动生成的测试以确保绑定正常工作：

_interoperability/bindgen/Android.bp_：

```javascript
{{#include bindgen/Android.bp:libbirthday_bindgen_test}}
```

```shell
{{#include ../../build_all.sh:libbirthday_bindgen_test}}
```
