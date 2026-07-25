# 安全说明

## 报告安全问题

请通过 GitHub Security Advisory 私下报告安全漏洞，不要在公开 Issue 中提交 OAuth Token、API Key、Bearer Token、项目机密或可复现的敏感凭据。

## 凭据边界

- 本插件不保存 Codex 或 Kimi 的 OAuth Token。
- 登录状态和凭据由官方 CLI 管理。
- 不要将 `.codex/` 中的敏感配置、环境变量文件或 Godot MCP Native Bearer Token 提交到仓库。
- Kimi ACP 文件操作被限制在当前 Godot 项目目录。
- Codex 默认使用 `workspace-write` 沙箱和按请求审批。
