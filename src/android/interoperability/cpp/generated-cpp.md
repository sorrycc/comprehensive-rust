---
translated_at: '2024-03-26T12:02:06.220Z'
---

# 生成的 C++

```rust,ignore
#[cxx::bridge]
mod ffi {
{{#include ../../../../third_party/cxx/blobstore/src/main.rs:rust_bridge}}
}
```

大致会生成以下的 C++ 代码：

```cpp
struct MultiBuf final : public ::rust::Opaque {
  ~MultiBuf() = delete;

private:
  friend ::rust::layout;
  struct layout {
    static ::std::size_t size() noexcept;
    static ::std::size_t align() noexcept;
  };
};

::rust::Slice<::std::uint8_t const> next_chunk(::org::blobstore::MultiBuf &buf) noexcept;
```
