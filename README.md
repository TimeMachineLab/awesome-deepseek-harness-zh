# DeepSeek Harness 中文使用指南与资源大全（dsh 教程 · 插件 · Skills）

**中文** | [English](README.en.md)

**DeepSeek Harness（简称 dsh）是 DeepSeek 开源的 AI Agent 运行框架，采用「万物皆插件」的架构（MIT 协议）。** 本仓库用中文讲清楚 dsh 怎么安装、怎么配模型和 API Key、怎么装插件和 Skills、哪些默认设置要先改、遇到报错怎么办，并收录了 68 个精选插件、Skills 和中文教程。

> 📌 最后核对：**2026-10-23**，对应 dsh `0.2.1-rc` 版本。dsh 还是**开发者预览版**，官方明确说会有不兼容的更新，遇到和本文不一致的地方请以[官方文档](https://deepseek-harness.github.io/deepseek-harness/)为准，也欢迎提 [Issue](../../issues) 告诉我们。
>
> 由 [Orbis（orbiorbi.com）](https://orbiorbi.com/?utm_source=github&utm_medium=readme&utm_campaign=awesome-deepseek-harness-zh&utm_content=intro) 团队维护；本仓库与 DeepSeek 官方无关联。

## 目录

- [dsh 是什么](#dsh-是什么)
- [5 分钟上手](#5-分钟上手)
- [用之前先改的 3 个设置](#用之前先改的-3-个设置)
- [入门教程](#入门教程)
- [精选插件](#精选插件)
- [精选 Skills](#精选-skills)
- [常见报错速查](#常见报错速查)
- [FAQ](#faq)
- [贡献与收录标准](#贡献与收录标准)

## dsh 是什么

| 项目 | 说明 |
|---|---|
| [wwewtech/numes-deepseek-harness](https://github.com/wwewtech/numes-deepseek-harness) | 免费使用 Numes 市场的 `$0` 模型：零依赖本地代理，`:free` + `max_price` 双重零成本防护、5 秒到 5 分钟指数重试、免费模型自动发现 |
| 开发方 | DeepSeek AI，官方仓库 [deepseek-ai/deepseek-harness](https://github.com/deepseek-ai/deepseek-harness) |
| 定位 | 开源 AI Agent 运行框架，**一切功能都是插件**：模型、工具、界面、记忆都能替换 |
| 协议 | MIT，软件本身免费 |
| 当前版本 | `0.2.1-rc`（开发者预览版，2026 年 8 月发布） |
| 使用方式 | Web 界面（默认 `http://127.0.0.1:3080`）、桌面版（Windows / macOS）、命令行无界面模式、Python SDK |
| 默认模型 | DeepSeek 官方 API（`deepseek-flash`、`deepseek-v4-pro`），也能接 Kimi、GLM 和任何 OpenAI / Anthropic 兼容服务 |
| 反馈渠道 | 官方仓库关闭了 Issues，只能在 [Discussions](https://github.com/deepseek-ai/deepseek-harness/discussions) 反馈 |

## 5 分钟上手

**第 1 步：安装**，三选一：

| 方式 | 适合谁 | 命令 / 下载 |
|---|---|---|
| **桌面版**（推荐新手） | Windows、macOS 用户，不想装 Node.js | [Windows x64](https://download.deepseek.com/desktop/dsh-latest-windows-x64.exe) · [macOS Apple 芯片](https://download.deepseek.com/desktop/dsh-latest-macos-arm64.dmg) · [macOS Intel](https://download.deepseek.com/desktop/dsh-latest-macos-x64.dmg) |
| **npx 一行启动**（官方快速开始） | 已装 Node.js 的开发者 | `npx @deepseek-ai/dsh web` |
| **源码运行** | 想改代码、装 Git 插件 | 见[安装教程](docs/install.md#方式三从源码运行) |

> `npx` 第一次运行要解析大量依赖，**看起来像卡住是常见现象**，解决办法见[安装卡住怎么办](docs/install.md#安装卡住怎么办)。

**第 2 步：填 API Key**。打开 **Settings → Models**，填入 [DeepSeek 开放平台](https://platform.deepseek.com/) 的 API Key 并保存。也可以登录 DeepSeek 账号，或者[接其他模型](docs/models.md)。

**第 3 步：选工作区**。点 **Choose workspace** 选择项目文件夹。**不选工作区，输入框是灰的**，这是很多人以为「装坏了」的原因。

**第 4 步：发第一条消息**，比如「读一下这个项目的 README，总结一下」。

## 用之前先改的 3 个设置

这几点官方文档里都有写，但中文资料很少提到：

1. **会话日志默认上传**：用 DeepSeek 官方 API 时，dsh 默认把会话日志上传给 DeepSeek。另外还有一套遥测上传对所有用户生效。不想上传就分别关掉，方法见 [隐私与安全设置](docs/privacy-security.md)。
2. **内置联网搜索会带着你的 Key 发请求**：它会把 DeepSeek 卡片上配置的 Key 发到对应地址，而且**每搜一次都消耗一次模型调用**。用第三方服务时要特别注意，见[联网搜索](docs/models.md#内置联网搜索的坑)。
3. **在隔离环境里用**：dsh 会执行模型生成的命令、加载第三方插件，官方说明它**没有经过安全审计**，建议在虚拟机或容器里使用。

## 入门教程

| 教程 | 解决什么问题 |
|---|---|
| [DeepSeek Harness 安装教程](docs/install.md) | 桌面版、npx、全局安装、源码运行；**安装卡住**、Windows 文件夹选择框报错 |
| [配置模型与 API Key](docs/models.md) | DeepSeek 官方、Kimi、GLM、自定义 OpenAI 兼容服务；Key 存在哪 |
| [插件安装教程与精选插件](docs/plugins.md) | `dsh plugin add` 命令、插件市场、51 个精选插件 |
| [Skills 安装与使用](docs/skills.md) | Skills 放在哪个目录、`SKILL.md` 怎么写、精选 Skills |
| [配置 MCP 服务器](docs/mcp.md) | 接入 GitHub、本地服务等 MCP 工具 |
| [隐私与安全设置](docs/privacy-security.md) | 关掉日志上传和遥测、代理密码泄露风险 |
| [常见报错排查](docs/troubleshooting.md) | 403、模型连不上、`UNKNOWN_MODEL`、输出被截断等 |
| [中文教程与资料](docs/resources.md) | 橙皮书、深度手册、开发教程、其他精选列表 |

## 精选插件

按星数挑了最常用的一部分，完整的 51 个按用途分类的插件见 [精选插件](docs/plugins.md)。

| 插件 | 做什么 |
|---|---|
| [anywhere-labs/dsh-desktop](https://github.com/anywhere-labs/dsh-desktop) | 社区最火的 dsh 桌面端 |
| [dsh-market/dsh-market](https://github.com/dsh-market/dsh-market) | 可视化插件市场：浏览、搜索、一键安装 |
| [ccch1mneyyy/dsh-TUI](https://github.com/ccch1mneyyy/dsh-TUI) | 终端界面（TUI），npm 一键安装 |
| [bowenliang123/dsh-context](https://github.com/bowenliang123/dsh-context) | 上下文洞察与管理，带上下文仪表盘 |
| [liustack/modlens](https://github.com/liustack/modlens) | 让纯文本模型也能看图 |
| [liustack/modsearch](https://github.com/liustack/modsearch) | 免费联网搜索，无需 API Key |
| [NanmiCoder/dsh-agent-teams](https://github.com/NanmiCoder/dsh-agent-teams) | 多个 Agent 组队协作 |
| [xmanrui/dsh-im](https://github.com/xmanrui/dsh-im) | 接入飞书、微信、钉钉、QQ 等机器人 |
| [Han-1413141/dsh-cost-meter](https://github.com/Han-1413141/dsh-cost-meter) | 按会话、按模型统计花费 |

安装方法：`dsh plugin --profile web add <npm 包名>`，详见[插件安装教程](docs/plugins.md#怎么安装插件)。

## 精选 Skills

Skills 是一个带说明的 `SKILL.md` 文件夹，放进 `~/.dsh/skills/`（全局）或项目里的 `.dsh/skills/` 就能用。完整列表见 [Skills 安装与使用](docs/skills.md)。

| Skill | 做什么 |
|---|---|
| [tt-a1i/archify](https://github.com/tt-a1i/archify) | 把方案或代码库画成可交互的架构图 |
| [anbeime/skill](https://github.com/anbeime/skill) | 中文 Skills 商店，打包好直接装 |
| [vinvcn/mattpocock-skills-zh-CN](https://github.com/vinvcn/mattpocock-skills-zh-CN) | Matt Pocock skills 简体中文版 |
| [Jesseovo/last30days-skill-cn](https://github.com/Jesseovo/last30days-skill-cn) | 中文互联网近 30 天热点研究 |

## 常见报错速查

| 现象 | 原因和处理 |
|---|---|
| `npx @deepseek-ai/dsh web` 很久没反应 | npx 在解析大量依赖。耐心等，或改用桌面版 / 全局安装，见[安装卡住](docs/install.md#安装卡住怎么办) |
| 打开网页显示 403 | 用 `localhost` 打开会被拒，**改用 `http://127.0.0.1:3080`** |
| 输入框是灰的，发不了消息 | 还没选工作区，点 **Choose workspace** |
| `DeepSeek API request ... failed` | 网络或代理问题，或 Key 无效，见[报错排查](docs/troubleshooting.md#模型连不上) |
| `UNKNOWN_MODEL` / `MISSING_CREDENTIAL` | 模型 ID 没加到服务商的模型列表 / Key 没保存，见[配置模型](docs/models.md#常见配置错误) |
| `--host 0.0.0.0` 被拒绝 | 官方有意禁止，改用具体的局域网 IP |
| `Output token limit reached` | 单次输出达到上限，不是上下文满了，调大对应线路的 `maxTokens` |

更多见 [常见报错排查](docs/troubleshooting.md)。

## FAQ

### DeepSeek Harness 是免费的吗？

dsh **软件本身免费开源**（MIT）。但它要调用大模型才能干活，模型调用按你所用服务商的价格计费。官方文档没有提到免费额度。

### 用 dsh 需要 DeepSeek 账号吗？

不需要。填一个 DeepSeek API Key 就能用；也可以选择用 DeepSeek 账号在浏览器里授权登录。

### 国内能用 dsh 吗？

能。默认连接的 DeepSeek 官方 API 国内直连。安装时 npm 下载慢，可以用国内镜像或直接下载桌面版，见[安装教程](docs/install.md)。

### dsh 能用 Kimi、GLM、Claude、GPT 等其他模型吗？

能。dsh 内置了 Kimi（moonshotai）、GLM（zai）、OpenAI、Anthropic 等服务商，也可以在 **Settings → Models → Add model provider → Custom model API** 里添加任何 OpenAI 或 Anthropic 兼容的服务。想用**一个 Key 切换多家模型**，可以接聚合平台，比如 [Orbis](https://orbiorbi.com/docs/deepseek-harness/?utm_source=github&utm_medium=readme&utm_campaign=awesome-deepseek-harness-zh&utm_content=faq-models)（本仓库维护方），配置见[接入第三方服务](docs/models.md#接入第三方--聚合平台以-orbis-为例)。不知道选哪个模型，可以看 [AI Agent 能力排行榜](https://orbiorbi.com/leaderboards/agent/?utm_source=github&utm_medium=readme&utm_campaign=awesome-deepseek-harness-zh&utm_content=faq-models)。

### dsh 会上传我的数据吗？

默认会：用 DeepSeek 官方 API 时上传会话日志，另有一套遥测对所有用户生效。两者都能关，见 [隐私与安全设置](docs/privacy-security.md)。

### dsh 和 Claude Code、Codex 有什么区别？

三者都是 AI 编程 / Agent 工具。dsh 开源（MIT）、以插件为核心、默认用 Web 界面，模型默认是 DeepSeek；Claude Code 和 Codex 分别来自 Anthropic 和 OpenAI，以终端为主。想在国内用 Claude Code 和 Codex，可以看我们的另一份指南 [Claude Code / Codex 国内使用教程](https://github.com/TimeMachineLab/claude-code-china-guide)。

### Linux 有 dsh 桌面版吗？

官方发布的桌面版目前只有 Windows x64 和 macOS（Apple 芯片 / Intel）。Linux 用 `npx` 或源码运行 Web 界面。

## 贡献与收录标准

欢迎推荐插件、Skills 和中文教程，开 [Issue](../../issues/new/choose) 或直接提 PR（改 [`data/projects.json`](data/projects.json)，再运行 `python scripts/render.py`）。

**收录标准**：开源、近两个月内有更新（教程资料不限）、与 dsh 明确相关。**不收录**：破甲 / 越狱提示词、逆向接口、来源不明的「免 Key 免费模型」、借用他人订阅账号的工具。详见 [CONTRIBUTING.md](CONTRIBUTING.md)。

星数表格由 GitHub Actions 每周一自动刷新。

## License

[CC0 1.0](LICENSE)：列表和教程内容可自由使用。各项目的版权归其作者所有。

> 披露：本仓库由 Orbis 团队维护，文中指向 Orbis 的链接带有来源统计参数（UTM），不含邀请返利。
