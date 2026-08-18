# FastAiToken 小白入门指南

> [!TIP]
> **想直接开始？** [点击注册 FastAiToken](https://www.fastaitoken.com/register?aff=BF9KNKFHX725)
>
> 目前平台提供 **0.06 倍率 ChatGPT 分组**，可按平台当前规则使用 GPT-5.6 Sol、GPT-5.6 Terra 等模型，也可使用 Claude Fable 5。简单理解：如果某次调用的基准费用是 1 元，0.06 倍率下约扣 0.06 元。具体可用模型、分组、倍率和价格会调整，请以登录后的控制台为准。
>
> 上面的注册链接含推广参数 `aff=BF9KNKFHX725`。通过该链接注册可能给本项目作者带来推广收益，但不会改变本指南的阅读方式。

这是一份写给第一次接触 AI API 和“中转站”的中文入门手册。你不需要会编程，也不需要先弄懂一堆英文缩写。读完后，你应该能理解钱是怎么扣的、地址和密钥填在哪里，以及怎样让 Codex、Chatbox 等工具连接 FastAiToken。

## 先用一分钟理解

- **中转站（AI 网关）**：像一个统一前台。你的软件先把请求交给它，再由它转交给对应模型。
- **API Key**：像门钥匙，也是计费凭证。谁拿到它，谁就可能使用你的余额。
- **Base URL**：像收件地址，告诉软件把请求发到哪里。
- **Token**：模型处理文字时使用的计量单位，不完全等于汉字数或单词数。
- **倍率**：在基准费用上乘的价格系数。`0.06 倍率`不是“每次固定 0.06 元”。
- **余额**：账户还能消费多少钱；它不是 Token 数量。

最常见的费用估算方法是：

```text
实际费用 ≈ 模型基准费用 × 分组倍率
```

例如，某次请求按模型基准价算出 10 元，在 0.06 倍率分组下约为 `10 × 0.06 = 0.6 元`。实际账单还会受输入/输出 Token、模型、计费方式和平台规则影响。

## 从哪里开始

完全没有基础，建议按顺序阅读：

1. [什么是中转站](docs/01-what-is-a-relay.md)
2. [倍率到底是什么意思](docs/02-multiplier.md)
3. [Token、余额与计费模式](docs/03-billing.md)
4. [注册到第一次请求](docs/04-quick-start.md)
5. [OpenAI Codex 安装与使用](docs/05-openai-codex.md)
6. [Chatbox 与其他客户端配置](docs/06-client-config.md)
7. [常见报错排查](docs/07-troubleshooting.md)
8. [API Key 安全须知](docs/08-security.md)
9. [小白常见问题](docs/09-faq.md)

只想尽快用起来，可以直接看[快速开始](docs/04-quick-start.md)。想在终端里使用 AI 编程助手，可以直接看[Codex 教程](docs/05-openai-codex.md)。

## 你需要准备什么

- 一个 FastAiToken 账户
- 少量可用余额
- 一枚在控制台创建的 API Key
- 一个支持自定义 API 地址的客户端，例如 Codex 或 Chatbox

创建密钥的入口是 [FastAiToken API 密钥页面](https://www.fastaitoken.com/token)。普通 OpenAI 兼容客户端通常填写：

```text
Base URL: https://www.fastaitoken.com/v1
API Key:  sk-你自己创建的密钥
```

> [!IMPORTANT]
> Codex 的 Responses 配置示例使用 `https://www.fastaitoken.com`，不带 `/v1`。普通客户端和 Codex 的示例协议不同，不要把两个地址混用，也不要写出 `/v1/v1`。

## 阅读前说明

- 本仓库是第三方新手指南，不是 FastAiToken、OpenAI 或 Anthropic 的官方文档。
- 0.06 倍率、模型名称、优惠、分组和可用性都可能变化，以平台控制台的实时信息为准。
- “GPT-5.6 Sol”“GPT-5.6 Terra”“Claude Fable 5”等名称在这里按平台展示名称记录；选择前请在控制台确认当前模型 ID、分组和费用。
- 中转站能够接触你发送给模型的请求。不要提交密码、身份证、私有密钥、公司机密等敏感内容。
- 使用前请自行确认服务条款、隐私政策、退款规则以及所在地区的适用要求。

## 官方资料

- [FastAiToken 文档首页](https://docs.fastaitoken.com/docs/)
- [FastAiToken 快速开始](https://docs.fastaitoken.com/docs/getting-started)
- [FastAiToken 价格说明](https://docs.fastaitoken.com/docs/pricing)
- [FastAiToken API 手册](https://docs.fastaitoken.com/docs/api-manual)
- [FastAiToken 疑难杂症](https://docs.fastaitoken.com/docs/help)
- [OpenAI Codex 官方文档](https://developers.openai.com/codex/)

## 免责声明

本项目只提供学习和配置参考，不对服务稳定性、模型可用性、价格变化或第三方平台的处理行为作保证。充值前建议先小额测试，确认模型、速度、计费和客户端配置都符合自己的需要。
