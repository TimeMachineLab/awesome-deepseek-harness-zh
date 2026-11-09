# DeepSeek Harness 插件安装教程与精选插件（2026）

> 返回 [DeepSeek Harness 中文使用指南](../README.md) · 最后核对：2026-10-23（dsh `0.2.1-rc`）· 安装方法依据官方 `apps/cli/reference`、`docs/user/guide/plugin-market.md`

dsh 的口号是「万物皆插件」：模型适配、工具、界面、记忆都是插件。**一个插件就是一个 npm 包**，插件按 profile（配置档）安装，Web 界面用的是 `web` 这个 profile。

## 怎么安装插件

**命令行：**

```bash
# 从 npm 安装到 Web 界面用的 profile
dsh plugin --profile web add @作者/插件包名

# 从 GitHub 仓库安装（这个例子装到 tui profile）
dsh plugin --profile tui add github:deepseek-harness/turtle-ui

# 卸载
dsh plugin --profile web remove 插件包名
```

- 其他 pnpm 子命令会被原样转发，比如 `update`。
- 从 Git 安装、而且带构建脚本的插件，需要在配置里加一条 `allowBuilds`，dsh 会在命令行里提示具体要加什么。
- 插件声明了它支持的 dsh 版本（`engines.dsh`），版本不匹配时会拒绝安装。`allow-version ... --accept-risk` 可以强制放行，但**风险自负**。

**Web 界面：**

- 左侧边栏的 **Plugins** 页面管理已安装的插件，以及默认关闭的官方插件包。
- Settings → Built-in plugins 可以看内置插件清单。

**插件市场：**

- dsh **默认不带任何插件市场源**。打开实验功能「Custom plugin markets」后会多一个 **Discover** 标签页，在里面添加市场索引地址（建议用 `https:` 开头的）。
- 社区维护的可视化市场见下面「插件市场与发现」分类。第三方市场都是**非官方**的，安装前看清作者和代码。

> ⚠️ 插件会以你的权限运行代码。只装来源清楚、近期有维护的插件，最好在虚拟机或容器里使用 dsh（官方建议）。

## 精选插件

收录标准：开源、与 dsh 明确相关、近两个月内有更新（教程资料不限）。**不收录**破甲 / 越狱、逆向接口、来源不明的「免 Key 免费模型」、借用他人订阅账号的插件。想推荐插件？见 [贡献指南](../CONTRIBUTING.md)。

<!-- BEGIN:projects -->
> 星数和更新时间截至 2026-11-09，每周自动刷新。

### 桌面端与启动器

