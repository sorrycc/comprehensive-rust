---
translated_at: '2024-03-26T11:10:54.001Z'
---

# 设置

确保你能够构建并运行 Chromium。任何平台和一组构建标志都是可以的，只要你的代码相对较新（提交位置 1223636 以后，对应于 2023 年 11 月）：

```shell
gn gen out/Debug
autoninja -C out/Debug chrome
out/Debug/chrome # 或在 Mac 上，out/Debug/Chromium.app/Contents/MacOS/Chromium
```

（组件调试构建被推荐用于最快的迭代时间。这是默认设置！）

如果你还没准备好，请查看[如何构建 Chromium](https://www.chromium.org/developers/how-tos/get-the-code/)。要注意：设置构建 Chromium 需要时间。

同时建议你安装 Visual Studio Code。

# 关于练习

这部分课程包含了一系列互相依赖的练习。
我们将在整个课程中分散进行，而不是仅在最后。如果你没有时间完成某个部分，不用担心：你可以在下一环节中赶上。
