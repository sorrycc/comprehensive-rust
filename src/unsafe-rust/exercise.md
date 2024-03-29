---
minutes: 30
translated_at: '2024-03-26T09:55:00.210Z'
---

# 安全的 FFI 包装器

Rust 对调用通过 _外部函数接口_（FFI）的函数支持得很好。我们将使用它来构建一个安全的包装器，用以调用你会在 C 语言中用来读取目录中文件名的 `libc` 函数。

你需要查阅手册页面：

- [`opendir(3)`](https://man7.org/linux/man-pages/man3/opendir.3.html)
- [`readdir(3)`](https://man7.org/linux/man-pages/man3/readdir.3.html)
- [`closedir(3)`](https://man7.org/linux/man-pages/man3/closedir.3.html)

你还会想浏览 [`std::ffi`] 模块。在那里你会发现一些在练习中需要的字符串类型：

| 类型                        | 编码方式       | 使用场景                      |
| --------------------------- | -------------- | ----------------------------- |
| [`str`] 和 [`String`]       | UTF-8          | Rust 中的文本处理             |
| [`CStr`] 和 [`CString`]     | NUL 结尾       | 与 C 函数通信                 |
| [`OsStr`] 和 [`OsString`]   | 系统特定       | 与操作系统通信                |

你将在所有这些类型之间进行转换：

- `&str` 到 `CString`：你需要为尾随的 `\0` 字符分配空间，
- `CString` 到 `*const i8`：你需要一个指针来调用 C 函数，
- `*const i8` 到 `&CStr`：你需要某些东西以找到尾随的 `\0` 字符，
- `&CStr` 到 `&[u8]`：字节切片是“某些未知数据”的通用接口，
- `&[u8]` 到 `&OsStr`：`&OsStr` 是向 `OsString` 迈进的一步，使用 [`OsStrExt`](https://doc.rust-lang.org/std/os/unix/ffi/trait.OsStrExt.html) 来创建它，
- `&OsStr` 到 `OsString`：你需要克隆 `&OsStr` 中的数据以能够返回它并再次调用 `readdir`。

[Nomicon] 也有一个关于 FFI 非常有用的章节。

[`std::ffi`]: https://doc.rust-lang.org/std/ffi/
[`str`]: https://doc.rust-lang.org/std/primitive.str.html
[`String`]: https://doc.rust-lang.org/std/string/struct.String.html
[`CStr`]: https://doc.rust-lang.org/std/ffi/struct.CStr.html
[`CString`]: https://doc.rust-lang.org/std/ffi/struct.CString.html

```rust,should_panic
// TODO: 移除此行，当你完成实现后。
#![allow(unused_imports, unused_variables, dead_code)]

{{#include exercise.rs:ffi}}

{{#include exercise.rs:DirectoryIterator}}
        unimplemented!()
    }
}

{{#include exercise.rs:Iterator}}
        unimplemented!()
    }
}

{{#include exercise.rs:Drop}}
        unimplemented!()
    }
}

{{#include exercise.rs:main}}
```
