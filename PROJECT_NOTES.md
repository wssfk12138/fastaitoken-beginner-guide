# PROJECT_NOTES

## 最近状态摘要

- **2026-11-15 修订，2026-11-19 纳入 main 更新**：保护已有 Codex 配置，创建前检查并备份后停止；修正无依据比例与保证式措辞；恢复缓存/特殊能力计费和密钥安全边界；补充 7 张真实截图，并按现场将 API 密钥入口改为 `/keys`、模型价格入口改为 `/available-channels`。截图与功能验证日期为 2026-11-15，验证范围见 [修订说明](REVISION_NOTES.md)。

- **2026-11-14**：完成面向零基础读者的全面可读性与实操性升级：
  1. **阅读动线优化**：在 `README.md` 新增「3 分钟极速上手（4 步闭环）」「核心黑话一分钟翻译表」与「按需分流阅读路线」，并在每章顶部加入「本章一句话看懂」导读框；
  2. **实操盲区补齐**：在 `03-billing.md` 与 `04-quick-start.md` 补齐创建 API Key 时的「令牌分组（Group）」与「令牌计费方式（默认模式 vs 仅按量计费）」对照表，讲清怎么在控制台复制真实模型 ID 以及平台 30 天未使用余额无理由原路退回规则；
  3. **高频卡点根治**：在 `05-openai-codex.md` 补充官方推荐的 **CC Switch (`ccs`) 一键导入法**，并提供 **PowerShell 一键生成 `auth.json` 与 `config.toml` 命令**，帮助处理 Windows 隐藏 `.txt` 扩展名造成的配置问题；仍需检查其他登录原因；
  4. **客户端与排错速查**：在 `06-client-config.md` 新增主流软件（Chatbox、Cherry Studio、沉浸式翻译、Cursor、Codex、CC Switch）Base URL 速查表与 Cherry Studio 配置步骤；在 `07-troubleshooting.md` 顶部新增「报错代码 10 秒速查表」。
- **2026-08-18**：建立纯 Markdown 中文新手指南，覆盖中转站、倍率、计费、快速开始、Codex、通用客户端、排错、安全和 FAQ，并公开发布到 `wssfk12138/fastaitoken-beginner-guide`。

## 项目定位

面向第一次使用 AI 中转站和 API 的中文用户，用生活化比喻（点外卖、商场打折、免密支付卡）解释基础概念，并提供可直接复制核对的配置示例与排错速查表。

本仓库是第三方指南。涉及价格、分组、倍率、模型名称和可用性的内容必须标注“以平台控制台实时信息为准”，不得写成永久承诺。

## 推荐补充的 GitHub 仓库侧边栏信息（About & Topics）

目前 GitHub 仓库右侧的 `About` 栏为空（显示 `No description, website, or topics provided.`），建议在仓库主页右上角点击 `About` 旁边的 ⚙️ 齿轮图标，填入以下内容以提升读者第一印象与搜索可见度：

- **Description（简介）**：
  ```text
  面向零基础小白的 FastAiToken 与 AI API 中转站中文入门指南：一分钟看懂 Token、倍率与计费，手把手搞定 OpenAI Codex、CC Switch、Chatbox、Cherry Studio 配置与常见报错排查。
  ```
- **Website（网址）**：
  ```text
  https://docs.fastaitoken.com/docs/
  ```
- **Topics（标签，按空格分隔）**：
  ```text
  ai-api openai-codex chatbox cherry-studio beginner-guide llm-gateway chinese-tutorial fastaitoken
  ```

## 技术栈

- Markdown（利用 GitHub 原生 Alert 提示框 `[!TIP]` / `[!IMPORTANT]` / `[!WARNING]` / `[!CAUTION]` 与 `<details>` 折叠块优化视觉层级）
- GitHub 原生 README 与相对链接
- 无构建工具、无运行时依赖

## 常用命令

```powershell
git diff --check
git status --short
git add README.md PROJECT_NOTES.md docs
git commit -m "docs: improve readability and beginner onboarding workflows"
```

## 当前开发状态

- 11 个核心文档（`README.md`、`PROJECT_NOTES.md` 及 `docs/01` ~ `docs/09`）已完成可读性重构与交叉校验。
- 原压缩包曾自述通过全部校验；本次实际执行的链接、脚本和截图检查单独记录于修订说明，不以旧声明代替当前证据。

## 已知问题与解决方案

- 普通 OpenAI 兼容客户端一般使用 `https://www.fastaitoken.com/v1`（若客户端预览已自动追加 `/v1/chat/completions`，则填 `https://www.fastaitoken.com`）。
- FastAiToken 的 Codex Responses 示例使用 `https://www.fastaitoken.com`，不带 `/v1`。
- Windows 用户用记事本创建 `.codex/auth.json` 和 `.codex/config.toml` 时极易因隐藏扩展名生成 `.txt` 文件；指南提供 CC Switch 导入、扩展名检查和安全创建脚本；已有配置需先备份并手动合并。
- Windows PowerShell 可能阻止 `npm.ps1`；遇到执行策略错误时可使用 `npm.cmd`。

## 后续维护

- 平台价格、活动或配置文档更新时，同步检查 README、倍率、计费、Codex 和客户端章节。
- 不提交真实 API Key 或 IP。账户信息、余额截图与个人资料默认不公开；本版 7 张界面图经账户所有者明确授权，Key/IP 已遮挡，其余内容按授权保留。后续补图须核对授权范围。
