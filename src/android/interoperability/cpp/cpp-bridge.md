---
translated_at: '2024-03-26T12:02:59.115Z'
---

# C++ 桥接声明

```rust,ignore
#[cxx::bridge]
mod ffi {
{{#include ../../../../third_party/cxx/blobstore/src/main.rs:cpp_bridge}}
}
```

大致会产生以下 Rust 代码：

```rust,ignore
#[repr(C)]
pub struct BlobstoreClient {
    _private: ::cxx::private::Opaque,
}

pub fn new_blobstore_client() -> ::cxx::UniquePtr<BlobstoreClient> {
    extern "C" {
        #[link_name = "org$blobstore$cxxbridge1$new_blobstore_client"]
        fn __new_blobstore_client() -> *mut BlobstoreClient;
    }
    unsafe { ::cxx::UniquePtr::from_raw(__new_blobstore_client()) }
}

impl BlobstoreClient {
    pub fn put(&self, parts: &mut MultiBuf) -> u64 {
        extern "C" {
            #[link_name = "org$blobstore$cxxbridge1$BlobstoreClient$put"]
            fn __put(
                _: &BlobstoreClient,
                parts: *mut ::cxx::core::ffi::c_void,
            ) -> u64;
        }
        unsafe {
            __put(self, parts as *mut MultiBuf as *mut ::cxx::core::ffi::c_void)
        }
    }
}

// ...
```

<details>

- 程序员不需要保证他们输入的签名是准确的。CXX 执行静态断言以确保签名完全对应于 C++ 中声明的内容。
- `unsafe extern` 块允许你声明从 Rust 安全调用的 C++ 函数。

</details>
