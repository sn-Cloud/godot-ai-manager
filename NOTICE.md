# 项目归属与第三方说明

## Godot AI Manager

本项目由 `sn-Cloud` 独立开发和维护，是一个面向 Godot 编辑器的第三方 AI Agent 管理插件。

本项目不是 OpenAI、Moonshot AI、Godot Engine、Fennara 或 Godot MCP Native 的官方产品，也不代表这些组织或项目。

## Fennara

本项目最初从 Fennara 的分支实验发展而来，并参考了 Fennara 在 AI 对话管理、会话组织、状态展示、审批、Diff、日志和编辑器交互方面的代码与架构。

原项目：<https://github.com/fennaraOfficial/fennara-godot-ai>

本仓库不包含 Fennara MCP Server、daemon、CLI、WebSocket Bridge、Godot 工具定义或模型提供方运行时。Fennara 的原始 MIT 许可证声明保存在 [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md)。

## Godot MCP Native

Godot MCP Native 是本项目的独立核心配套子项目，由其原作者维护：

<https://github.com/yurineko73/Godot-MCP-Native>

本仓库不会复制、打包、自动更新或声明拥有 Godot MCP Native。用户必须单独安装并启用它。

## Codex 与 Kimi Code

Codex CLI / app-server 由 OpenAI 提供；Kimi Code CLI / ACP 由 Moonshot AI 提供。本仓库仅实现其官方本地客户端协议的第三方 Godot 前端，不包含这些 CLI。
