# FastAiToken 小白入门指南

> [!TIP]
> **想直接开始？** 👉 **[点击注册 FastAiToken](https://www.fastaitoken.com/register?aff=BF9KNKFHX725&utm=fastaitoken-beginner-guide)**
>
> 目前平台提供 **0.06 倍率 ChatGPT 优惠分组**，可按平台当前规则使用 GPT-5.6 Sol、GPT-5.6 Terra、GPT-6.1 Sol 等模型，也可使用 Claude Fable 5 等模型。
> **用大白话理解 `0.06 倍率`**：相当于打 **0.6 折**——如果某次对话按官方基准价算出来是 **1 元**，在 0.06 倍率下大约只扣 **6 分钱（0.06 元）**。具体可用模型、分组、倍率和价格会随时间调整，请以登录后的控制台实时展示为准。
>
> *透明说明：上面的注册链接含推广参数 `aff=BF9KNKFHX725`。通过该链接注册可能给本项目作者带来推广收益，但不会增加你的任何费用，也不会改变本指南的阅读方式。*

这是一份专门写给**第一次接触 AI API 和“中转站”**的中文入门手册。你不需要会写代码，也不需要提前背诵一堆英文缩写。读完这份指南，你能清清楚楚搞懂：**钱是怎么算的、网址和密钥填在软件哪里、怎么避开新手最常踩的报错坑**。

---

## ⚡ 3 分钟极速上手（不想看长文？按这 4 步就能用）

如果你手头已经有 Chatbox、Cherry Studio、沉浸式翻译或 Codex 等工具，只需做完这 4 步即可跑通第一次对话：

1. **注册并准备小额余额**：打开 [FastAiToken 注册页](https://www.fastaitoken.com/register?aff=BF9KNKFHX725&utm=fastaitoken-beginner-guide) 注册登录。第一次建议只准备几元钱的小额余额（或按 [文档说明](https://docs.fastaitoken.com/docs/) 联系客服了解新用户福利），先测试跑通。
2. **创建一把绑定了分组的钥匙（API Key）**：进入 [API 密钥页面](https://www.fastaitoken.com/keys) 点击新建令牌。**重点**：在弹窗里的 **「分组」** 一栏选好你想用的优惠分组（如 0.06 倍率分组），额度先设一个小数字（如 `1`），生成后把 `sk-` 开头的密钥复制保存好。
3. **复制真实“模型 ID”**：去控制台的「可用渠道 / 模型价格」页面，找到你那个分组支持的模型，**直接点击复制它的真实模型 ID**（通常区分大小写和连字符，比如 `gpt-6.1-sol`，不要凭印象手打宣传名）。
4. **填进客户端并发送测试**：
   - **绝大多数聊天/翻译软件（Chatbox、Cherry Studio 等）**：
     ```text
     API 地址 (Base URL): https://www.fastaitoken.com/v1
     API 密钥 (API Key):  sk-刚才复制的密钥
     模型名称 (Model ID): 控制台复制的准确模型 ID
     ```
   - **OpenAI Codex 终端编程助手**（使用 Responses 协议，**不带 `/v1`**，详见 [Codex 专章](docs/05-openai-codex.md)）：
     ```text
     base_url = "https://www.fastaitoken.com"
     wire_api = "responses"
     ```
   - 发送一句 `请只回复：连接成功`，收到回复再去控制台「使用记录」看一眼扣费，就彻底大功告成了！

---

## 📖 核心黑话一分钟翻译表

第一次配软件时，你一定会在界面上看到这 6 个词。用“去商场点餐”来比喻，一秒就能看懂：

| 你在软件里看到的词 | 大白话是什么意思 | 你需要做什么 | 新手最容易踩的坑 |
| --- | --- | --- | --- |
| **中转站（AI 网关）** | **商场的统一服务台**。软件先把请求发给它，它再帮你转交给 OpenAI、Claude 等不同模型。 | 注册一个账号，在这里统一管余额和密钥。 | 以为中转站本身是个聊天软件（其实你还要配一个客户端软件，或者用网页自带的操练场）。 |
| **Base URL（接口地址）** | **收件地址**。告诉你的软件把请求寄到哪个网站。 | 普通软件填 `https://www.fastaitoken.com/v1`。 | 地址末尾多写了斜杠、重复变成 `/v1/v1`，或把 Codex 的无 `/v1` 地址跟普通软件混用。 |
| **API Key（令牌/密钥）** | **付款码 + 门钥匙**。以 `sk-` 开头，软件每次提问都靠它刷卡扣费。 | 在 [API 密钥页面](https://www.fastaitoken.com/keys) 创建，贴进软件设置里。 | 创建时没选对**「令牌分组」**，或者把带有真实 Key 的截图发到群里/GitHub 上被别人盗刷。 |
| **Model ID（模型 ID）** | **菜品编号**。指定这次让哪个 AI 模型来干活。 | 从控制台模型列表**一键复制**准确代码。 | 把网页海报上的宣传名（如 `GPT-5.6 Sol`）直接手打填进去，导致报 `404 模型不存在`。 |
| **Token（词元）** | **字数计价秤**。模型读入你的问题、写出回答时的最小字词计算单位。 | 粗略理解即可，约 500 个汉字 ≈ 1000 Token；实际以用量记录为准。 | 旧对话可能携带较多历史，输入量随之增加；具体还受客户端裁剪、摘要和缓存计费影响。 |
| **倍率（Multiplier）** | **折扣系数**。`实际扣费 ≈ 模型原价 × 分组倍率`。 | 在控制台选择低倍率优惠分组（如 `0.06 倍率`）。 | 误以为 `0.06 倍率` 是“每问一次固定收 0.06 元”（其实是原价乘 0.06，即打 **0.6 折**）。 |

---

## 🧭 按你的需求选阅读路线

### 路线 A：我想尽快把软件配好、立刻用起来
- 👉 **第一步**：[04. 注册到第一次请求（5 分钟保姆级实操）](docs/04-quick-start.md)
- 👉 **第二步（如果你用聊天/翻译软件）**：[06. Chatbox、Cherry Studio 与其他客户端配置](docs/06-client-config.md)
- 👉 **第二步（如果你用终端 AI 编程）**：[05. OpenAI Codex 安装与使用（含 CC Switch 一键导入与防坑命令）](docs/05-openai-codex.md)
- 👉 **卡住了看这里**：[07. 常见报错 10 秒速查与排查](docs/07-troubleshooting.md)

### 路线 B：我是纯零基础，想按顺序彻底搞懂怎么算钱、怎么省钱
1. [01. 什么是中转站（它和官方会员有什么区别？）](docs/01-what-is-a-relay.md)
2. [02. 倍率到底是什么意思（0.06 倍率是怎么算钱的？）](docs/02-multiplier.md)
3. [03. Token、余额与计费模式（为什么越聊越贵？怎么省钱？）](docs/03-billing.md)
4. [04. 注册到第一次请求（怎么选令牌分组与计费方式？）](docs/04-quick-start.md)
5. [05. OpenAI Codex 安装与使用（Windows 零基础避坑版）](docs/05-openai-codex.md)
6. [06. Chatbox、Cherry Studio 与其他客户端配置](docs/06-client-config.md)
7. [07. 常见报错排查（401 / 404 / 429 一眼定位）](docs/07-troubleshooting.md)
8. [08. API Key 安全须知（3 条铁律防盗刷）](docs/08-security.md)
9. [09. 小白常见问题 FAQ（14 个高频疑问解答）](docs/09-faq.md)

---

## ⚠️ 阅读前说明与安全边界

- **非官方教程声明**：本仓库是第三方整理的新手入门指南，不是 FastAiToken、OpenAI 或 Anthropic 的官方文档。
- **实时信息原则**：`0.06 倍率`、模型名称、优惠活动、分组规则和可用性都会随时间调整，一切请以登录后的平台控制台实时信息为准。
- **展示名 vs 模型 ID**：“GPT-5.6 Sol”“GPT-5.6 Terra”“GPT-6.1 Sol”“Claude Fable 5”等名称在本指南中仅按平台展示名称或文档示例记录；填写客户端前，请务必在控制台确认当前准确的模型 ID、所属分组和单价。
- **隐私与数据安全**：从技术原理上，任何中转站都需要接收你的请求才能转发给模型。请不要在对话中提交银行卡密码、身份证号、私有密钥、未脱敏客户资料或公司核心机密。
- **合规与条款**：使用前请自行查阅平台的服务条款、隐私政策、退款规则以及你所在地区的适用要求。

## 📷 真实界面图解

本版补充了 **2026-11-15** 在真实登录账户中截取的 7 张界面图：

- [创建密钥、选择分组、复制模型 ID 与核对账单](docs/04-quick-start.md)
- [查看输入、输出和缓存用量](docs/03-billing.md)
- [找到「导入到 CCS」入口，并安全配置 Codex](docs/05-openai-codex.md)

截图经账户所有者授权使用，Key 和 IP 已实色遮挡，用户名、余额、模型、分组与用量等其余信息按授权保留；未使用 AI 重绘界面。截图展示当时的账户与界面，不构成永久价格、支持范围或服务保障。

本次修订说明见 [修订说明](REVISION_NOTES.md)。

## 🔗 官方资料直达

- [FastAiToken 官方网站与控制台](https://www.fastaitoken.com/)
- [FastAiToken 文档中心首页](https://docs.fastaitoken.com/docs/)
- [FastAiToken 零基础简易使用（含 CC Switch 与 Codex 图文）](https://docs.fastaitoken.com/docs/easyuse)
- [FastAiToken 快速开始](https://docs.fastaitoken.com/docs/getting-started)
- [FastAiToken 价格与退款说明](https://docs.fastaitoken.com/docs/pricing)
- [FastAiToken API 手册](https://docs.fastaitoken.com/docs/api-manual)
- [FastAiToken 疑难杂症](https://docs.fastaitoken.com/docs/help)
- [OpenAI Codex 官方文档](https://developers.openai.com/codex/)

## 免责声明

本项目仅提供学习与客户端配置参考，不对服务稳定性、模型可用性、价格变化或第三方平台的处理行为作任何保证。充值前建议始终遵守**“小额充值、短句测试、核对账单”**原则，确认模型、速度、计费和客户端配置都符合自己的需要后再日常使用。
