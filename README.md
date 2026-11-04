# Peaceful Eco Launcher

**Peaceful Eco Launcher（PEL）** 是面向 Minecraft Java 版的 Windows 启动器，提供游戏安装、实例管理、资源下载、Java 管理、账户登录和临时联机功能。

- **当前版本：1.0.4 Beta**
- **适用平台：Windows x64**（推荐 Windows 10 / 11）
- [下载发行版](https://github.com/Xiu-Tian/Peaceful-Eco-Launcher/releases) · [项目主页](https://github.com/Xiu-Tian/Peaceful-Eco-Launcher)

## 1.0.4 Beta 更新

- 优化资源中心的中文名称和常用别名搜索。
- 优化联机房间成员信息与连接状态显示，展示电脑主机名及直连或中转状态。
- 修复若干问题，提升启动器稳定性。

## 功能概览

### 游戏、实例与 Java

- 安装和管理 Minecraft Java 版及 Fabric、Forge、NeoForge 等加载器。
- 每个实例使用独立游戏目录，分别管理模组、存档、截图、光影和材质包。
- 按游戏版本检测所需 Java，并优先选择兼容的本机 Java。
- 缺少合适 Java 时会说明所需主版本，可从启动器下载安装 Azul Zulu；下载页也提供 Eclipse Temurin 和 Alibaba Dragonwell。
- PEL 安装的 Java 保存在 `PeacefulEcoLauncher\Java` 目录中，可在本机 Java 列表中删除；其他位置的 Java 不提供此删除操作。
- 下载任务页面集中显示游戏、Java、模组及整合包任务的阶段、进度、速度和日志；支持的任务可以取消并查看历史记录。

### 游戏目录管理与导入

PEL 可以管理多个 `.minecraft` 目录，并合并显示其中的游戏版本。游戏列表会标出版本来源，也可以把版本迁移到其他目录。

在**存储位置**中可以手动添加目录，或检测 PCL2 / HMCL 的游戏目录。PCL2 检测会读取其 `LaunchFolders` 注册表配置和 `PCL\Setup.ini` 中的当前目录设置；不要求 `Setup.ini` 必须存在。检测只读取原启动器配置，不会修改或移动原文件。每个检测结果由用户选择后再导入；配置缺失时发现的 `.minecraft` 目录只作为候选项展示，不会被误认为已配置目录。

### 资源中心

- 搜索 Modrinth 和 CurseForge 上的模组、整合包、光影及资源包，支持中文名称和常用中文别名。
- 按 Minecraft 版本、加载器和资源类型筛选，并查看可用文件及兼容信息。
- 购物车可分析资源组合、必需前置和运行组件，确认安装方案后创建新实例。
- 下载模组时可以选择保存文件的文件夹，例如桌面；这会保存所选模组文件，前置模组需另行下载。
- 支持导入 Modrinth / CurseForge 整合包，以及向模组、光影、材质包和存档管理页面拖入本地文件。

资源兼容性和可下载性以作者发布的文件及平台规则为准。若平台或作者不允许启动器分发文件，请打开资源的官方页面获取。

### 账户与启动器工具

- 支持 Microsoft 正版账户、离线账户和 LittleSkin（Yggdrasil）等第三方认证账户。
- Microsoft 登录通过系统浏览器完成，不需要在 PEL 中输入 Microsoft 密码。
- 支持深色 / 浅色主题、启动器日志、诊断信息导出和反馈附件。
- 内置网页与启动器功能隔离；游戏日志需由用户手动复制，不会自动发送到网页。
- 如果启动检测发现启动器处于异常的低完整性级别，会自动执行内置修复流程；用户无需手动点击修复 CMD。

## 临时联机

PEL 联机目前支持 **Windows x64 和 Minecraft Java 版**。房主创建房间并分享邀请码，好友加入后在 Minecraft 多人游戏中使用 PEL 提供的本地连接地址。

### 房主

1. 在 Minecraft 单人世界中选择**对局域网开放**，或启动本地 Java 服务端。
2. 在 PEL 联机页填写游戏实际端口。局域网开放时，端口可能不是 `25565`。
3. 创建联机房间，并把邀请码分享给好友。
4. 保持游戏世界、房间和 PEL 运行。

### 好友

1. 在 PEL 联机页粘贴完整邀请码并加入房间。
2. 在 Minecraft 多人游戏中添加 PEL 显示的连接地址。
3. 确保双方的 Minecraft 版本和模组配置兼容。

联机优先尝试 P2P 直连，无法直连时使用配置的中转节点。房间状态显示成员的电脑主机名和连接状态（直连或中转），不显示虚拟 IP。房间成员代表加入临时网络的电脑，不代表已进入 Minecraft 世界的玩家。关闭 PEL 时会结束联机桥接与 EasyTier 进程。

离线（非正版）玩家加入局域网世界时，房主可能需要使用 **mcwifipnp（LAN World Plug-n-Play / 更高级联机设置）** 并按需配置正版验证。联机页面提供资源下载入口；下载时请匹配 Minecraft 版本和加载器。

邀请码包含房间密钥，请只分享给信任的人。公共中转节点的可用性会受网络和节点状态影响。

## 下载与首次运行

1. 从 [Releases 页面](https://github.com/Xiu-Tian/Peaceful-Eco-Launcher/releases) 下载 `PeacefulEcoLauncher.exe`。
2. 将程序放在准备长期使用的文件夹中，再从资源管理器启动。
3. 按提示选择账户和游戏目录；也可以从存储位置导入已有目录。
4. 安装游戏，确认 Java 版本后启动。

启动器会检查 .NET Framework 4.8 和 WebView2 Runtime。系统缺少所需组件时，启动器会提示处理方式。普通玩家使用发行版 EXE 即可，无需安装 Node.js。

游戏目录和启动器数据的实际位置可在启动器的**存储位置**中查看。默认游戏目录通常为 EXE 同级的 `.minecraft`，启动器数据通常保存在 EXE 同级的 `Launcher` 文件夹；如果该位置不可写，部分数据会使用用户缓存目录。

## 故障排查与日志

- **游戏无法启动或 Java 不兼容**：查看启动提示中的 Java 主版本要求，在 Java 页面扫描或安装合适版本。
- **联机失败**：确认房主的游戏和房间仍在运行、游戏端口填写正确，并在联机页刷新状态。公共中转不可用时，可稍后重试。
- **启动器或界面初始化失败**：查看 `Launcher\logs\bootstrap.log`、`Launcher\logs\startup-latest.txt` 和 `Launcher\logs\web.log`。
- **联机桥接失败**：查看 `Launcher\multiplayer\logs\bridge.log`、`easytier.err.log` 和 EasyTier 日志。
- **提交反馈**：通过启动器内的反馈入口描述复现步骤，并按需附上诊断日志或截图。发送前请确认附件内容适合分享。

## 开发者构建

在 Windows x64 环境安装 Node.js 20 或更高版本，并确保网络可访问后，在项目目录运行：

```powershell
npm run setup:vendor
node scripts/get-tcc.mjs
npm run build
```

构建产物为 `build\PeacefulEcoLauncher.exe`。构建脚本会下载所需的 WebView2、Roslyn 和 TinyCC 构建依赖；这些构建工具不需要随发行版提供。

中文资源名称索引及搜索行为参考 PCL-CE。相关来源与 Apache License 2.0 文本随构建产物提供，详见 `PCL-CE-SEARCH-NOTICE.txt` 和 `PCL-CE-APACHE-2.0.txt`。

## 作者

**EMOCHAN · F1xSky**

感谢 Minecraft、Modrinth、CurseForge、PCL-CE、EasyTier 及相关开源项目和资源作者。
