# 注册到第一次请求

[上一章：计费](03-billing.md) · [返回首页](../README.md) · [下一章：Codex](05-openai-codex.md)

## 第 1 步：注册并登录

[点击注册 FastAiToken](https://www.fastaitoken.com/register?aff=BF9KNKFHX725)

> [!NOTE]
> 这个链接包含推广参数 `aff=BF9KNKFHX725`。通过它注册可能给本项目作者带来推广收益。

注册后先登录控制台。不要急着大额充值，第一次建议只准备足够完成小额测试的余额。

## 第 2 步：创建 API Key

打开 [API 密钥页面](https://www.fastaitoken.com/token)，创建一枚新密钥。

建议这样做：

- 名称写清用途，例如“我的 Chatbox”或“家用电脑 Codex”。
- 如果页面支持额度、有效期或模型限制，第一次先设置较小范围。
- 创建后立即把密钥保存到密码管理器。
- 不要把密钥发到群聊、截图或提交到 GitHub。

页面可能只完整显示一次密钥。教程中的 `sk-your-key` 是占位符，必须换成你自己的值。

## 第 3 步：确认模型和计费

在控制台价格或模型页面确认：

1. 想使用的模型当前是否可用。
2. 它属于哪个分组，倍率是多少。
3. 按 Token 还是按次计费。
4. 输入和输出单价是否不同。
5. 你要填入客户端的准确模型 ID。

不要只看到宣传名称就猜模型 ID。平台调整分组或模型后，旧名称也可能暂时不可用。

## 第 4 步：在客户端填写三项信息

普通 OpenAI 兼容客户端通常填写：

| 设置项 | 填写内容 |
| --- | --- |
| API 类型 | OpenAI 或 OpenAI Compatible |
| Base URL | `https://www.fastaitoken.com/v1` |
| API Key | 你在控制台创建的 `sk-...` |
| Model | 控制台中当前可用的准确模型 ID |

有的客户端会自动在地址后添加 `/v1`。如果它明确要求“不含 /v1 的主机地址”，就填写 `https://www.fastaitoken.com`。最终地址不能出现 `/v1/v1`。

## 第 5 步：发送最小测试

第一次只问一句：

```text
请只回复：连接成功
```

成功收到回复后，到平台的使用记录或日志页检查：

- 实际调用的模型
- 输入和输出 Token
- 所用分组与倍率
- 本次扣费

四项都符合预期，再开始正常使用。

## 可选：用命令行测试

Windows PowerShell 用户可以运行下面的示例。先把环境变量中的占位符换成自己的密钥，模型 ID 换成控制台当前显示的值。

```powershell
$env:FASTAI_API_KEY = "sk-your-key"
$body = @{
  model = "your-model-id"
  messages = @(
    @{ role = "user"; content = "请只回复：连接成功" }
  )
} | ConvertTo-Json -Depth 5

Invoke-RestMethod `
  -Uri "https://www.fastaitoken.com/v1/chat/completions" `
  -Method Post `
  -Headers @{ Authorization = "Bearer $env:FASTAI_API_KEY" } `
  -ContentType "application/json; charset=utf-8" `
  -Body ([System.Text.Encoding]::UTF8.GetBytes($body))
```

测试完成后可关闭当前 PowerShell 窗口，避免密钥继续留在这个会话的环境变量中。

## 成功标准

- 客户端没有提示 401、404 或余额不足。
- 返回内容来自你选择的模型。
- 使用记录出现且扣费符合预期。
- API Key 没有出现在公开文件或终端截图中。

接下来可以配置[OpenAI Codex](05-openai-codex.md)，或跳到[Chatbox 与其他客户端](06-client-config.md)。

资料：[FastAiToken 快速开始](https://docs.fastaitoken.com/docs/getting-started) · [API 手册](https://docs.fastaitoken.com/docs/api-manual)

