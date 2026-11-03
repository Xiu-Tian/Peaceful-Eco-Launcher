# Peaceful Eco Launcher

**Peaceful Eco Launcher（PEL）** 是一款面向 Minecraft Java 版玩家的 Windows 启动器。它把游戏安装、实例管理、资源搜索与账户切换放在一个简洁的桌面界面中，并提供内置 DeepSeek 网页入口和启动日志辅助功能。

> 当前版本：**1.0.1 Alpha**。项目仍在持续开发中，部分资源下载能力会受平台授权和网络环境影响。

## 功能一览

- **安装和管理游戏版本**：获取 Minecraft 官方版本信息，安装游戏版本及 Fabric、Forge、NeoForge 等加载器，并管理多个游戏实例。
- **实例隔离**：为不同实例分别管理存档、模组和配置；支持调整游戏目录与隔离设置。
- **资源中心**：聚合搜索 Modrinth 与 CurseForge 资源，支持模组类型筛选、游戏版本和加载器匹配，以及资源购物车批量安装。
- **支持多类资源**：浏览模组、整合包、光影和资源包；支持导入 Modrinth 与 CurseForge 整合包。
- **多种账户方式**：支持 Microsoft 正版账户、离线账户和 LittleSkin（Yggdrasil）账户。
- **Java 管理**：检测本机 Java，并提供 Java 下载与安装入口。
- **DeepSeek 网页**：在启动器内打开 DeepSeek 网页，使用独立 WebView2 页面保存网页登录状态。可以手动复制最近一次游戏日志，复制内容会进行敏感信息脱敏；日志不会自动发送。
- **启动日志和诊断**：查看启动器与游戏相关日志，导出诊断日志以便排查问题。
- **首次运行环境引导**：原生引导程序检查 .NET Framework 4.8 及兼容版本和 WebView2 Runtime。缺失时，可从微软官方 HTTPS 地址下载并引导安装，同时验证安装程序的微软签名。
- **深浅色主题**：界面支持浅色和深色主题。

## 下载与安装

1. 前往 GitHub 仓库的 **Releases** 页面。
2. 下载最新发布中的 `PeacefulEcoLauncher.exe`。
3. 双击运行。若系统缺少必要运行环境，PEL 会提示并引导从微软官方地址下载安装。

运行环境检测和安装由不依赖 .NET 或 WebView2 的原生引导程序完成。安装程序由微软签名验证；是否需要管理员权限由官方安装程序决定。

## 资源下载说明

资源中心会联合展示 Modrinth 与 CurseForge 的搜索结果。Modrinth 资源支持读取所需前置并按兼容信息安装；CurseForge 资源会遵守作者和平台的分发限制。若某个文件不允许第三方启动器直接分发，PEL 会提示前往该项目的官方页面获取。部分 CurseForge 前置需要玩家根据项目说明确认。

光影和资源包下载后不会自动启用；具体效果还取决于 Minecraft 版本、加载器及相应运行组件。

## 自动更新

启动器已包含 GitHub Releases 更新检查、下载校验和替换回滚流程，并可在设置中控制自动检查与下载。**当前更新通道尚待本项目的公开 GitHub 仓库配置完成**；通道启用后，启动器将从 Release 下载更新，安装前由用户确认重启。

## 数据与隐私

- 游戏文件和启动器设置分开管理，启动器不会把自己的设置写进 Minecraft 游戏目录。
- DeepSeek 浏览器页与启动器功能接口隔离；复制日志是手动操作，PEL 不会自动把日志或聊天内容发送给 DeepSeek。
- 设置中的 DeepSeek API Key 是可选项，仅用于资源介绍翻译功能；不填写时会使用备用翻译服务或原始介绍。
- Microsoft 和第三方账户登录会与对应认证服务通信；账户凭据按启动器实现保存在本机。

## 系统要求

- Windows 10 或更高版本，x86 或 x64 处理器。
- 游戏运行需要合适版本的 Java。PEL 可以检测已有 Java，也可以协助下载。
- .NET Framework 4.8 及兼容版本与 Microsoft Edge WebView2 Runtime。缺少时可通过首次运行引导安装。
- 安装游戏、加载器、模组或整合包需要网络连接。

## 从源码构建

构建环境需要 Windows、Node.js 20 或更高版本，以及本机 .NET Framework 编译所需组件。首次构建时获取 WebView2 SDK、Roslyn 编译器和 Tiny C Compiler：

```powershell
node scripts/get-webview2.mjs
node scripts/get-roslyn.mjs
node scripts/get-tcc.mjs
node scripts/build-cs.mjs
```

构建产物输出到 `build/PeacefulEcoLauncher.exe`。启动器版本号统一配置在 `assets/version.txt`。

## 技术组成

- **桌面与启动流程**：Windows 原生 Bootstrapper + C# / .NET Framework 4.8
- **界面**：HTML、CSS、JavaScript
- **内置网页与界面宿主**：Microsoft WebView2
- **游戏资源**：Mojang 官方元数据、Modrinth 和 CurseForge 资源信息
- **更新分发**：GitHub Releases（更新通道配置完成后启用）

## 开发者

EMOCHAN · F1xSky
