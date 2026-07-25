# Godot AI Manager

Godot AI Manager 是一个运行在 Godot 编辑器中的 AI Agent 管理插件。它统一接入 **OpenAI Codex** 与 **Kimi Code** 的官方本地后端，并将 Godot 编辑器专用能力交给独立项目 **Godot MCP Native**。

本项目由 `sn-Cloud` 独立维护。项目的对话管理、会话组织、状态展示、审批、Diff 和日志设计参考了 [Fennara](https://github.com/fennaraOfficial/fennara-godot-ai) 的代码与架构；Godot 编辑器操作由 [Godot MCP Native](https://github.com/yurineko73/Godot-MCP-Native) 提供。

## 项目定位

```text
Godot AI Manager
├── Codex 官方后端
│   ├── codex app-server
│   └── ChatGPT / Codex 账户登录
├── Kimi Code 官方后端
│   ├── kimi acp
│   └── kimi login 设备码登录
└── Godot MCP Native
    └── 独立安装的 Godot 原生 MCP 配套子项目
```

核心原则：

- Codex 只使用 OpenAI 官方 `codex app-server`。
- Kimi Code 只使用 Moonshot AI 官方 `kimi acp` 和 `kimi login`。
- 不使用第三方协议转换器。
- 本仓库不实现第二套 Godot MCP。
- Godot MCP Native 独立安装、独立升级，由其原作者维护。

## Godot MCP Native

Godot MCP Native 是本项目的核心配套子项目，但不是本仓库的一部分。本仓库不会复制、打包、自动修改或声明拥有 Godot MCP Native。

官方仓库：<https://github.com/yurineko73/Godot-MCP-Native>

默认 MCP 地址：

```text
http://127.0.0.1:9080/mcp
```

Godot MCP Native 提供场景、节点、脚本、资源、调试器、Profiler、运行时对象、输入、动画、材质、音频和截图等 Godot 编辑器能力。

未安装或未启动 Godot MCP Native 时，Codex 与 Kimi Code 仍可使用文件、Shell 和 Git 工具，但无法可靠读取或操作 Godot 编辑器内部状态。插件会显示缺失状态和安装引导。

## 功能

### Codex

- 自动查找 `codex.exe`、`codex.cmd` 或 Unix `codex`。
- 使用 `codex app-server` 的 stdio JSON-RPC / JSONL 接口。
- 支持账户状态读取、ChatGPT 登录和退出。
- 支持创建、恢复和切换会话。
- 支持启动、中断任务和流式消息。
- 展示工具活动、计划、Diff 和日志。
- 处理命令、文件、额外权限、用户输入和 MCP elicitation 审批。
- 自动维护项目 `.codex/config.toml` 中唯一的 `godot-mcp` 配置。

### Kimi Code

- 自动查找 `kimi.exe`、`kimi.cmd` 或 Unix `kimi`。
- 使用官方 `kimi acp` stdio ACP JSON-RPC。
- 支持 ACP 初始化、能力协商和会员身份验证。
- 使用官方 `kimi login` 设备码登录流程。
- 支持创建、加载和恢复会话。
- 通过 ACP `mcpServers` 接入 Godot MCP Native。
- 支持 prompt、流式消息、思考摘要、计划、工具活动和取消任务。
- ACP 文件读写严格限制在当前 Godot 项目目录。

Kimi ACP 当前没有官方 `logout` 方法。退出账户时，请在 Kimi Code CLI 中执行 `/logout`。

## 安装

### 1. 安装 Godot MCP Native

在 Godot Asset Library 搜索 **Godot MCP Native**，或从其官方仓库安装：

```text
addons/godot_mcp/
```

然后在 **项目 > 项目设置 > 插件** 中启用。

### 2. 安装 Godot AI Manager

将本仓库中的目录复制到 Godot 项目：

```text
addons/godot_ai_manager/
```

然后启用 **Godot AI Manager** 插件。

推荐目录结构：

```text
addons/
├── godot_ai_manager/
└── godot_mcp/
```

### 3. 安装官方 CLI

安装 OpenAI Codex CLI，并确认：

```bash
codex --version
```

安装 Kimi Code CLI：

```bash
npm install -g @moonshot-ai/kimi-code@latest
kimi --version
```

## 使用

1. 打开 Godot 编辑器中的 **GodotAiManagerDock**。
2. 选择 **Codex** 或 **Kimi Code**。
3. 点击连接。
4. 使用对应官方流程登录账户。
5. 检查 Godot MCP Native 连接状态。
6. 输入开发任务并审查审批、Diff 和日志。

## 安全边界

- Codex 默认使用 `workspace-write` 沙箱和 `on-request` 审批策略。
- Kimi ACP 文件反向 RPC 只能访问当前 Godot 项目目录。
- 本插件不读取或保存 ChatGPT、Codex、Kimi 的 OAuth Token。
- 登录凭据由各自官方 CLI 保存和刷新。
- 插件发现旧 Fennara MCP 配置时只显示警告，不修改用户私人配置。
- Godot MCP Native 使用 Bearer Token 时，不要把 Token 提交到 Git。

## 仓库边界

本仓库不包含：

- Fennara MCP Server、daemon、CLI 或 WebSocket Bridge；
- Fennara 的 Godot 工具和模型运行时；
- Godot MCP Native 源码；
- Codex CLI 或 Kimi Code CLI；
- OAuth Token、API Key 或用户登录凭据。

## 验证

仓库提供两个仅手动触发的 GitHub Actions 工作流：

- 仓库结构与遗留运行时检查；
- Windows / Linux Godot 双后端完整测试。

它们不会因普通提交或 Pull Request 自动运行，也不会生成安装 ZIP。

## 文档

- [架构](docs/architecture.md)
- [手动安装](docs/manual-install.md)
- [仓库结构](docs/repo-map.md)
- [发布检查](docs/release.md)
- [插件说明](addons/godot_ai_manager/README.md)

## 许可证与归属

Godot AI Manager 使用 MIT License。

本项目参考了 Fennara 的代码和架构。Fennara 与 Godot MCP Native 均为独立第三方项目，本项目与其作者、OpenAI、Moonshot AI 或 Godot Engine 不存在官方隶属关系。详见 [NOTICE.md](NOTICE.md) 和 [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md)。
