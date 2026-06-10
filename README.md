<p align="center">
  <img src="docs/images/app-icon.png" alt="Agent Island" width="180">
</p>

<h1 align="center">Agent Island</h1>

<p align="center">
  <strong>本地优先、原生 macOS 的 AI coding agent 伴侣应用。</strong>
</p>

<p align="center">
  <a href="https://github.com/dimsky/agent-island-dist/releases/latest"><img src="https://img.shields.io/github/v/release/dimsky/agent-island-dist?style=flat-square&label=release&color=blue" alt="最新版本"></a>
</p>

<p align="center">
  <a href="#下载安装">下载安装</a> ·
  <a href="https://island.dimsky.cn">官网</a>
</p>

---

## Agent Island 是什么？

Agent Island 驻留在 Mac 的**灵动岛区域**（或顶部栏），为你的 AI coding agents 提供实时控制面板——会话状态、权限审批、一键跳回正确的终端。全程不打断你的工作流。

## 为什么选 Agent Island？

- **本地优先** — 无服务器、无遥测、无需注册。一切在你的 Mac 上运行
- **原生 macOS** — SwiftUI + AppKit，不是 Electron 套壳
- **多 Agent** — 一个界面管理 Claude Code、Codex、Cursor、Gemini CLI、OpenCode 等
- **多终端** — 一键跳回到准确的终端/IDE 会话

## 支持的 Agents 和终端

**10 个 Agents**：Claude Code、Codex、Cursor、Gemini CLI、Kimi CLI、OpenCode、Qoder、Qwen Code、Factory、CodeBuddy

**15+ 终端和 IDE**：Terminal.app、Ghostty、iTerm2、WezTerm、Zellij、tmux、cmux、Kaku、VS Code、Cursor、Windsurf、Trae、JetBrains 全家桶

<details>
<summary>完整兼容列表</summary>

### Code Agents

| Agent | 状态 | 说明 |
|---|---|---|
| **Claude Code** | 已支持 | Hook 集成、JSONL 会话发现、status line bridge、用量追踪 |
| **Codex**（CLI） | 已支持 | Hook 集成（默认 SessionStart、UserPromptSubmit、Stop），用量追踪 |
| **Codex 桌面 App** | 已支持 | Hook 集成 + app-server JSON-RPC 直连，点击通过 `codex://threads/<id>` 精确跳转 |
| **OpenCode** | 已支持 | JS 插件集成、权限/问答交互、进程检测 |
| **Qoder** | 已支持 | Claude Code 分支，配置位于 `~/.qoder/settings.json` |
| **Qwen Code** | 已支持 | Claude Code 分支，配置位于 `~/.qwen/settings.json` |
| **Factory** | 已支持 | Claude Code 分支，配置位于 `~/.factory/settings.json` |
| **CodeBuddy** | 已支持 | Claude Code 分支，配置位于 `~/.codebuddy/settings.json` |
| **Cursor** | 已支持 | Hook 集成，通过 `~/.cursor/hooks.json` 配置，工作区跳转 |
| **Gemini CLI** | 已支持 | Hook 集成，通过 `~/.gemini/settings.json` 配置 |
| **Kimi CLI** | 已支持 | Hook 集成，通过 `~/.kimi/config.toml` 配置，复用 Claude payload 协议 |

### 终端和 IDE

| 终端 / IDE | 支持级别 | 说明 |
|---|---|---|
| **Terminal.app** | 完整 | Jump-back，TTY 定位 |
| **Ghostty** | 完整 | Jump-back，ID 匹配 |
| **iTerm2** | 完整 | Jump-back，session ID / TTY 匹配 |
| **WezTerm** | 完整 | Jump-back，CLI pane 定位 |
| **Zellij** | 完整 | Jump-back，CLI pane/tab 定位 |
| **tmux** | 完整 | Jump-back，session/window/pane 定位 |
| **cmux** | 完整 | Jump-back，Unix socket API |
| **Kaku** | 完整 | Jump-back，CLI pane 定位 |
| **Warp** | 完整 | 通过 SQLite pane 查找 + AX 菜单点击精准跳转 |
| **VS Code** | 工作区 | 通过 `code` CLI 激活工作区 |
| **Cursor** | 工作区 | 通过 `cursor` CLI 激活工作区 |
| **Windsurf** | 工作区 | 通过 `windsurf` CLI 激活工作区 |
| **Trae** | 工作区 | 通过 `trae` CLI 激活工作区 |
| **JetBrains 全家桶** | 工作区 | IDEA、WebStorm、PyCharm、GoLand、CLion、RubyMine、PhpStorm、Rider、RustRover |

</details>

## 下载安装

### 方式一：直接下载

从本仓库 [Releases](https://github.com/dimsky/agent-island-dist/releases) 下载最新 DMG——已签名公证，开箱即用。

### 方式二：Homebrew

```bash
brew install --cask dimsky/tap/agentisland
```

后续升级：

```bash
brew upgrade --cask agentisland
```

> **系统要求**：macOS 14+

## 工作原理

```
Agent（Claude Code / Codex / Cursor / ...）
  ↓ hook 事件
AgentIslandHooks CLI（stdin → Unix socket）
  ↓ JSON envelope
BridgeServer（app 内）
  ↓ 状态更新
Notch 覆盖层 UI ← 你在这里看到它
  ↓ 点击
跳回 → 正确的终端 / IDE
```

Hooks **fail open**——如果 Agent Island 没在运行，你的 agents 不受任何影响。

## 功能一览

| 功能 | 说明 |
|---|---|
| 灵动岛 / 顶部栏覆盖层 | 灵动岛 Mac 在灵动岛区域，其他 Mac 顶部居中栏 |
| 实时会话面板 | 可展开的详情行，显示 agent 状态和进度 |
| 权限审批 | 自适应高度面板，直接在覆盖层处理权限请求 |
| 一键跳回 | 点击即跳回对应的终端/IDE 精确位置 |
| 用量仪表盘 | 追踪 Claude Code / Codex 的 5 小时和 7 天用量 |
| Hook 管理 | 设置窗口一键安装/卸载所有 agent hooks |
| 通知音效 | 可配置系统音效，支持静音切换 |
| 自动更新 | 基于 Sparkle 的静默自动更新 |
| 国际化 | English、简体中文 |

## 反馈与支持

遇到问题或有功能建议，欢迎直接 [提交 Issue](https://github.com/dimsky/agent-island-dist/issues)。

---

## 关于本仓库

这是 Agent Island 的**发布分发仓库**，包含：

- **`appcast.xml`** — Sparkle 自动更新订阅源
- **Release 资产** — 每个版本的已签名 `AgentIsland.dmg` / `AgentIsland.zip`

自动更新订阅源：`https://raw.githubusercontent.com/dimsky/agent-island-dist/main/appcast.xml`

