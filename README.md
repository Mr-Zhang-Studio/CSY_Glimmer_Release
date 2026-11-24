# CSY Glimmer · 萤川 星野

粉色可爱风格的 Minecraft 启动器：装游戏、装整合包、开服务器、管服务器都在同一个软件里。桌面端是 Electron + React，内置网页面板与远程节点，手机或另一台电脑用浏览器就能照看同一批服务器。

- **当前版本**：1.0.1
- **作者**：Mr.Zhang（张先生） · **联系方式**：ab.c@aliyun.com
- **性质**：个人学习与自用作品，未经作者许可禁止转载、分发、售卖或二次打包
- **适龄提醒**：面向 18 岁以上用户，启动前只弹一次提醒供确认，不做实名认证、不校验年龄与身份

> 本软件不附带游戏本体，需要你自行拥有合法的 Minecraft 资源；与 Mojang、Microsoft 无任何关联。
>
> 安装包内不预置第三方音乐、壁纸或游戏素材：背景图运行时按需获取，背景音乐自行放入 `config/bgm`。

## 下载与安装

- 源码仓库保持**私有**，公开的发布仓库只放打包好的 exe、便携 zip 与 `latest.json`
- 便携版一个 exe 双击即用，不需要安装；数据目录默认 `%APPDATA%\CSY_Glimmer`
- 也可以在公开 Release 里下载 zip 备份一份，解压后与 exe 用法相同

## 一、启动器能做什么

**装游戏**

- 实时拉取官方版本清单（正式版 / 快照 / 历史版本都在，不写死列表），按需下载客户端 jar、库与资源文件，全部 SHA1 校验，断点可续传
- **自带 Java**：打开时自动从 Adoptium / 清华镜像下载匹配的 JRE 到 `runtime/java`，不需要自己装 Java；也支持指定本机已有 Java
- 实例化：每个实例独立目录（mods / config / saves / natives），互不干扰
- 微软正版设备码登录 + 离线账号；令牌过期自动续期，凭据只存本地

**装内容**

- 整合包：支持 `.mrpack`、CurseForge `.zip`、MultiMC / Prism 实例、HMCL / PCL 导出包、纯 mods 压缩包，自动识别格式并落位
- Modrinth 整合包一键安装；模组 / 资源包 / 光影按游戏版本 + 加载器筛选
- **中英文都能搜**：输入「小地图」「优化」会自动翻译成对应英文关键词再检索

**更好看**

- 樱粉半透明主题：卡片透明度、背景模糊、圆角、字号、字体都能调
- 8 套内置模板（樱花绯 / 暮色紫 / 薄荷星 / 夜樱黑 / 薰衣草 / 棉花糖 / 晴天蓝 / 奶油可可）
- 背景主色、文字颜色可自定义，也能上传自己的背景图；内置免费壁纸站，一键铺成半透明背景
- 主页有小屋 3D 皮肤、今日心情、小屋速览与常用入口；点击全站有低密度樱花粒子
- 下载浮窗是独立的桌面小窗：一圈樱花随进度旋转，可以拖到桌面任意位置，位置会记住

**服务器（桌面 + 网页双端）**

- 支持 16 种服务端：Vanilla、Paper、Folia、Purpur、Spigot、Leaves、Fabric、Quilt、Forge、NeoForge、Mohist（墨端）、Arclight、CatServer、Velocity、Waterfall、BungeeCord
  - 自动下载安装：Vanilla / Paper / Folia / Leaves / Fabric / Quilt / Forge / Velocity / Waterfall
  - 网页端支持「一键开服」（先选类型与版本，再填端口与内存）与「导入服务器包」（上传 zip，自动解压、识别核心 jar 与 server.properties，保留世界与配置）
  - 源不可达时可「导入本地服务端」直接放 jar：Purpur / Spigot / BungeeCord / NeoForge / Mohist / Arclight / CatServer
- 生命周期：安装 / 启动 / 优雅停止 / 重启 / 崩溃自动重启；安装途中可随时中止
- 控制台实时日志、指令下发（stdin，无进程时自动降级 RCON）、玩家列表、踢人
- `server.properties` 可视化编辑、在线世界备份、备份文件可打开目录或删除
- **automod 模组同步**：服务器目录 `automod/{mods,config,scripts,datapacks}` 放好文件，一键同步到客户端实例；实例绑定服务器后，启动游戏前自动比对并补齐缺失模组与配置
- 远程节点：目标机器 `npm run agent`，桌面端 / 网页端加节点即可统一管理
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

| 脚本 | 作用 |
|---|---|
| `启动 CSY Glimmer.bat` | 双击启动启动器；缺依赖时自动 `npm install`，随后构建界面并拉起窗口 |
| `启动-数据放本目录.bat` | 同上，但把数据目录设为 `mc-launcher\data`，配置 / 游戏 / 服务器 / Java 都跟着文件夹走 |

两个脚本都会先检查 Node.js，缺失时提示安装；启动失败会停在窗口里显示错误。

### 双端分工

- **客户端**：启动游戏、实例与版本、整合包、模组、账号、外观设置，以及服务器启停、控制台与玩家查看
- **网页端**：服务器完整管理——新建服务器、类型与版本、配置编辑、备份、automod 同步、节点与用户权限、审计

