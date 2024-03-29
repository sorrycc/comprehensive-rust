---
translated_at: '2024-03-26T11:55:10.932Z'
---

# 设置

我们将使用 Cuttlefish Android 虚拟设备来测试我们的代码。请确保您已经可以访问一个设备，或者使用以下命令创建一个新的：

```shell
source build/envsetup.sh
lunch aosp_cf_x86_64_phone-trunk_staging-userdebug
acloud create
```

详情请参见 [Android 开发者 Codelab](https://source.android.com/docs/setup/start)。

<details>

关键点：

- Cuttlefish 是一个参考 Android 设备，旨在通用 Linux 桌面上工作。MacOS 支持也在计划中。

- Cuttlefish 系统镜像保持了对真实设备的高保真度，并且是运行许多 Rust 使用案例的理想模拟器。

</details>
