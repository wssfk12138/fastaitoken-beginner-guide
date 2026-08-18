# PROJECT_NOTES

## 最近状态摘要

- 2026-08-18：建立纯 Markdown 中文新手指南，覆盖中转站、倍率、计费、快速开始、Codex、通用客户端、排错、安全和 FAQ。
- 仓库计划公开发布到 `wssfk12138/fastaitoken-beginner-guide`。

## 项目定位

面向第一次使用 AI 中转站和 API 的中文用户，用生活化比喻解释基础概念，并提供可直接核对的配置示例。

本仓库是第三方指南。涉及价格、分组、倍率、模型名称和可用性的内容必须标注“以平台控制台实时信息为准”，不得写成永久承诺。

## 技术栈

- Markdown
- GitHub 原生 README 与相对链接
- 无构建工具、无运行时依赖

## 常用命令

```powershell
git diff --check
git status --short
git add README.md PROJECT_NOTES.md docs
git commit -m "docs: publish FastAiToken beginner guide"
```

## 当前开发状态

- 文档结构已建立。
- 待完成 Markdown 链接、代码围栏、UTF-8、隐私扫描和远端可见性校验。

## 已知问题与解决方案

- 普通 OpenAI 兼容客户端一般使用 `https://www.fastaitoken.com/v1`。
- FastAiToken 的 Codex Responses 示例使用 `https://www.fastaitoken.com`，不带 `/v1`。
- OpenAI 官方 Codex 文档和安装方式可能更新，教程必须保留官方入口，并提醒读者复核当前命令。
- Windows PowerShell 可能阻止 `npm.ps1`；遇到执行策略错误时可使用 `npm.cmd`。

## 后续维护

- 平台价格或配置文档更新时，同步检查 README、倍率、计费、Codex 和客户端章节。
- 不提交真实 API Key、账户信息、余额截图或个人资料。
