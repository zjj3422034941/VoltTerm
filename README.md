<div align="center">

# ⚡ VoltTerm

**面向 Windows 的轻量原生 SSH 客户端与现代终端模拟器**

[![Platform](https://img.shields.io/badge/Platform-Windows%2010%20%2F%2011%20x64-0078D4?style=flat-square&logo=windows)](https://github.com)
[![Version](https://img.shields.io/badge/Release-v0.8.3-2563EB?style=flat-square)](https://github.com)
[![Tech](https://img.shields.io/badge/C%2B%2B20-Qt%206.8%20Widgets%20%2B%20libvterm%20%2B%20libssh-41CD52?style=flat-square)](https://github.com)
[![License](https://img.shields.io/badge/License-Non--Commercial-orange?style=flat-square)](../LICENSE.txt)

原生 C++20 + Qt 6 Widgets（QPainter 直绘）打造，告别 Electron 高内存占用；<br>
延续经典终端操作习惯，原生支持 **多进程标签隔离**、**Windows 云盘级远程目录挂载**、**AI Agent 侧边栏** 与 **4K 高分屏原生渲染**。

</div>

---

## ✨ 核心亮点

- **🚀 原生直绘 & 多进程标签隔离**
  - 非 Electron / 非 WebView，终端画面由 `QPainter` 逐行直绘，配合行级哈希脏区与滚动位块搬运，高频刷屏与大输出依旧流畅。
  - 每个终端标签运行在独立子进程（`--terminal-host`）中：单个会话卡死、断网或异常崩溃**不会拖垮主窗口与其他标签页**；后台空闲标签自动压缩快照并修剪工作集，多标签常驻内存更低。
- **🖥️ 4K / 高分屏原生适配**
  - 原生支持 Windows 100% / 125% / 150% / 175% / 200% 缩放与多显示器混合 DPI 切换，行缓存严格 1:1 像素对齐，告别高分屏发虚、裁切与行距错位。
- **📁 Windows Cloud Files 远程文件夹挂载**
  - 基于 Windows 原生 Cloud Files API，一键将远端 SSH 服务器目录挂载为本地资源管理器文件夹，支持按需水合、双向实时同步（含大文件按需占位与 0 字节文件同步），无需额外第三方驱动。
- **🤖 内置 AI 侧边栏 & 现代 TUI 深度兼容**
  - 集成侧边 AI 终端面板，支持在远程服务器中直接运行 **Codex CLI / Claude Code / OpenCode / Hermes / Aider** 等 AI Agent 工具，支持备用屏历史回看。
  - 完整支持 `OSC 10/11` 配色查询、`DSR / DA1 / DA2` 终端能力应答、`DECSET 1004` 焦点上报、24-bit TrueColor 与 Braille 字符回退，完美呈现 TUI 动画与配色。
- **📦 现代 ZMODEM（`rz` / `sz`）体验**
  - 内置 `lrzsz`，下载同名文件自动保留原文件并递增编号（如 `file(1).txt`、`file(2).txt`），绝不静默覆盖。
  - 现代化目录/文件选择弹窗（支持桌面/下载/文档一键快捷跳转）与实时速率/ETA 传输进度条。
- **🔄 经典终端零成本迁移**
  - 原生支持导入 `.xsh` 会话文件、`.qbl` / `.qblx` 快捷命令集与 `.scs` 配色方案，菜单布局、快捷键与操作直觉无缝衔接。

---

## 🛠️ 功能一览

| 分类 | 功能特性 |
| :--- | :--- |
| **连接协议** | SSH（密码 / 公钥 / 键盘交互 / 跳板机 ProxyJump / 本地与远程端口转发）、Windows 本地 Shell（ConPTY，兼容 Win10/Win11） |
| **文件传输** | SFTP 图形化浏览与传输、Windows 云盘级远程目录挂载与同步、ZMODEM（`rz` / `sz`）自动防覆盖下载 |
| **终端引擎** | `libvterm` 核心、256 色 & 24-bit 真彩、备用屏（`vim` / `less` / `htop` / AI TUI）、鼠标事件上报、`DECSCUSR` 光标形状、Vim 逐行安全粘贴（Bracketed Paste） |
| **多语与编码** | 支持 `UTF-8` / `GBK` / `GB18030` / `Big5` / `Shift-JIS` / `EUC-KR` / 自动识别；中文双宽对齐与 IME 候选框光标跟随 |
| **效率工具** | 多标签 + 水平/垂直分屏、分组快捷命令条、关键词行级高亮、纯文本 / RTF / HTML 富文本复制、会话日志记录、全局查找 |
| **外观与安全** | 浅色 / 深色 / 跟随系统三档主题、主密码加密凭据库（`secrets.vault`）、空闲自动锁屏、主机密钥与用户密钥管理 |

---

## 📥 下载与安装

请前往本仓库的 **[Releases](../../releases)** 页面下载最新版本（当前版本 `v0.8.3`）：

- **安装版**：`VoltTerm-Setup-0.8.3.exe`（Inno Setup 安装程序，包含 Qt 6 运行时、ConPTY 与 `lrzsz`，自动创建桌面与开始菜单快捷方式）
- **便携版**：`VoltTerm-0.8.3-portable.zip`（绿色免安装，解压即用，不写注册表）

> **系统要求**：Windows 10 / Windows 11（64 位 x64）。覆盖升级安装前，请先关闭正在运行的 VoltTerm 进程。

---

## 🔨 从源码构建

### 环境要求

| 组件 | 推荐版本 |
| :--- | :--- |
| 操作系统 | Windows 10 / 11 x64 |
| Qt | Qt 6.8.3（MinGW 13.1 64-bit，含 `Core / Gui / Widgets / Network / PrintSupport / Sql / Svg`） |
| 编译器 | MinGW-w64 GCC 13.1（C++20） |
| 构建工具 | CMake 3.20+、Ninja |
| 打包工具 | Inno Setup 6（仅打包安装包时需要） |

### 外部依赖目录

第三方源码依赖默认放置在 `VOLT_DEPS_DIR`（默认 `E:/dev/third_party`）：

```text
third_party_deps/
├── libvterm/          # https://github.com/neovim/libvterm
├── WindTerm/          # https://github.com/kingToolbox/WindTerm (libssh)
└── openssl-install/   # OpenSSL 3.x (include/ + lib64/libcrypto.a)
```

### 编译与运行

```powershell
# 1. 配置 PATH（按本机 Qt 安装路径调整）
$env:PATH = "E:\Qt\6.8.3\mingw_64\bin;E:\Qt\Tools\mingw1310_64\bin;" + $env:PATH

# 2. 配置并编译
cmake -S . -B build -G Ninja `
      -DCMAKE_BUILD_TYPE=Release `
      -DCMAKE_PREFIX_PATH=E:/Qt/6.8.3/mingw_64 `
      -DVOLT_DEPS_DIR=E:/dev/third_party

cmake --build build --target voltterm -j 8
```

编译产物位于 `build/voltterm.exe`（构建脚本会自动复制所需的 `conpty.dll`、`OpenConsole.exe` 与 `lrzsz` 工具）。

### 打包发布

```powershell
# 生成安装包、便携版 zip 与 SHA256 校验文件（输出到 dist/）
powershell -NoProfile -ExecutionPolicy Bypass -File packaging\windows\package-inno.ps1 -Version 0.8.3
```

---

## 📂 项目目录结构

```text
VoltTerm/
├── app/                # GUI 应用层（主窗口、TerminalView、多进程隔离宿主、SFTP/ZMODEM/AI 面板、对话框）
├── core/               # 核心层（VtScreen、libssh/ConPTY 连接、凭据加密库、配置与会话模型）
├── packaging/windows/  # Windows 图标资源与 Inno Setup 打包脚本
├── tests/              # 自动化回归探针（终端渲染、粘贴、ZMODEM、云盘同步、隔离宿主等）
├── third_party/        # Windows 运行时组件（ConPTY、lrzsz）
└── CMakeLists.txt      # CMake 构建配置
```

---

## 📄 许可协议

本软件遵循 **VoltTerm 软件许可协议（非商业用途许可）**，详见仓库根目录的 [LICENSE.txt](../LICENSE.txt) 与第三方开源组件声明 [THIRD_PARTY_NOTICES.txt](../THIRD_PARTY_NOTICES.txt)：

- **个人非商业使用**：自然人可在个人学习、研究、技术评估及个人自用场景下免费安装和使用。
- **商业使用**：未经版权人事先书面授权，不得将本软件（含源码、安装包及衍生作品）用于任何商业行为或组织内部生产环境。
- **持久化使用**：本软件支持免费试用 15 天，如果想持久化使用请联系作者：`3422034941@qq.com`。
