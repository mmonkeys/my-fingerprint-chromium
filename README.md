# fingerprint-chromium

[中文文档](README-ZH.md)

*A fingerprint browser based on `Ungoogled Chromium`.*

## Installation and Usage

### Download

Please download the version suitable for your system from the links below. Each major version of Chromium is compiled into a corresponding release. Choose the appropriate version for your operating system:

| **Version**      | **Source Code**                                                                                      | **Windows**                                                                                   | **Linux**                                                                                   |
|------------------|------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------|
| **Chrome 130**   | [130.0.6723.116](https://github.com/adryfish/fingerprint-chromium/tree/130.0.6723.116)               | [Installer](https://github.com/adryfish/fingerprint-chromium/releases/download/130.0.6723.116/ungoogled-chromium_130.0.6723.116-1.1_installer_x64.exe) <br> [ZIP](https://github.com/adryfish/fingerprint-chromium/releases/download/130.0.6723.116/ungoogled-chromium_130.0.6723.116-1.1_windows_x64.zip) | [130.0.6723.116-1_linux.tar.xz](https://github.com/adryfish/fingerprint-chromium/releases/download/130.0.6723.116/ungoogled-chromium_130.0.6723.116-1_linux.tar.xz) |
| **Chrome 129**   | [129.0.6668.100](https://github.com/adryfish/fingerprint-chromium/tree/129.0.6668.100)               | [Installer](https://github.com/adryfish/fingerprint-chromium/releases/download/129.0.6668.100/ungoogled-chromium_129.0.6668.100-1.1_installer_x64.exe) <br> [ZIP](https://github.com/adryfish/fingerprint-chromium/releases/download/129.0.6668.100/ungoogled-chromium_129.0.6668.100-1.1_windows_x64.zip) | [129.0.6668.100-1_linux.tar.xz](https://github.com/adryfish/fingerprint-chromium/releases/download/129.0.6668.100/ungoogled-chromium_129.0.6668.100-1_linux.tar.xz) |

---

You can find the compiled versions for each major Chromium release on the GitHub Release page. Download the appropriate file for your platform.

### Build from Source

Refer to the [`ungoogled-chromium`](https://github.com/ungoogled-software/ungoogled-chromium/blob/master/docs/building.md) documentation. Simply replace the `ungoogled-chromium` submodule URL with the `fingerprint-browser` repository URL.

---

## Features

### Fingerprinting Features

| **Fingerprint**                 | **Description**                                                                                          | **Command Line Arguments**                                                      |
|-----------------------------------------|----------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------|
| **User-Agent**                          | Modify the browser's `User-Agent`, including `navigator.userAgent`, `navigator.platform`, `navigator.userAgentData`, and Client Hints | `--fingerprint-platform` <br>`--fingerprint-platform-version`                  |
| **Audio**                | Obfuscate or spoof audio fingerprint data                                                                | `--fingerprint` (activated when fingerprint seed is enabled)                    |
| **Plugin**               | Modify plugin-related features                                                                           | `--fingerprint` (activated when fingerprint seed is enabled)                    |
| **Hardware**             | Customize hardware parameters such as CPU cores and memory size                                          | `--fingerprint` <br> `--fingerprint-hardware-concurrency`                       |
| **Font**                 | Modify system font information                                                                           | `--fingerprint` (activated when fingerprint seed is enabled)                    |
| **Canvas Image Data Noise**             | Add noise to canvas image data, modifying up to 10 pixels to interfere with fingerprinting               | `--fingerprinting-canvas-image-data-noise`                                      |
| **Canvas MeasureText Noise**            | Scale `Canvas::measureText()` output by a random factor between `-0.0003%` and `0.0003%`, recalculated at each document initialization | `--fingerprinting-canvas-measuretext-noise`                                    |
| **ClientRects Noise**                   | Scale `getClientRects()` and `getBoundingClientRect()` output by a random factor between `-0.0003%` and `0.0003%`, recalculated at each document initialization | `--fingerprinting-client-rects-noise`                                          |
| **WebRTC Policy**                       | Disable non-proxied UDP connections by default, preventing real IP address leaks via WebRTC              | `--disable-non-proxied-udp` (enabled by default)                                |
| **Language Support**                    | Set the browser language and accepted languages                                                          | `--lang` (set browser language) <br> `--accept-lang` (set accepted languages)   |
| **Timezone Support**                    | Set the browser timezone                                                                                 | `TZ` environment variable (e.g., `TZ=Asia/Shanghai`)                            |

---

### Automation Features

**Optimized for automation scenarios, offering the following features:**

1. **Fake Shadow DOM Support**  
   Adds the `fakeShadowRoot` property, equivalent to the `shadowRoot` property, enabling access to Closed Shadow Root for easier automation handling.

2. **Avoid CDP Detection**  
   Prevents Chrome DevTools Protocol (CDP) detection when invoking `Runtime.enable`, enhancing stealthiness for automation tools.

---

### Enabling Fingerprint Features with Command Line Arguments

You can enable or customize fingerprinting and privacy protection features by passing command line arguments when launching the browser:

| **Command Line Argument**                  | **Description**                                                                                  |
|--------------------------------------------|--------------------------------------------------------------------------------------------------|
| **`--fingerprint`**                        | Specify the fingerprint seed (seed). Most fingerprint features are activated when this is set.   |
| **`--fingerprint-platform`**               | Specify the operating system type: `windows`, `linux`, or `macos`.                              |
| **`--fingerprint-platform-version`**       | Specify the operating system version. Defaults to the browser's default version if unspecified. |
| **`--fingerprint-hardware-concurrency`**   | Specify the number of CPU cores. If unspecified, this is randomly generated based on the seed.  |
| **`--fingerprinting-canvas-image-data-noise`** | Enable canvas image data noise to interfere with fingerprinting.                                |
| **`--fingerprinting-canvas-measuretext-noise`** | Enable proportional scaling noise for canvas `measureText()` fingerprints.                     |
| **`--fingerprinting-client-rects-noise`**  | Enable proportional scaling noise for `getClientRects()` and `getBoundingClientRect()`.         |
| **`--disable-non-proxied-udp`**            | Specify WebRTC policy. Default: disable non-proxied UDP connections (recommended to leave unset).|
| **`--lang`** <br> **`--accept-lang`**      | Set the browser language.                                                                       |

## Credits

 * [Ungoogled Chromium](https://github.com/ungoogled-software/ungoogled-chromium)

 ## License

BSD-3-clause. See [LICENSE](LICENSE)