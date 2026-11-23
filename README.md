# CSY Glimmer · 萤川 星野

一个粉色可爱风格的 Minecraft 启动器，把「装游戏」「装整合包」「开服务器」「管服务器」放在同一个软件里；桌面端用 Electron + React，内置网页面板与远程节点，手机或另一台电脑用浏览器也能管同一批服务器。

- **作者**：Mr.Zhang（张先生） · **联系方式**：通过公开仓库 Issue 反馈
- **性质**：个人学习与自用作品，未经作者许可禁止转载、分发、售卖或二次打包
- **适龄提醒**：本软件面向 18 岁以上用户，启动前只弹一次 18+ 提醒供你确认，不做实名认证、不校验年龄与身份

> 本软件不附带游戏本体，需要你自行拥有合法的 Minecraft 资源；与 Mojang、Microsoft 无任何关联。
>
> 安装包内不预置任何第三方音乐、壁纸或游戏素材：背景图运行时按需获取，背景音乐请自行放入 `config/bgm`。

## 下载与自动更新

- 源码仓库保持**私有**；只有打包好的 exe 与 `latest.json` 放在**公开的发布仓库**，朋友通过 Release 链接下载即可
- 客户端「关于 → 在线更新」填入发布仓库（`用户名/仓库名`），启动 6 秒后自动静默检查一次，也能手动点「检查更新」
- 发现新版本：显示更新说明 → 下载（进度条 + sha256 校验）→ 退出并自动替换 exe → 重新打开
- **更新只替换程序文件**：`%APPDATA%\\CSY_Glimmer` 下的 config（账号 / 微软凭据 / 面板密码）、games（实例 / 模组 / 存档）、servers（世界 / 备份）、runtime（Java）都不会被改动
- 发布流程：改代码 → 提交 → 打 tag（如 `v1.0.3`）→ GitHub Actions 自动构建并发布到公开仓库

## 一、启动器能做什么

**装游戏**

- 实时拉取官方版本清单（正式版 / 快照 / 历史版本都在，不写死列表），按需下载客户端 jar、库与资源文件，全部 SHA1 校验，断点可续传
- **自带 Java**：启动器打开时自动从 Adoptium / 清华镜像下载匹配的 JRE 到 `runtime/java`，不需要自己装 Java；也支持指定本机已有 Java
- 实例化：每个实例独立目录（mods / config / saves / natives），互不干扰
- 微软正版设备码登录 + 离线账号；令牌过期自动续期，凭据只存本地

**装内容**

- 整合包：支持 `.mrpack`、CurseForge `.zip`、MultiMC / Prism 实例、HMCL / PCL 导出包、纯 mods 压缩包，自动识别格式并落位
- Modrinth 整合包一键安装；模组 / 资源包 / 光影按游戏版本 + 加载器筛选
- **中英文都能搜**：输入「小地图」「优化」会自动翻译成对应英文关键词再检索

**更好看**

- 樱粉半透明主题：卡片透明度、背景模糊、圆角、字号、字体都能调
- 8 套内置可爱模板（樱花绯 / 暮色紫 / 薄荷星 / 夜樱黑 / 薰衣草 / 棉花糖 / 晴天蓝 / 奶油可可）
- 背景主色、文字颜色可自定义（取色器），也能上传自己的背景图
- 内置免费壁纸站：一键拉取必应每日壁纸，点一下就铺成半透明背景

**服务器（桌面 + 网页双端）**

- 支持 16 种服务端：Vanilla、Paper、Folia、Purpur、Spigot、Leaves、Fabric、Quilt、Forge、NeoForge、Mohist（墨端）、Arclight、CatServer、Velocity、Waterfall、BungeeCord
  - 自动下载安装：Vanilla / Paper / Folia / Leaves / Fabric / Quilt / Forge / Velocity / Waterfall
  - 源当前不可达时可「导入本地服务端」直接放 jar：Purpur / Spigot / BungeeCord / NeoForge / Mohist / Arclight / CatServer
