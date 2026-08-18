# OpenAI Codex 安装与使用

[上一章：快速开始](04-quick-start.md) · [返回首页](../README.md) · [下一章：其他客户端](06-client-config.md)

Codex 是 OpenAI 提供的编程助手，可以在终端中读取和修改项目文件、运行命令并协助完成开发任务。本章介绍如何让 Codex CLI 使用 FastAiToken。

> [!WARNING]
> Codex 仍在持续更新。下面的安装命令和配置结构基于当前公开资料与 FastAiToken 配置文档；开始前请同时核对 [OpenAI Codex 官方文档](https://developers.openai.com/codex/) 和 [FastAiToken Codex 配置说明](https://docs.fastaitoken.com/docs/easyuse)。

## 1. 安装 Node.js

Codex CLI 的 npm 安装方式需要 Node.js 和 npm。打开 PowerShell，检查是否已经安装：

```powershell
node --version
npm --version
```

如果提示找不到命令，先从 [Node.js 官网](https://nodejs.org/) 安装当前受支持的 LTS 版本，安装后重新打开终端。

## 2. 安装 Codex CLI

当前常见安装命令是：

```powershell
npm install -g @openai/codex
```

Windows PowerShell 如果提示 `npm.ps1` 被执行策略阻止，可使用：

```powershell
npm.cmd install -g @openai/codex
```

然后检查：

```powershell
codex --version
```

如果官方文档已经给出不同命令，请以官方最新说明为准。

## 3. 找到 Codex 配置目录

Windows 用户目录下的配置位置通常是：

```text
C:\Users\你的用户名\.codex\
```

在 PowerShell 中可以打开它：

```powershell
explorer.exe "$env:USERPROFILE\.codex"
```

如果文件夹不存在，可以先运行一次 `codex`，或自行创建 `.codex` 文件夹。

## 4. 创建 auth.json

在 `.codex` 文件夹中创建 `auth.json`：

```json
{
  "OPENAI_API_KEY": "sk-your-key"
}
```

把 `sk-your-key` 换成自己在 FastAiToken 创建的密钥。不要把这个文件上传到 GitHub。

## 5. 创建 config.toml

在同一文件夹创建 `config.toml`：

```toml
model_provider = "custom"
model = "your-current-model-id"
model_reasoning_effort = "high"
disable_response_storage = true

[model_providers.custom]
name = "fastaitoken"
base_url = "https://www.fastaitoken.com"
wire_api = "responses"
requires_openai_auth = true
```

把 `your-current-model-id` 换成平台控制台当前支持、且适用于 Codex Responses 的准确模型 ID。

### 为什么这里没有 /v1

FastAiToken 的 Codex 示例使用 Responses 协议，并把 `base_url` 设置为：

```text
https://www.fastaitoken.com
```

普通 Chat Completions 客户端通常使用 `https://www.fastaitoken.com/v1`。两种配置面向的协议和客户端不同，请不要混用。

## 6. 第一次运行

先进入一个用于测试的项目目录：

```powershell
cd "C:\path\to\your-project"
codex
```

第一次可以只让它执行安全、容易验证的任务，例如：

```text
请阅读这个项目的 README，只总结它的用途，不修改任何文件。
```

确认能正常返回后，再尝试：

```text
请检查当前项目并告诉我如何运行测试，先不要修改文件。
```

Codex 能运行命令和改文件。执行删除、覆盖、安装依赖或推送代码前，务必看清它准备做什么，并保留 Git 版本或备份。

## 7. 怎么切换模型

最稳妥的方法是先在平台控制台复制当前模型 ID，再修改 `config.toml` 中的：

```toml
model = "your-current-model-id"
```

不要凭宣传名称猜大小写、连字符或版本后缀。GPT-5.6 Sol、GPT-5.6 Terra、Claude Fable 5 等平台展示名称、实际模型 ID、可用分组和倍率都可能变化。

## 常见问题

- **启动后要求登录官方账户**：检查 `auth.json`、`requires_openai_auth` 和文件位置是否正确。
- **404 或模型不存在**：模型 ID 不准确，或该分组当前不支持它。
- **请求地址错误**：检查 Codex 配置是否误写为 `/v1`，并确认 `wire_api = "responses"`。
- **密钥无效**：重新复制 API Key，避免首尾空格或中文引号。
- **扣费超出预期**：Codex 会读取较多项目上下文，也可能连续执行多轮；先用小项目、小任务测试并查看账单。

更多错误处理见[常见报错排查](07-troubleshooting.md)，密钥保护见[安全须知](08-security.md)。

资料：[OpenAI Codex 官方文档](https://developers.openai.com/codex/) · [FastAiToken 简易使用](https://docs.fastaitoken.com/docs/easyuse)
