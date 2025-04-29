# fingerprint-chromium

*一个基于`Ungoogled Chromium`的指纹浏览器*

## 安装与使用

### 下载
请从以下链接下载适配您系统的版本，每个大版本的 Chromium 会编译一个对应的版本，选择适合的操作系统和版本进行下载：

| **版本**        | **源码**                                                                                   | **Windows**                                                                                   | **Linux**                                                                                   | **MacOS**     |
|------------------|--------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------| ---------------------------------------------------------------------------------------------|
| **Chrome 134**   | [134.0.6998.165](https://github.com/adryfish/fingerprint-chromium/tree/134.0.6998.165)               | [安装包](https://github.com/adryfish/fingerprint-chromium/releases/download/134.0.6998.165/ungoogled-chromium_134.0.6998.165-1.1_installer_x64.exe) <br> [ZIP](https://github.com/adryfish/fingerprint-chromium/releases/download/134.0.6998.165/ungoogled-chromium_134.0.6998.165-1.1_windows_x64.zip) | [ 134.0.6998.165-1_linux.tar.xz ](https://github.com/adryfish/fingerprint-chromium/releases/download/134.0.6998.165/ungoogled-chromium_134.0.6998.165-1_linux.tar.xz) |  |
| **Chrome 133**   | [133.0.6943.126](https://github.com/adryfish/fingerprint-chromium/tree/133.0.6943.126)               | [安装包](https://github.com/adryfish/fingerprint-chromium/releases/download/133.0.6943.126/ungoogled-chromium_133.0.6943.126-1.1_installer_x64.exe) <br> [ZIP](https://github.com/adryfish/fingerprint-chromium/releases/download/133.0.6943.126/ungoogled-chromium_133.0.6943.126-1.1_windows_x64.zip) | [ 133.0.6943.126-1_linux.tar.xz ](https://github.com/adryfish/fingerprint-chromium/releases/download/133.0.6943.126/ungoogled-chromium_133.0.6943.126-1_linux.tar.xz) |  |
| **Chrome 132**   | [132.0.6834.159](https://github.com/adryfish/fingerprint-chromium/tree/132.0.6834.159)               | [安装包](https://github.com/adryfish/fingerprint-chromium/releases/download/132.0.6834.159/ungoogled-chromium_132.0.6834.159-1.1_installer_x64.exe) <br> [ZIP](https://github.com/adryfish/fingerprint-chromium/releases/download/132.0.6834.159/ungoogled-chromium_132.0.6834.159-1.1_windows_x64.zip) | [ 132.0.6834.159-1_linux.tar.xz ](https://github.com/adryfish/fingerprint-chromium/releases/download/132.0.6834.159/ungoogled-chromium_132.0.6834.159-1_linux.tar.xz) | [132.0.6834.110-1.1_macos.dmg](https://github.com/adryfish/fingerprint-chromium/releases/download/132.0.6834.159/ungoogled-chromium_132.0.6834.110-1.1_macos.dmg) |

---

在 GitHub Release 页面中，您可以找到每个大版本的 Chromium 对应的编译版本，选择合适的文件进行下载。

### 编译源码
参考 [`ungoogled-chromium`](https://github.com/ungoogled-software/ungoogled-chromium/blob/master/docs/building.md) 。只需将submodule中的`ungoogled-chromium`仓库地址替换为 `fingerprint-browser`即可。


## 📢 广告

<div style="border: 2px solid #f39c12; padding: 15px; background-color: #fffbe6; border-radius: 10px;">

<details open>
<summary><b>🌟 推荐工具：EasyChat - Claude官网镜像</b></summary>

🔥 **EasyChat** 是一个无需注册和登录的 Claude 官网镜像，免费提供国内直登体验，1:1 还原官网功能，为你畅享高效的 AI 助手服务！

- 🆓 **免费使用**：无任何额外费用，即刻体验 Claude 的强大功能。
- 🚀 **无需登录**：轻松访问，无需繁琐的注册流程。
- 🌐 **国内直登**：快速直连，无需额外设置，畅享便捷。
- 💎 **共享会员**：支持多人共享高级会员权益，解锁高阶模型与专属服务。

🔗 **访问网站**：[https://easychat.top](https://easychat.top)

</details>

</div>


## 功能特性

### 指纹支持

| **指纹特性**                          | **描述**                                                                                     | **命令行参数**                                                                 |
|--------------------------------------|----------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------|
| **User-Agent**                       | 修改浏览器的 `User-Agent` 信息，包括 `navigator.userAgent`、`navigator.platform`、`navigator.userAgentData` 和 `Client Hints` | `--fingerprint-platform` <br>`--fingerprint-platform-version` <br>`--fingerprint-brand` <br>`--fingerprint-brand-version` |
| **音频指纹**                         | 干扰或伪造音频指纹数据                                                                       | `--fingerprint`（启用指纹种子后生效）                                           |
| **插件指纹**                         | 修改插件相关特征                                                                              | 133+去除，浏览器会返回固定的插件列表,伪装反而会暴露 |
| **硬件指纹**                         | 自定义硬件参数，包括 CPU 核心数和内存大小                                                     | `--fingerprint` <br> `--fingerprint-hardware-concurrency` |
| **GPU Report**                         | 修改GPU供应商和显卡型号(暂时只支持Linux) | `--fingerprint`（启用指纹种子后生效） |
| **字体指纹**                         | 修改系统字体信息                                                                              | `--fingerprint`（启用指纹种子后生效）                                           |
| **Canvas 图像数据噪声**               | 在 Canvas 图像数据中添加噪声，最多修改 10 个像素，干扰指纹生成                                | `--fingerprint`                                        |
| **Canvas 测量文本噪声**               | 对 `Canvas::measureText()` 输出值进行比例缩放，随机因子范围为 `-0.0003%` 到 `0.0003%`，每次文档初始化时重新计算 |  `--fingerprint`                                      |
| **ClientRects 噪声**                  | 对 `getClientRects()` 和 `getBoundingClientRect()` 输出值进行比例缩放，随机因子范围为 `-0.0003%` 到 `0.0003%`，每次文档初始化时重新计算 |  `--fingerprint`                                          |
| **WebRTC 策略**                       | 默认禁用非代理 UDP 连接，防止通过 WebRTC 泄露真实 IP 地址                                     | `--disable-non-proxied-udp`（默认启用）                                           |
| **语言支持**                         | 设置浏览器的语言和接受的语言                                                                  | `--lang`（设置浏览器语言）<br> `--accept-lang`（设置接受语言）                     |
| **时区支持**                         | 设置浏览器时区                                                                              | `TZ` 环境变量（设置时区，例如 `TZ=Asia/Shanghai`）                              |


### 自动化支持
**优化了自动化使用场景，提供了以下特性：**

1. **封闭 Shadow DOM 的伪造支持**
  新增fakeShadowRoot属性，与shadowRoot属性相同，但是实现对Closed Shadow Root访问，方便自动化工具处理。

2. **避免 CDP 检测**
调用 Runtime.enable 时不会触发 CDP（Chrome DevTools Protocol）检测，进一步增强自动化的隐蔽性。

3. **Webdriver**
`navigator.webdriver`设定为false，避免自动化工具设置为true。

4. **Headless**
只是将`User-Agent`的`HeadlessChrome`的改成`Chrome`，其他Headless特征没有更改，谨慎使用。

### 启用指纹功能的命令行参数

在启动浏览器时，通过命令行参数启用或自定义指纹和隐私保护功能：

| **参数** | **描述** | **可用值/示例** |
|---------|---------|---------------|
| **`--fingerprint`** | 指定指纹种子(seed)，启用后大部分指纹功能生效 | 32位整数 |
| **`--fingerprint-platform`** | 指定操作系统类型 | `windows`, `linux`, `macos` |
| **`--fingerprint-platform-version`** | 指定操作系统版本 | 不填时使用默认版本 |
| **`--fingerprint-brand`** | 指定 `User-Agent` 和 `User-Agent Data` 中的浏览器品牌 | Chrome, Edge, Opera, Vivaldi (默认Chrome) |
| **`--fingerprint-brand-version`** | 指定品牌的版本号 | 不填时使用默认版本 |
| **`--fingerprint-hardware-concurrency`** | 指定 CPU 核心数 | 整数值（不提供时由指纹种子随机生成） |
| **`--disable-non-proxied-udp`** | 指定 WebRTC 策略，默认是禁用非代理 UDP 连接 | 建议保持默认设置 |
| **`--lang`** | 设置浏览器的语言 | 语言代码（如 `zh-CN`） |
| **`--accept-lang`** | 设置浏览器接受的语言 | 语言代码（如 `zh-CN,en-US`） |

### **新增的 User-Agent 自定义命令行参数**

Chrome 131 新增了两个用于进阶自定义 `User-Agent` 和 `User-Agent Data` 的命令行参数：

- **`--fingerprint-brand`**
  - 指定在 `User-Agent` 和 `User-Agent Data` 中使用的浏览器品牌。
  - 支持的值：`Chrome`，`Edge`，`Opera`，`Vivaldi`，或自定义品牌名称。

- **`--fingerprint-brand-version`**
  - 指定指定品牌的版本号。
  - 默认值：`Chrome`，`Edge`，`Opera`，`Vivaldi` 都提供默认版本，也可以传入自定义版本。

这些参数增强了浏览器环境模拟的能力，适合自动化和测试场景。如果没有指定 `--fingerprint-brand`，将使用默认品牌。

## 使用示例

以下是几个常见使用场景的命令行示例：

### 基本使用（Linux 环境）

```bash
export TZ="America/Los_Angeles" && ./chrome --fingerprint=1000 --user-data-dir=/tmp/chromium/1000
```

### 定制`User-Agent`

```bash
chrome.exe --fingerprint=2023 --fingerprint-platform=macos --fingerprint-platform-version="15.2.0" --fingerprint-brand="Edge"  --user-data-dir=%TEMP%\chromium
```

## 用户交流

扫码加入QQ群与其他用户交流：

<img src="qq-group.png" alt="QQ群二维码" width="300">

## Credits

 * [Ungoogled Chromium](https://github.com/ungoogled-software/ungoogled-chromium)

 ## License

BSD-3-clause. See [LICENSE](LICENSE)