| 项目 | 说明 | ⭐ | 最近更新 |
|---|---|--:|---|
| [anywhere-labs/dsh-desktop](https://github.com/anywhere-labs/dsh-desktop) | 社区最火的 dsh 桌面端，把插件生态做成桌面应用 | 35.5k | 2026-11-06 |
| [dataelement/dsh-desktop](https://github.com/dataelement/dsh-desktop) | DSHDesktop：另一款主流 dsh 桌面版 | 17.6k | 2026-11-06 |
| [dsh-tauri/deepseek-harness-desktop](https://github.com/dsh-tauri/deepseek-harness-desktop) | Tauri 桌面版，安装包约 8 MB，免配环境、预置插件 | 3.5k | 2026-11-09 |
| [yyh-001/DSH-X](https://github.com/yyh-001/DSH-X) | 轻量启动器：多实例、版本、插件、整合包、MCP 与技能管理 | 774 | 2026-11-09 |
| [lencx/Minke](https://github.com/lencx/Minke) | DeepSeek Harness 桌面客户端 | 700 | 2026-10-18 |

### 手机与远程访问

| 项目 | 说明 | ⭐ | 最近更新 |
|---|---|--:|---|
| [DSH-APP/DSHA](https://github.com/DSH-APP/DSHA) | 免 Root、免 Termux，在安卓手机上运行 dsh | 3.2k | 2026-11-09 |
| [shaobeichen/dsh-pocket](https://github.com/shaobeichen/dsh-pocket) | 电脑上跑 dsh web，手机扫码同步访问（局域网 + 公网） | 2.9k | 2026-10-17 |
| [liguobao/ds-harness-remote](https://github.com/liguobao/ds-harness-remote) | P2P 优先、端到端加密的多端远程访问 | 2.4k | 2026-11-09 |
| [saya-ch/dsh-mobile](https://github.com/saya-ch/dsh-mobile) | 安卓 App + 安全远程访问插件 | 799 | 2026-11-09 |
| [Clarklevis1995/dsh-mobile](https://github.com/Clarklevis1995/dsh-mobile) | 原生 iOS 客户端 | 750 | 2026-11-08 |

### 插件市场与发现

| 项目 | 说明 | ⭐ | 最近更新 |
|---|---|--:|---|
| [dsh-market/dsh-market](https://github.com/dsh-market/dsh-market) | dsh 可视化插件市场：浏览、搜索、一键安装 | 11.6k | 2026-11-08 |
| [zhu1090093659/dsh-web](https://github.com/zhu1090093659/dsh-web) | dsh Web 插件聚合生态，通过创意工坊分发 | 10.3k | 2026-11-08 |
| [AdamPlatin123/dsh-plugin-radar](https://github.com/AdamPlatin123/dsh-plugin-radar) | 持续追踪 dsh 插件生态的雷达 | 1.5k | 2026-11-09 |
| [LivXue/dsh-plugin-shop](https://github.com/LivXue/dsh-plugin-shop) | 每日刷新的 dsh 插件商店 | 662 | 2026-11-08 |

### 界面与交互

| 项目 | 说明 | ⭐ | 最近更新 |
|---|---|--:|---|
| [ccch1mneyyy/dsh-TUI](https://github.com/ccch1mneyyy/dsh-TUI) | 高性能终端界面（TUI）插件 | 7.3k | 2026-11-09 |
| [omdsh-dev/DSH-better-sidebar](https://github.com/omdsh-dev/DSH-better-sidebar) | 可扩展侧边栏：文件编辑、终端、侧边对话、Git、子代理 | 5.0k | 2026-11-09 |
| [omdsh-dev/dsh-genui](https://github.com/omdsh-dev/dsh-genui) | 在回复里渲染可交互的 UI 组件 | 941 | 2026-11-09 |
| [Aisland-SJL/dsh-worktable](https://github.com/Aisland-SJL/dsh-worktable) | 面向项目的 Agent 工作台 | 849 | 2026-10-31 |
| [liangmianya/dsh-synapse](https://github.com/liangmianya/dsh-synapse) | 可视化、非线性的对话工作区 | 690 | 2026-11-04 |

### 上下文、记忆与省 Token

| 项目 | 说明 | ⭐ | 最近更新 |
|---|---|--:|---|
| [T-Auto/dsh-ops](https://github.com/T-Auto/dsh-ops) | 底层操作工具集，减少 Token 消耗和任务耗时 | 5.6k | 2026-11-08 |
| [bowenliang123/dsh-context](https://github.com/bowenliang123/dsh-context) | 上下文洞察与管理，带上下文仪表盘 | 4.7k | 2026-11-09 |
| [omdsh-dev/dsh-mnemon](https://github.com/omdsh-dev/dsh-mnemon) | 可组合、基于视图的上下文来源 | 940 | 2026-11-08 |
| [csyangwen/dsh-memory-evolve](https://github.com/csyangwen/dsh-memory-evolve) | 跨会话长期记忆 + 后台自我进化 | 729 | 2026-10-29 |
| [adoresever/graph-memory](https://github.com/adoresever/graph-memory) | 知识图谱记忆插件（同时支持 OpenClaw） | 673 | 2026-10-01 |

### 联网搜索与视觉（给纯文本模型加眼睛）

| 项目 | 说明 | ⭐ | 最近更新 |
|---|---|--:|---|
| [liustack/modlens](https://github.com/liustack/modlens) | dsh 视觉插件，让纯文本模型也能看图 | 4.9k | 2026-11-07 |
| [ysr666/dsh-vision-router](https://github.com/ysr666/dsh-vision-router) | 视觉路由：为纯文本模型接入看图能力 | 1.2k | 2026-11-09 |
| [DDDMUC/dsh-free-search](https://github.com/DDDMUC/dsh-free-search) | 基于 DuckDuckGo 的免费搜索提供方，无需 Key | 1.0k | 2026-11-08 |
| [liustack/modsearch](https://github.com/liustack/modsearch) | 免费联网搜索插件，免注册、无需 API Key | 963 | 2026-11-07 |
| [Anionex/dsh-vision-toolkit](https://github.com/Anionex/dsh-vision-toolkit) | 视觉工具箱：粘贴图片识别、多图问答、截图还原前端 | 934 | 2026-11-06 |
| [anysearch-team/anysearch-dsh](https://github.com/anysearch-team/anysearch-dsh) | AnySearch 搜索提供方与高级搜索工具 | 687 | 2026-10-10 |

### 多 Agent 与自动化

| 项目 | 说明 | ⭐ | 最近更新 |
|---|---|--:|---|
| [Fei2411/DeepSeek-Bot](https://github.com/Fei2411/DeepSeek-Bot) | 长期运行的机器人团队，支持 bot 间消息 | 6.5k | 2026-11-09 |
| [xiaobright/dsh-anchored-standard](https://github.com/xiaobright/dsh-anchored-standard) | 两阶段预设：最小化启动，再加载完整工具 | 3.7k | 2026-10-21 |
| [chuspeeism/dashi-taskboard](https://github.com/chuspeeism/dashi-taskboard) | 可嵌入的任务面板（支持 Codex 与 dsh） | 3.5k | 2026-11-06 |
| [NanmiCoder/dsh-agent-teams](https://github.com/NanmiCoder/dsh-agent-teams) | Agent Teams：多个 Agent 组队分工、并行协作 | 2.8k | 2026-11-06 |
| [omdsh-dev/dsh-browser](https://github.com/omdsh-dev/dsh-browser) | Chrome 侧边栏扩展，让 dsh 操作你的浏览器 | 1.0k | 2026-11-08 |

### 消息与办公

| 项目 | 说明 | ⭐ | 最近更新 |
|---|---|--:|---|
| [xmanrui/dsh-im](https://github.com/xmanrui/dsh-im) | 把飞书、微信、钉钉、企业微信、QQ、Telegram 等机器人接入 dsh | 3.4k | 2026-11-07 |
| [Devin-AXIS/deepseek-design](https://github.com/Devin-AXIS/deepseek-design) | 可编辑的设计系统与 PPT 工作室 | 1.8k | 2026-11-04 |
| [dream-num/dsh-univer-office](https://github.com/dream-num/dsh-univer-office) | 给 dsh 一个真正的办公环境（Univer 表格 / 文档） | 701 | 2026-11-03 |
| [1692775560/dsh-Mimir-Academic-research](https://github.com/1692775560/dsh-Mimir-Academic-research) | 科研工作台：LaTeX、arXiv、实验追踪、GPU 任务 | 562 | 2026-11-04 |

### 创作

| 项目 | 说明 | ⭐ | 最近更新 |
|---|---|--:|---|
| [sixtysevenlf/dsh-blender-plugin](https://github.com/sixtysevenlf/dsh-blender-plugin) | 直连 Blender，让 AI 驱动 3D 建模 | 1.9k | 2026-11-08 |
| [c1overzz/dsh-bili-scroll](https://github.com/c1overzz/dsh-bili-scroll) | 每天替你刷 B 站、读字幕、写日报 | 1.3k | 2026-11-08 |
| [shanliuling/dsh-image-gen](https://github.com/shanliuling/dsh-image-gen) | 对话内生成和编辑图像，内置 500+ 提示词，支持 ComfyUI | 1.2k | 2026-11-08 |
| [LiPu-jpg/Openwrite](https://github.com/LiPu-jpg/Openwrite) | 小说创作插件，含 90 个写作工具 | 935 | 2026-11-08 |
| [zenstory-ai/oh-story-dsh](https://github.com/zenstory-ai/oh-story-dsh) | 网文、短剧、游戏、视频解说四个创作工作台 | 715 | 2026-11-08 |

### 费用与用量

| 项目 | 说明 | ⭐ | 最近更新 |
|---|---|--:|---|
| [MeteorNOX/DeepSeek-Balance-Whale-Widget](https://github.com/MeteorNOX/DeepSeek-Balance-Whale-Widget) | 界面右下角的小鲸鱼，帮你盯 DeepSeek 账户余额 | 7.1k | 2026-10-11 |
| [xiufengsun/TokenTracker](https://github.com/xiufengsun/TokenTracker) | 本地统计 31 种 AI 编程工具的 Token 和费用 | 2.2k | 2026-11-09 |
| [Han-1413141/dsh-cost-meter](https://github.com/Han-1413141/dsh-cost-meter) | 按会话、按模型统计 dsh 的花费和 Token | 655 | 2026-11-09 |

### 皮肤与趣味

| 项目 | 说明 | ⭐ | 最近更新 |
|---|---|--:|---|
| [elysia395/dsh-wallpaper-engine](https://github.com/elysia395/dsh-wallpaper-engine) | 把 Wallpaper Engine 壁纸搬进 dsh 网页界面 | 6.1k | 2026-11-09 |
| [PC2005-cloud/dsh-pet](https://github.com/PC2005-cloud/dsh-pet) | 一行命令装好的桌面宠物 | 5.9k | 2026-11-09 |
| [Small-tailqwq/dsh-deep-whale](https://github.com/Small-tailqwq/dsh-deep-whale) | 鲸鱼娘系列皮肤 | 3.1k | 2026-11-08 |
| [flizzywine/dsh-tavern](https://github.com/flizzywine/dsh-tavern) | 类酒馆文字游戏 Agent，兼容 SillyTavern 人物卡 | 1.5k | 2026-11-09 |
<!-- END:projects -->

## 写自己的插件

插件是带 `dsh` 字段的 npm 包，最小的 `package.json`：

```json
{
  "name": "dsh-hello-plugin",
  "version": "0.1.0",
  "type": "module",
  "main": "index.js",
  "dsh": { "bundle": { "patch": "./cordis.patch.yml" } },
  "engines": { "dsh": ">=0.2.0 <0.3.0" }
}
```

入门可以看 [hello-dsh](https://github.com/pingfanfan/hello-dsh)（零基础插件开发教程，含 22 个中文技能实例）和官方文档 `docs/user/develop/`。更多教程见 [中文教程与资料](resources.md)。
