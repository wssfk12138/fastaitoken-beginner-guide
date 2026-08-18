# Chatbox 与其他客户端配置

[上一章：Codex](05-openai-codex.md) · [返回首页](../README.md) · [下一章：排错](07-troubleshooting.md)

大多数支持“OpenAI 兼容接口”或“自定义服务商”的客户端，都围绕三项信息配置：API 地址、API Key 和模型 ID。

## 通用填写模板

| 客户端字段可能叫作 | 通常填写 |
| --- | --- |
| Provider / API Type | OpenAI、OpenAI Compatible 或 Custom OpenAI |
| API Host / Base URL / Endpoint | `https://www.fastaitoken.com/v1` |
| API Key / Secret Key | 你创建的 `sk-...` |
| Model / Model ID | 控制台当前可用的准确模型 ID |

保存后先发送“请只回复：连接成功”，再到平台使用记录核对实际模型与扣费。

## Chatbox 配置思路

不同版本的菜单名称可能略有变化，通常按这个顺序：

1. 打开 Chatbox 设置。
2. 找到模型提供方或 AI Provider。
3. 选择 OpenAI API 或支持自定义地址的兼容选项。
4. 填入 API Key。
5. 将 API Host 或 Base URL 设为 `https://www.fastaitoken.com/v1`。
6. 选择或手动添加平台当前支持的模型 ID。
7. 保存并发送最小测试消息。

若 Chatbox 的输入框提示它会自动补全 `/v1`，主机地址就只填 `https://www.fastaitoken.com`。设置完成后检查最终请求不能包含 `/v1/v1`。

参考：[FastAiToken 的 Chatbox AI 文档](https://docs.fastaitoken.com/docs/%E4%BD%BF%E7%94%A8%E5%9C%BA%E6%99%AF/Chatbox%20AI)

## 不知道地址该不该带 /v1

先看客户端字段旁的示例：

- 示例类似 `https://api.openai.com/v1`：通常填写带 `/v1` 的地址。
- 示例类似 `https://api.openai.com`，并说明会自动追加版本路径：通常不带 `/v1`。
- 客户端使用 Responses 协议并提供服务商配置：按该客户端和平台的专门说明填写。Codex 示例见[上一章](05-openai-codex.md)。

仍不确定时，先查客户端自己的官方文档，不要反复随机改地址。

## 模型列表为空怎么办

部分客户端能从 `/v1/models` 自动获取模型，部分客户端需要手动输入。列表为空不一定代表 API 完全不可用，可以依次检查：

1. Base URL 有没有多写或少写 `/v1`。
2. API Key 是否完整，是否有首尾空格。
3. Key 是否被限制了模型或分组。
4. 客户端是否允许手动添加模型 ID。
5. 控制台中该模型当前是否可用。

## 参数不懂就先用默认值

客户端还可能显示 Temperature、Top P、Max Tokens、上下文长度等参数。第一次使用时保留默认值即可。

- **Temperature**：大致影响回答的随机性。
- **Max Tokens**：限制最多生成多长；并不代表一定会用完。
- **上下文长度**：一次能携带多少历史内容；越大不等于每次都更划算。
- **流式输出**：让文字逐步显示，通常不改变核心内容。

先把连接、模型和计费验证正确，再调整这些高级选项。

## 客户端能登录，不等于 API 已配置

有些客户端自己的登录账号只负责同步设置或购买客户端功能，不会自动获得模型额度。真正调用 FastAiToken 时，仍需填写 FastAiToken 的 Base URL、API Key，并保证账户有可用余额。

连接失败时进入[常见报错排查](07-troubleshooting.md)。

