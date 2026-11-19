# Peaceful Eco Launcher

**Peaceful Eco Launcher（PEL）** 是面向 Minecraft Java 版的 Windows 启动器，提供游戏安装、实例管理、资源下载、Java 管理、账户登录和临时联机功能。

- **当前版本：1.1.4 Beta**
- **适用平台：Windows x64**（推荐 Windows 10 / 11）
- [下载发行版](https://github.com/Xiu-Tian/Peaceful-Eco-Launcher/releases) · [项目主页](https://github.com/Xiu-Tian/Peaceful-Eco-Launcher)

本页仅保留当前版本的更新公告。发行记录见 GitHub Releases；启动器内的更新包通过[夸克网盘](https://pan.quark.cn/s/30adaf0cf935#/list/share)下载。

## 1.1.4 Beta 更新

- 进一步优化下载引擎，改善线路切换与断点续传表现。
- 减少大文件的重复下载，改善部分整合包在最后几个文件上的等待时间。
- 修复下载缓存长期残留的问题。新版启动时会清理旧版遗留的共享缓存，下载成功后也会自动清理，不影响已安装的游戏和存档。
- 修复若干已知问题，提升启动器稳定性。

## 功能概览

共享下载器支持跨重试和重启的 HTTP 断点续传；实现、缓存清理和测试说明见 [HTTP 断点续传](docs/download-resume.md)。

Minecraft 下载器第一轮优化已处理 Fabric Maven 错误候选和慢元数据等待，并将客户端、Libraries、Assets 文件下载合并到共享限流池。任务会输出网络、排队、重试、检查点、SHA1 校验及安装耗时；实现边界、测试结果和后续计划见 [下载性能诊断](docs/download-performance-review.md)。

### 游戏、实例与 Java

- 安装和管理 Minecraft Java 版及 Fabric、Forge、NeoForge 等加载器。
- 每个实例使用独立游戏目录，分别管理模组、存档、截图、光影和材质包。
- 按游戏版本检测所需 Java，并优先选择兼容的本机 Java。
- 缺少合适 Java 时会说明所需主版本，可从启动器下载安装 Azul Zulu；下载页也提供 Eclipse Temurin 和 Alibaba Dragonwell。
- PEL 安装的 Java 保存在 `PeacefulEcoLauncher\Java` 目录中，可在本机 Java 列表中删除；其他位置的 Java 不提供此删除操作。
- 下载任务页面集中显示游戏、Java、模组及整合包任务的阶段、进度、速度和日志；支持的任务可以取消并查看历史记录。

### 游戏目录管理与导入

PEL 可以管理多个 `.minecraft` 目录，并合并显示其中的游戏版本。游戏列表会标出版本来源，也可以把版本迁移到其他目录。

在**存储位置 → 导入或找回游戏目录**中，可以检测 PCL2、HMCL 和 PEL 旧版游戏目录。PCL2 检测会读取其 `LaunchFolders` 注册表配置，以及可靠定位到程序目录时对应的 `PCL\Setup.ini`；不要求 `Setup.ini` 必须存在。升级后游戏不显示时，点击「检测目录」，勾选标为「PEL 旧版」的目录后导入。只登记原路径，不移动或删除文件；未检测到时仍可手动添加目录。

PCL2 快捷方式仅用于辅助定位程序目录，不会被直接当作 Minecraft 游戏目录。

### 资源中心

- 搜索 Modrinth 和 CurseForge 上的模组、整合包、光影及资源包，支持中文名称和常用中文别名。
- 按 Minecraft 版本、加载器和资源类型筛选，并查看可用文件及兼容信息。
- 购物车会分析资源组合、平台声明的必需前置和运行组件。确认游戏版本、加载器和安装清单后，即可创建新实例。
- 下载模组时可以选择保存文件的文件夹，例如桌面；这会保存所选模组文件，前置模组需另行下载。
- 支持导入 Modrinth / CurseForge 整合包，以及向模组、光影、材质包和存档管理页面拖入本地文件。
- 整合包导入时可从已添加目录中选择安装位置，也可以浏览并添加新目录；所选位置会记为下次导入的默认位置。

资源兼容性和可下载性以作者发布的文件及平台规则为准。CurseForge 作者关闭第三方分发时，PEL 与 PCL2 的做法一致：不用平台 API 给出的下载地址，而是按「文件 ID + 文件名」拼出官方媒体 CDN 直链直接下载，也就是在官网上点 Download 时浏览器拿到的同一个地址；安装前仍用平台返回的 SHA-1 和文件大小逐字节校验，校验不通过的文件不会被装进实例。只有直链无法构造（例如文件名缺失或非法）或下载校验失败时，才退回「在内置浏览器打开官方文件页 + 手动选择 JAR」的补下载通道。平台未声明的前置仍需参考作者说明。Fabric API 在能验证是同一文件时优先使用 CurseForge 下载源，失败后回退 Modrinth。

OptiFine 安装包支持分块传输等不提供 \`Content-Length\` 的响应。下载完成后会检查 JAR 结构与条目 CRC；无效网页、截断文件或校验失败的文件不会作为安装包使用。

### 键位配置

在**设置 → 键位配置管理**中，可以从已安装版本保存完整 `options.txt`，也可以浏览并导入外部 `options.txt` 或其他 `.txt` 文件作为预设。预设可以重命名、删除，并应用到单个或全部已安装版本。应用前会自动备份原文件；由于 Minecraft 将键位、画面、声音和语言等设置保存在同一文件中，应用预设会一并覆盖这些设置。导入文件只会新增预设，不会立即应用。

### 模组配置

在**设置 → 模组配置管理**中，选择来源实例并点击**扫描配置**，勾选需要保存的文件，再命名保存为预设。未识别的文件可手动确认归属。预设独立于游戏实例存放，可查看、重命名、覆盖保存或删除。恢复时只覆盖预设中选中的文件，并备份目标实例的原配置；游戏运行期间不能覆盖配置，批量应用只处理兼容实例。

### 账户与启动器工具

- 支持 Microsoft 正版账户、离线账户和 LittleSkin（Yggdrasil）等第三方认证账户。
- Microsoft 登录通过系统浏览器完成，不需要在 PEL 中输入 Microsoft 密码。
- 正版账号登录信息默认保存在启动器同级的 `Launcher` 文件夹。请勿分享该文件夹；打包发送启动器时也请将它排除。
- 若 Microsoft 账号尚未创建 Minecraft Java 版档案，登录时会提供 Minecraft 官网快捷入口；完成设置后返回 PEL 重新登录。
- 支持深色 / 浅色主题、启动器日志、诊断信息导出和反馈附件。
- 内置网页与启动器功能隔离；游戏日志需由用户手动复制，不会自动发送到网页。
- 启动时会检查进程完整性级别。检测到低完整性时才执行内置修复；检测到以管理员权限运行时，会尝试通过 Windows 桌面 Shell 或 Windows 提供的关联普通令牌重启。WebView2 不支持人工受限令牌，PEL 不再使用这种方式。若当前账户没有真实的普通权限令牌，启动器会提示使用普通 Windows 用户登录。临时修复脚本会自动删除，不修改系统权限设置。

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

在**设置 → 有可用更新时提示**中可关闭启动时的自动检查和提醒。发现可用更新时，确认后才会下载；也可以暂停提醒 7 天，并在设置中提前恢复。关闭或暂停提醒期间，仍可在主页手动检查更新。

游戏目录和启动器数据的实际位置可在启动器的**存储位置**中查看。默认游戏目录通常为 EXE 同级的 `.minecraft`，启动器数据通常保存在 EXE 同级的 `Launcher` 文件夹；如果该位置不可写，部分数据会使用用户缓存目录。

## 故障排查与日志

- **游戏无法启动或 Java 不兼容**：查看启动提示中的 Java 主版本要求，在 Java 页面扫描或安装合适版本。
- **联机失败**：确认房主的游戏和房间仍在运行、游戏端口填写正确，并在联机页刷新状态。公共中转不可用时，可稍后重试。
- **启动器或界面初始化失败**：查看 `Launcher\logs\bootstrap.log`、`Launcher\logs\startup-latest.txt` 和 `Launcher\logs\web.log`。
- **诊断 WebView2 图形兼容问题**：完全退出 PEL 后，从 PowerShell 以 `PeacefulEcoLauncher.exe --pel-diagnostic-no-gpu` 启动一次。此参数只为本次 WebView2 启动传入 `--disable-gpu`，用于判断故障是否与 GPU/驱动有关，不会保存设置；将最新的 `Launcher\logs\launcher-*.log`、`launcher-errors.log` 和 `startup-latest.txt` 一并提供。
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

## GitHub 发布与自动更新

PEL 启动时优先读取 GitHub 的 [静态更新清单](https://raw.githubusercontent.com/Xiu-Tian/Peaceful-Eco-Launcher/main/assets/update-manifest.json)，不可用时回退 GitHub Releases API。发现新版后点击「立即更新」，在内置浏览器的[夸克分享页](https://pan.quark.cn/s/30adaf0cf935#/list/share)手动下载对应的 EXE。仅接受较新版本，并按 GitHub 发布信息校验 SHA-256 和 EXE 产品版本；文件大小仅用于进度展示和下载上限检查，不作为文件身份依据。

夸克网页实际开始下载时，PEL 会自动切到「下载与任务」；总大小未知时不显示百分比。点击「立即更新」即授权校验通过后由更新助手自动替换、重启并检查首屏；新版本启动失败会尝试恢复旧版。有游戏任务运行时不会强制重启，可稍后手动安装。若下载由夸克客户端接管，PEL 无法读取客户端进度，请下载后选择「导入更新包」，并在校验通过后确认安装。

发布新版时按以下顺序操作：

1. 将 `assets/version.txt` 改为新版本号，并在本文件顶部添加完全匹配的标题 `## <版本号> 更新` 和更新内容。
2. 提交并推送版本号与 README 更新到 GitHub 的 `main` 分支，然后在项目目录运行 `npm run build`。
3. 构建会生成 `build\PeacefulEcoLauncher.exe` 和更新后的 `assets\update-manifest.json`。清单会自动写入版本号、更新说明、下载地址、文件大小和 EXE 的 SHA-256。
4. 在 GitHub 仓库的 **Releases → Draft a new release** 创建发行版：标签为版本号前加 `v`（版本号中的空格替换为连字符），标题使用 `PeacefulEcoLauncher <版本号>`。上传构建产物 `build\PeacefulEcoLauncher.exe`，资产名称必须保持为 **`PeacefulEcoLauncher.exe`**；仅 Alpha / Beta 版勾选 **Set as a pre-release**，稳定版不勾选，然后发布 Release，不能留作 Draft。
5. 把**同一个构建产物**放进固定夸克分享目录，确认可下载后，再把构建生成的 `assets\update-manifest.json` 推送到 `main`。GitHub 资产和夸克文件必须逐字节一致，不能用同版本号重新构建的另一份 EXE。
6. 在普通用户可写的独立目录中，用已支持夸克更新的较旧 PEL 分别验证内置下载和手动导入，不要直接在带沙盒权限限制的构建目录里验证 EXE 替换。仍使用旧更新机制的版本需要先手动换到支持夸克更新的版本；清单保留原 GitHub 资产字段以兼容已有检测和 API 回退。

每次发布都要提高 `assets/version.txt` 的版本号，并用相同版本号的 README 标题生成更新说明。不要手工改清单里的 SHA-256 或资产大小，也不要把 EXE 重命名后上传。构建脚本生成的是稳定资产名 `PeacefulEcoLauncher.exe`；带版本号的本地副本不能代替该 Release 资产。

中文资源名称索引及搜索行为参考 PCL-CE。相关来源与 Apache License 2.0 文本随构建产物提供，详见 `PCL-CE-SEARCH-NOTICE.txt` 和 `PCL-CE-APACHE-2.0.txt`。

## 作者

**EMOCHAN · F1xSky**

感谢 Minecraft、Modrinth、CurseForge、PCL-CE、EasyTier 及相关开源项目和资源作者。
