# 常见报错排查

[上一章：客户端配置](06-client-config.md) · [返回首页](../README.md) · [下一章：安全](08-security.md)

## 先做这五项检查

遇到报错先不要反复充值或重新安装软件，按顺序检查：

1. API Key 是不是来自当前 FastAiToken 账户，首尾有没有空格。
2. 普通客户端的 Base URL 是否为 `https://www.fastaitoken.com/v1`。
3. Codex Responses 配置是否按专门示例使用不带 `/v1` 的地址。
4. 模型 ID 是否从当前控制台复制，而不是自己猜的。
5. 余额、密钥额度、模型分组和平台状态是否正常。

## 常见状态码

### 401 invalid_api_key

意思：平台无法接受当前 API Key。

处理：重新从密钥页面复制；检查漏字、空格、中文引号和密钥是否已删除或过期。不要把真实 Key 发到公开 Issue 求助。

### 429 insufficient_quota

意思：余额或可用额度不足。

处理：查看账户余额、API Key 限额和分组额度。先确认真实原因再充值。

### 429 rate_limit_exceeded

意思：短时间请求太多，触发速率限制。

处理：停止并发任务，等待片刻再试；降低并发和自动重试频率。它与“余额不足”同为 429，但原因不同，要看完整错误文字。

### 404 model_not_found

意思：填写的模型不存在，或当前 Key/分组不能使用。

处理：在控制台复制准确模型 ID，确认分组支持情况。不要把展示名称直接当作 ID。

### 400 invalid_request_error

意思：请求格式或参数不符合接口要求。

处理：先恢复客户端默认参数；检查 API 协议、消息格式、图片格式和上下文长度。普通 Chat Completions 与 Codex Responses 配置不能混用。

### 500 server_error

意思：服务端处理失败，可能是临时故障。

处理：记录时间、模型和请求 ID，稍后用短问题重试。持续发生时把脱敏后的错误信息交给平台支持。

### 403：Image generation is not enabled for this group

意思：当前分组没有开启图片生成功能。

处理：换到支持图片的分组或模型，并先核对按次价格。不要只更改模型名称而忽略分组权限。

## 连接超时或没有响应

- 换一个短问题，排除请求内容过大。
- 暂停代理、VPN 或安全软件后再做一次受控测试。
- 检查平台公告和客户端日志。
- 避免多个任务同时运行。
- 若客户端会自动重试，先关闭或降低次数，避免连续扣费。

## 地址错误的典型表现

如果日志里出现类似下面的地址，通常多写了一段路径：

```text
https://www.fastaitoken.com/v1/v1/chat/completions
```

正确目标通常应是：

```text
https://www.fastaitoken.com/v1/chat/completions
```

修改的是 Base URL，不要直接在多个位置同时追加 `/chat/completions`。

## 求助时提供什么

可以提供：

- 报错发生的时间
- 客户端名称和版本
- 使用的模型 ID 和分组名称
- 脱敏后的 Base URL
- 完整状态码与错误文字
- 平台返回的请求 ID（如果有）

不要提供：完整 API Key、密码、支付信息、私密对话或未经脱敏的日志。若怀疑密钥已经泄露，立即删除并重建，详见[安全须知](08-security.md)。

资料：[FastAiToken 疑难杂症](https://docs.fastaitoken.com/docs/help)