- 生命周期：安装 / 启动 / 优雅停止 / 重启 / 崩溃自动重启
- 控制台实时日志、指令下发（stdin，无进程时自动降级 RCON）、玩家列表、踢人
- `server.properties` 可视化编辑、在线世界备份（自动跳过被锁文件）
- **automod 模组同步**：服务器目录里 `automod/{mods,config,scripts,datapacks}` 放好文件，一键同步到客户端实例；实例绑定服务器后，每次启动游戏前自动比对并补齐缺失模组与配置
- 远程节点：在目标机器 `npm run agent`，桌面端/网页端加节点即可统一管理；远程 automod 文件走 agent 拉取
- 网页面板：全中文、多用户、管理员 / 操作员 / 只读三级权限、WebSocket 实时日志、操作审计、新手引导

## 二、快速开始

```bash
npm install         # 国内网络如卡在 Electron 下载：
                    #   Windows: set ELECTRON_MIRROR=https://npmmirror.com/mirrors/electron/
                    #   macOS/Linux: export ELECTRON_MIRROR=https://npmmirror.com/mirrors/electron/
npm start           # 构建界面并启动桌面客户端
npm run dev         # 开发模式（Vite 热更新 + Electron 热重启）
```

### 一键启动脚本

`mc-launcher` 目录里内置两个双击即可运行的脚本：

| 脚本 | 作用 |
|---|---|
| `启动 CSY Glimmer.bat` | 双击启动启动器；首次会自动 `npm install`（缺依赖时），随后构建界面并拉起窗口 |
| `启动-数据放本目录.bat` | 同上，但把数据目录设为 `mc-launcher\data`，配置 / 游戏 / 服务器 / Java 都跟着文件夹走，方便整个搬走 |

两个脚本都会先检查 Node.js，缺失时会提示安装；启动失败会停在窗口里显示错误，不会一闪而过。

首次打开：

1. 阅读免责声明 → 勾选「已成年」→ 填写真实姓名与身份证号完成本机校验（不上传）
2. 「版本与实例」新建实例，或在「整合包」里导入 / 一键装
3. 回「启动主页」点启动游戏，第一次会自动下载版本文件与 Java

### 双端分工（2.1.1 起）

- **客户端**：启动游戏、实例与版本、整合包、模组、账号、外观设置；服务器只保留启停、控制台与玩家查看
- **网页端**：服务器完整管理——新建服务器、类型与版本、配置编辑、备份、automod 同步、节点与用户权限、审计

两端共用同一份数据目录（默认 `%APPDATA%\CSY_Glimmer`，可用 `CSY_GLIMMER_HOME` 覆盖），单独启动面板也能看到客户端创建的服务器。

### 网页面板

1.0.6 起，网页端服务器卡重新设计，启停/备份/配置等操作只更新内容区不整页刷新；服务器安装进度不再出现乱码，只推动进度条；配置页搜索与保存不再重建整页。

1.0.5 起，面板入口收进客户端「服务器」页的卡片：卡片直接显示网页端账号与初始密码，点「打开网页面板」会自动带上账号密码并复制初始密码；网页端改密后卡片只显示掩码，并可一键重置。网页端本身改为左侧导航 + 粉色玻璃卡片布局，设置、关于与客户端同源，账号菜单支持邮箱验证码绑定。

默认随启动器在 `http://127.0.0.1:27123` 开启（端口可在「外观与设置」改，被占用会自动顺延）。

- 首次启动创建管理员账号，写入 `config/panel/initial-credentials.txt`，登录后请立刻修改密码
- 也可单独运行：`npm run panel`
- 面板默认监听 `0.0.0.0`，局域网可访问；公网部署请自行加 HTTPS 反向代理

### 远程节点

```bash
# Windows
set AGENT_TOKEN=你的令牌
npm run agent

# macOS / Linux
AGENT_TOKEN=你的令牌 npm run agent
```

可选环境变量：`AGENT_PORT`（默认 8765）、`AGENT_HOST`、`CSY_GLIMMER_HOME`（节点数据目录）。

## 三、目录结构（配置、游戏、服务器分开放）

默认数据根目录：Windows `%APPDATA%\CSY_Glimmer`，可用环境变量 `CSY_GLIMMER_HOME` 指到任意位置（比如 D 盘）。

```
CSY_Glimmer/
├── config/                 配置与凭据（备份这个目录就够了）
│   ├── config.json         设置、账号、实例列表
│   ├── servers.json        服务器与节点列表
│   ├── appearance/         自定义背景图
│   ├── identity/           旧版本实名目录（1.0.3 起不再写入，可直接删除）
│   └── panel/              网页面板数据库与初始凭据
├── games/                  游戏文件（可以很大，独立备份/迁移）
│   ├── versions/ libraries/ assets/ meta/
│   ├── instances/          每个实例的 mods、config、saves、natives
│   └── modpacks/           下载中的整合包
├── servers/                每个服务器一个目录（server.jar、world、automod、backups）
├── runtime/java/           自动下载的 JRE
└── logs/
```

