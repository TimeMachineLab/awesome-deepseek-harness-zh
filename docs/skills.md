# DeepSeek Harness 如何安装 Skills：目录位置、SKILL.md 写法与精选 Skills

> 返回 [DeepSeek Harness 中文使用指南](../README.md) · 最后核对：2026-10-23（dsh `0.2.1-rc`）· 依据官方文档 `docs/subsystems/skills.md`

Skill 是一份**告诉模型「遇到某类任务该怎么做」的说明书**，通常是一个文件夹，里面有 `SKILL.md`，还可以带脚本和模板。dsh 的 Skills 格式和 Claude Code 的 `SKILL.md` 思路一致，很多 Skills 仓库同时支持 Claude Code、Codex 和 dsh。

## Skills 放在哪

**安装一个 Skill，就是把它的文件夹放进下面任意一个目录。** 同名 Skill 按优先级生效，数字越小越优先：

| 目录 | 作用范围 | 优先级 |
|---|---|:---:|
| `<项目>/.dsh/skills/` | 只对这个项目生效 | 100 |
| `<项目>/.agents/skills/` | 只对这个项目生效（和其他 Agent 工具共用） | 200 |
| 配置项 `customSkillDirs` 里的目录 | 自定义 | 300 |
| `~/.dsh/skills/` | 全局，所有项目 | 400 |
| `~/.agents/skills/` | 全局（和其他 Agent 工具共用） | 500 |
| dsh 内置 | —— | 600 |

「项目根目录」是离当前工作区最近、带 `.git` 的上级目录。

**手动安装（通用做法）**：找到 Skills 仓库里包含 `SKILL.md` 的那个文件夹，复制到全局目录：

```bash
# macOS / Linux
git clone https://github.com/作者/仓库名 /tmp/some-skill
mkdir -p ~/.dsh/skills
cp -r /tmp/some-skill/<含 SKILL.md 的文件夹> ~/.dsh/skills/
```

```powershell
# Windows PowerShell
git clone https://github.com/作者/仓库名 $env:TEMP\some-skill
New-Item -ItemType Directory -Force "$env:USERPROFILE\.dsh\skills" | Out-Null
Copy-Item -Recurse "$env:TEMP\some-skill\<含 SKILL.md 的文件夹>" "$env:USERPROFILE\.dsh\skills\"
```

**用安装命令的 Skills**：很多 Skills 仓库提供 `npx skills add <作者/仓库> -g` 这类一键安装命令，主要面向 Claude Code、Codex、Cursor。装完检查一下 Skill 是否落在上表的某个目录里（比如 `~/.agents/skills/`）；不在的话，按上面的方法手动复制一份到 `~/.dsh/skills/`。

想让多个 Agent 工具共用一份 Skills，放进 `~/.agents/skills/`，或者用 [Skills-Manager](https://github.com/jiweiyeah/Skills-Manager) 这类工具同步。

## SKILL.md 怎么写

两种格式都行：

- 文件夹：`<名字>/SKILL.md`（可以附带其他文件）
- 单文件：`<名字>.md`

规则：

- 名字用小写加连字符（kebab-case），比如 `weekly-report`
- **不支持嵌套**：`skills/a/b/SKILL.md` 不会被识别
- 开头的 frontmatter 必须有 `description`，模型靠它判断什么时候用这个 Skill

```markdown
---
description: 根据本周的 git 提交记录写一份中文周报。用户提到「周报」「本周总结」时使用。
---

# 写周报

1. 运行 `git log --since="1 week ago" --oneline` 获取本周提交
2. 按功能、修复、其他分组
3. 输出 Markdown 格式的周报，每组不超过 5 条
```

可选字段：

- `disable-model-invocation: true`：模型不会自动调用，只能你手动用
- `user-invocable: false`：不出现在你的手动调用列表里

**工作原理**：dsh 只把每个 Skill 的名字和 `description` 放进目录给模型看；模型判断需要时，才通过 `skill` 工具读取完整内容。所以 **`description` 要写清楚「做什么」和「什么时候用」**，这比正文更重要。

## 精选 Skills

<!-- BEGIN:projects -->
> 星数和更新时间截至 2026-11-02，每周自动刷新。

### Skills 合集与管理

| 项目 | 说明 | ⭐ | 最近更新 |
|---|---|--:|---|
| [anbeime/skill](https://github.com/anbeime/skill) | 中文 Skills 商店：精选技能包，打包好可直接安装 | 9.0k | 2026-11-01 |
| [vinvcn/mattpocock-skills-zh-CN](https://github.com/vinvcn/mattpocock-skills-zh-CN) | Matt Pocock skills 简体中文版，人工审核、同步上游，支持 dsh | 5.5k | 2026-10-28 |
| [iflytek/skillhub](https://github.com/iflytek/skillhub) | 可私有部署的企业级 Skills 仓库 | 5.4k | 2026-11-02 |
| [jiweiyeah/Skills-Manager](https://github.com/jiweiyeah/Skills-Manager) | 桌面端 Skills 管理器：写一次，同步到多个 Agent | 1.1k | 2026-09-10 |

### 实用 Skills

| 项目 | 说明 | ⭐ | 最近更新 |
|---|---|--:|---|
| [tt-a1i/archify](https://github.com/tt-a1i/archify) | 把想法、方案或代码库变成可交互的架构图 | 92.5k | 2026-11-02 |
| [Tencent/BrowserSkill](https://github.com/Tencent/BrowserSkill) | 让 Agent 使用你已登录的真实浏览器 | 9.9k | 2026-11-02 |
| [QingYunA/answer-me-with-html](https://github.com/QingYunA/answer-me-with-html) | 用一页 HTML 回答复杂问题 | 5.1k | 2026-11-02 |
| [Jesseovo/last30days-skill-cn](https://github.com/Jesseovo/last30days-skill-cn) | 中文互联网研究：检索 8 大平台近 30 天讨论，生成带来源的报告 | 2.0k | 2026-11-02 |
| [XiaoMaColtAI/math-modeling-skill](https://github.com/XiaoMaColtAI/math-modeling-skill) | 数学建模竞赛工作流：建模、编程、论文生成 | 1.9k | 2026-11-01 |
| [Anionex/agent-vision-toolkit](https://github.com/Anionex/agent-vision-toolkit) | 给纯文本模型用的看图工具箱和技能 | 1.3k | 2026-10-13 |
<!-- END:projects -->

更多 Skills 可以看 [anbeime/skill](https://github.com/anbeime/skill) 这样的 Skills 商店，或在 GitHub 上搜索 `topic:agent-skills`。
