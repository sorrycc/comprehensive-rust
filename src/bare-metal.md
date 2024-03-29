---
course: Bare Metal
session: Morning
translated_at: '2024-03-26T09:42:23.613Z'
---

# 欢迎来到裸机 Rust

这是一个关于裸机 Rust 的独立为期一天的课程，面向的是那些熟悉 Rust 基础的人（可能是通过完成全面的 Rust 课程），并且理想情况下还有一些在其他语言（如 C）中进行裸机编程的经验。

今天我们将讨论“裸机” Rust：在没有操作系统的支持下运行 Rust 代码。这将分为几个部分：

- 什么是 `no_std` Rust？
- 为微控制器编写固件。
- 为应用处理器编写引导程序 / 内核代码。
- 一些对裸机 Rust 开发有用的 crates。

对于课程中的微控制器部分，我们将使用 [BBC micro:bit](https://microbit.org/) v2 作为示例。它是一个基于 Nordic nRF51822 微控制器的 [开发板](https://tech.microbit.org/hardware/)，带有一些 LED 和按钮，一个通过 I2C 连接的加速度计和指南针，以及一个板载 SWD 调试器。

首先，安装一些稍后我们将需要的工具。在 gLinux 或 Debian 上：

<!-- mdbook-xgettext: skip -->

```bash
sudo apt install gcc-aarch64-linux-gnu gdb-multiarch libudev-dev picocom pkg-config qemu-system-arm
rustup update
rustup target add aarch64-unknown-none thumbv7em-none-eabihf
rustup component add llvm-tools-preview
cargo install cargo-binutils cargo-embed
```

并给予 `plugdev` 组的用户访问 micro:bit 编程器的权限：

<!-- mdbook-xgettext: skip -->

```bash
echo 'SUBSYSTEM=="usb", ATTR{idVendor}=="0d28", MODE="0664", GROUP="plugdev"' |\
  sudo tee /etc/udev/rules.d/50-microbit.rules
sudo udevadm control --reload-rules
```

在 MacOS 上：

<!-- mdbook-xgettext: skip -->

```bash
xcode-select --install
brew install gdb picocom qemu
brew install --cask gcc-aarch64-embedded
rustup update
rustup target add aarch64-unknown-none thumbv7em-none-eabihf
rustup component add llvm-tools-preview
cargo install cargo-binutils cargo-embed
```
