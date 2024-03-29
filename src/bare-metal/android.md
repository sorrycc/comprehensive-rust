---
translated_at: '2024-03-26T11:33:06.204Z'
---

# Android

要在 AOSP 中构建一个裸机 Rust 二进制文件，你需要使用 `rust_ffi_static` Soong 规则来构建你的 Rust 代码，然后使用 `cc_binary` 和链接脚本来生成二进制文件本身，接着使用 `raw_binary` 将 ELF 转换成准备运行的原始二进制文件。

```soong
rust_ffi_static {
    name: "libvmbase_example",
    defaults: ["vmbase_ffi_defaults"],
    crate_name: "vmbase_example",
    srcs: ["src/main.rs"],
    rustlibs: [
        "libvmbase",
    ],
}

cc_binary {
    name: "vmbase_example",
    defaults: ["vmbase_elf_defaults"],
    srcs: [
        "idmap.S",
    ],
    static_libs: [
        "libvmbase_example",
    ],
    linker_scripts: [
        "image.ld",
        ":vmbase_sections",
    ],
}

raw_binary {
    name: "vmbase_example_bin",
    stem: "vmbase_example.bin",
    src: ":vmbase_example",
    enabled: false,
    target: {
        android_arm64: {
            enabled: true,
        },
    },
}
```