代码目录：

```
electron/   Electron 主进程与 preload（IPC 暴露面）
core/       纯 Node 核心：版本、启动、Java、账号、整合包、automod、服务器、RCON、ZIP、类型注册表
server/     网页面板后端 + 远程 agent
web/        网页面板前端（原生 ES Module，无构建步骤）
src/        启动器界面（React）
scripts/    校验脚本与开发脚本
```

## 四、封装成 exe

工程已内置 electron-builder 配置（`package.json > build`），两种做法：

**便携版（一个 exe，双击就能开，推荐自用）**

```bash
npm install --save-dev electron-builder
npm run pack:win            # 产物在 release/CSY-Glimmer-2.0.0-portable.exe
```

**安装版（NSIS，可自选安装目录）**

```bash
npm install --save-dev electron-builder
npm run pack:nsis           # 产物在 release/CSY-Glimmer-2.0.0-setup.exe
```

打包提示：

- 首次打包会下载 Electron / winCodeSign 等资源，国内网络建议先设置镜像：
  ```bash
  set ELECTRON_MIRROR=https://npmmirror.com/mirrors/electron/
  set ELECTRON_BUILDER_BINARIES_MIRROR=https://npmmirror.com/mirrors/electron-builder-binaries/
  ```
- 打完的 exe 运行时，数据依然按上文结构分在 `config / games / servers / runtime` 四个目录，不会混在一起
- 想让「便携版」把数据放在 exe 旁边（真正的绿色版），启动前设置环境变量 `CSY_GLIMMER_HOME` 指向 exe 同级的 `data` 目录即可

## 五、自检脚本

```bash
npm run verify:core         # 版本清单、安装规划、启动参数、ZIP、RCON、UUID、属性
npm run verify:java         # 真实下载 JRE 并执行 java -version，二次调用命中缓存
npm run verify:servertypes  # 16 类服务端枚举 + 实时版本 + Fabric/Paper 真实下载
npm run verify:modpack      # 四种整合包格式识别与导入 + 中英文搜索
npm run verify:automod      # automod 清单、本机补齐、远程 agent 拉取
npm run verify:panel        # 面板登录、角色权限、服务器 API、WebSocket、审计
npm run verify:agent        # 节点接入、远程建服/改配置/删除
npm run verify:server       # 真实下载服务端并开服、指令、RCON、备份、停止（约 1 分钟）
npm run verify              # 串行跑前七项
```

## 六、已知边界

- Forge / Quilt / Fabric 服务端通过官方安装器部署，首次安装要下载较多依赖，请耐心等待；Purpur、Spigot、BungeeCord、NeoForge、Mohist、Arclight、CatServer 的官方源在部分网络不可达，此时用「导入服务端」放本地 jar
- CurseForge 整合包的模组直链需要官方接口；接口不可达时会先导入配置并把待补清单写到 `curseforge-pending.json`
- 微软正版登录默认使用公共通道：每次打开客户端都会自动从公开启动器上游（Prism Launcher 官方仓库）拉取最新公共 Client ID，并用微软 devicecode 接口实测验证后缓存 12 小时；登录时若 ID 被注销（AADSTS700016）会自动换 ID 重试一次。微软并未对外提供“公共 ID 目录”，官方只提供应用注册与 OAuth 端点；也可以填自己的 Azure Client ID 覆盖默认值
- 备份是在线备份，运行中会跳过被系统锁定的文件；需要强一致请先停服
- 面板是 HTTP + HttpOnly Cookie 会话，公网部署请置于 HTTPS 反代之后

## 七、隐私与合规

- 登录凭据与微软令牌只写在本机 `config/` 目录，启动器不会向作者或任何第三方上传
- 本软件不做实名认证或年龄校验：仅在首次启动弹出 18+ 适龄提醒，勾选确认后即可使用，不收集身份证号、不判断年龄
- 面板与 agent 之间的令牌只保存在本地配置中，请勿把 `AGENT_TOKEN` 或面板端口暴露到公网

## License

MIT（仅限作者本人学习使用；未经许可禁止对外传播）