两端共用同一份数据目录（默认 `%APPDATA%\CSY_Glimmer`，可用 `CSY_GLIMMER_HOME` 覆盖），单独启动面板也能看到客户端创建的服务器。

### 网页面板

- 默认随启动器在 `http://127.0.0.1:27123` 开启（端口可在「设置」改，被占用会自动顺延）
- 首次启动创建管理员账号，写入 `config/panel/initial-credentials.txt`，登录后请立刻修改密码
- 面板入口收在客户端「开服小站」页的卡片：卡片显示网页端账号与初始密码，点「打开网页面板」会自动带上账号密码并复制初始密码；网页端改密后卡片只显示掩码，并可一键重置
- 也可单独运行：`npm run panel`；默认监听 `0.0.0.0`，局域网可访问，左下角可一键复制面板地址
- 登录页是大字欢迎 + 居中登录卡；退出客户端后删除 `config/panel` 目录可恢复初始管理员（只在本机有效）

### 远程节点

```bash
# Windows
set AGENT_TOKEN=你的令牌
npm run agent

# macOS / Linux
AGENT_TOKEN=你的令牌 npm run agent
```

可选环境变量：`AGENT_PORT`（默认 8765）、`AGENT_HOST`、`CSY_GLIMMER_HOME`（节点数据目录）。

## 三、目录结构

默认数据根目录：Windows `%APPDATA%\CSY_Glimmer`，可用环境变量 `CSY_GLIMMER_HOME` 指到任意位置。

```
CSY_Glimmer/
├── config/                 配置与凭据（备份这个目录就够了）
│   ├── config.json         设置、账号、实例列表
│   ├── servers.json        服务器与节点列表
│   ├── appearance/         自定义背景图与本地图库
│   ├── skins/              本地皮肤
│   └── panel/              网页面板数据库与初始凭据
├── games/                  游戏文件（可以很大，独立备份/迁移）
│   ├── versions/ libraries/ assets/ meta/
│   ├── instances/          每个实例的 mods、config、saves、natives
│   └── modpacks/           下载中的整合包
├── servers/                每个服务器一个目录（server.jar、world、automod、backups）
├── backups/                实例备份 zip
├── runtime/java/           自动下载的 JRE
└── logs/
```

代码目录：

```
electron/   Electron 主进程与 preload（含桌面下载浮窗）
core/       纯 Node 核心：版本、启动、Java、账号、整合包、automod、服务器、RCON、ZIP、类型注册表
server/     网页面板后端 + 远程 agent
web/        网页面板前端（原生 ES Module，无构建步骤）
src/        启动器界面（React）
scripts/    校验脚本与开发脚本
```

## 四、封装成 exe

工程已内置 electron-builder 配置（`package.json > build`）：

```bash
npm run pack:win     # 便携版，产物在 release/CSY_Glimmer_<版本>.exe
npm run pack:nsis    # 安装版，可自选安装目录
```

打包提示：

- 首次打包会下载 Electron / winCodeSign 等资源，国内网络建议先设镜像：
  ```bash
  set ELECTRON_MIRROR=https://npmmirror.com/mirrors/electron/
  set ELECTRON_BUILDER_BINARIES_MIRROR=https://npmmirror.com/mirrors/electron-builder-binaries/
  ```
- 数据仍按 `config / games / servers / runtime` 四个目录分开，不会混在一起
- 想让便携版把数据放在 exe 旁边（绿色版），启动前把 `CSY_GLIMMER_HOME` 指向 exe 同级的 `data` 目录

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

- Forge / Quilt / Fabric 服务端通过官方安装器部署，首次安装要下载较多依赖；Fabric / Quilt 的版本列表走 BMCLAPI 镜像，安装器清单同时尝试官方与镜像再逐个候选探测；Purpur、Spigot、BungeeCord、NeoForge、Mohist、Arclight、CatServer 的官方源在部分网络不可达，此时用「导入服务器包」放 zip 或「导入本地服务端」放 jar
- CurseForge 整合包的模组直链需要官方接口；接口不可达时会先导入配置并把待补清单写到 `curseforge-pending.json`
- 微软正版登录默认使用公共通道：每次打开客户端都会从公开启动器上游（Prism Launcher 官方仓库）拉取公共 Client ID，用微软 devicecode 接口实测验证后缓存 12 小时；登录时若 ID 被注销（AADSTS700016）会自动换 ID 重试一次，也可以填自己的 Azure Client ID 覆盖默认值
- 备份是在线备份，运行中会跳过被系统锁定的文件；需要强一致请先停服
- 面板是 HTTP + HttpOnly Cookie 会话，公网部署请置于 HTTPS 反代之后

## 七、隐私与合规

- 登录凭据与微软令牌只写在本机 `config/` 目录，启动器不会向作者或任何第三方上传
- 本软件不做实名认证或年龄校验：仅在首次启动弹出 18+ 提醒，勾选确认后即可使用，不收集身份证号、不判断年龄
- 面板与 agent 之间的令牌只保存在本地配置中，请勿把 `AGENT_TOKEN` 或面板端口暴露到公网

## License

MIT（仅限作者本人学习使用；未经许可禁止对外传播）