# fingerprint-chromium

*一个基于`Ungoogled Chromium`的指纹浏览器*

## 安装与使用

### 下载
请从以下链接下载适配您系统的版本，每个大版本的 Chromium 会编译一个对应的版本，选择适合的操作系统和版本进行下载：

| **版本**        | **源码**                                                                                   | **Windows**                                                                                   | **Linux**                                                                                   |
|------------------|--------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------|
| **Chrome 130**   | [130.0.6723.116](https://github.com/adryfish/fingerprint-chromium/tree/130.0.6723.116)               | [安装包](https://github.com/adryfish/fingerprint-chromium/releases/download/130.0.6723.116/ungoogled-chromium_130.0.6723.116-1.1_installer_x64.exe) <br> [ZIP](https://github.com/adryfish/fingerprint-chromium/releases/download/130.0.6723.116/ungoogled-chromium_130.0.6723.116-1.1_windows_x64.zip) | [130.0.6723.116-1_linux.tar.xz](https://github.com/adryfish/fingerprint-chromium/releases/download/130.0.6723.116/ungoogled-chromium_130.0.6723.116-1_linux.tar.xz) |
| **Chrome 129**   | [129.0.6668.100](https://github.com/adryfish/fingerprint-chromium/tree/129.0.6668.100)               | [安装包](https://github.com/adryfish/fingerprint-chromium/releases/download/129.0.6668.100/ungoogled-chromium_129.0.6668.100-1.1_installer_x64.exe) <br> [ZIP](https://github.com/adryfish/fingerprint-chromium/releases/download/129.0.6668.100/ungoogled-chromium_129.0.6668.100-1.1_windows_x64.zip) | [129.0.6668.100-1_linux.tar.xz](https://github.com/adryfish/fingerprint-chromium/releases/download/129.0.6668.100/ungoogled-chromium_129.0.6668.100-1_linux.tar.xz) |


---

在 GitHub Release 页面中，您可以找到每个大版本的 Chromium 对应的编译版本，选择合适的文件进行下载。

### 编译源码
参考 [`ungoogled-chromium`](https://github.com/ungoogled-software/ungoogled-chromium/blob/master/docs/building.md) 。只需将submodule中的`ungoogled-chromium`仓库地址替换为 `fingerprint-browser`即可。


## 功能特性

### 指纹支持

| **指纹特性**                          | **描述**                                                                                     | **命令行参数**                                                                 |
|--------------------------------------|----------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------|
| **User-Agent**                       | 修改浏览器的 `User-Agent` 信息，包括 `navigator.userAgent`、`navigator.platform`、`navigator.userAgentData` 和 Client Hints | `--fingerprint-platform` <br>`--fingerprint-platform-version`|
| **音频指纹**                         | 干扰或伪造音频指纹数据                                                                       | `--fingerprint`（启用指纹种子后生效）                                           |
| **插件指纹**                         | 修改插件相关特征                                                                              | `--fingerprint`（启用指纹种子后生效）                                           |
| **硬件指纹**                         | 自定义硬件参数，包括 CPU 核心数和内存大小                                                     | `--fingerprint` <br> `--fingerprint-hardware-concurrency` |
| **字体指纹**                         | 修改系统字体信息                                                                              | `--fingerprint`（启用指纹种子后生效）                                           |
| **Canvas 图像数据噪声**               | 在 Canvas 图像数据中添加噪声，最多修改 10 个像素，干扰指纹生成                                | `--fingerprinting-canvas-image-data-noise`                                        |
| **Canvas 测量文本噪声**               | 对 `Canvas::measureText()` 输出值进行比例缩放，随机因子范围为 `-0.0003%` 到 `0.0003%`，每次文档初始化时重新计算 | `--fingerprinting-canvas-measuretext-noise`                                       |
| **ClientRects 噪声**                  | 对 `getClientRects()` 和 `getBoundingClientRect()` 输出值进行比例缩放，随机因子范围为 `-0.0003%` 到 `0.0003%`，每次文档初始化时重新计算 | `--fingerprinting-client-rects-noise`                                           |
| **WebRTC 策略**                       | 默认禁用非代理 UDP 连接，防止通过 WebRTC 泄露真实 IP 地址                                     | `--disable-non-proxied-udp`（默认启用）                                           |
| **语言支持**                         | 设置浏览器的语言和接受的语言                                                                  | `--lang`（设置浏览器语言）<br> `--accept-lang`（设置接受语言）                     |
| **时区支持**                         | 设置浏览器时区                                                                              | `TZ` 环境变量（设置时区，例如 `TZ=Asia/Shanghai`）                              |


### 自动化支持
**优化了自动化使用场景，提供了以下特性：**

1. 封闭 Shadow DOM 的伪造支持
新增fakeShadowRoot属性，与shadowRoot属性相同，但是实现对Closed Shadow Root访问，方便自动化工具处理。

2. 避免 CDP 检测
调用 Runtime.enable 时不会触发 CDP（Chrome DevTools Protocol）检测，进一步增强自动化的隐蔽性。

### 启用指纹功能的命令行参数

在启动浏览器时，通过命令行参数启用或自定义指纹和隐私保护功能：

| **命令行参数**                              | **描述**                                                                                       |
|---------------------------------------------|------------------------------------------------------------------------------------------------|
| **`--fingerprint`**                         | 指定指纹种子 (seed)，启用后大部分指纹生效 |
| **`--fingerprint-platform`**                | 指定操作系统类型，值可以是：`windows`, `linux`, `macos`                                        |
| **`--fingerprint-platform-version`**        | 指定操作系统版本，不填写时将使用默认版本                                                      |
| **`--fingerprint-hardware-concurrency`**    | 指定 CPU 核心数，如果未提供，则由 `--fingerprint` 中的种子随机生成                             |
| **`--fingerprinting-canvas-image-data-noise`** | 启用 Canvas 图像数据指纹的噪声干扰                                                            |
| **`--fingerprinting-canvas-measuretext-noise`** | 启用 Canvas 测量文本指纹的比例缩放噪声                                                       |
| **`--fingerprinting-client-rects-noise`**   | 启用 ClientRects 和 BoundingClientRect 的比例缩放噪声                                        |
| **`--disable-non-proxied-udp`**             | 指定WebRTC策略，默认是禁用非代理UDP连接(建议不设置)                                                      |
| **`--lang`** <br>  **`--accept-lang`**      | 设置浏览器的语言                                                  |


## Credits

 * [Ungoogled Chromium](https://github.com/ungoogled-software/ungoogled-chromium)

 ## License

BSD-3-clause. See [LICENSE](LICENSE)