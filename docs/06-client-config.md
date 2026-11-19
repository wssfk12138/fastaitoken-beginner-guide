# 06. Chatbox、Cherry Studio 与其他客户端配置

[⬅️ 上一章：OpenAI Codex 安装与使用](05-openai-codex.md) · [🏠 返回首页](../README.md) · [➡️ 下一章：常见报错排查](07-troubleshooting.md)

> [!TIP]
> **本章一句话看懂**：Chatbox、Cherry Studio、Cursor 和沉浸式翻译等工具通常都要配置 **地址（Base URL）、密钥（API Key）、模型 ID**。不同版本的字段、路径拼接和支持的协议可能不同，请按下表及软件当前说明核对。

---

## 一、主流软件怎么填？一眼速查表（不用自己猜带不带 `/v1`）

很多教程让新手自己去判断地址末尾到底加不加 `/v1`，其实常用软件一共就那几个，直接对照下面这张表抄作业最快：

| 你使用的客户端软件 | 接口类型（Provider）选什么？ | 接口地址（Base URL / API Host）填什么？ | 特别注意事项 |
| --- | --- | --- | --- |
| **Chatbox AI** | `OpenAI API` 或 `添加自定义提供方 (OpenAI 兼容)` | 通常填 `https://www.fastaitoken.com/v1`<br>*(若输入框下方预览已自带 `/v1/chat/completions`，则填 `https://www.fastaitoken.com`)* | 详见下方第二节步骤，或参考 [官方 Chatbox 文档](https://docs.fastaitoken.com/docs/%E4%BD%BF%E7%94%A8%E5%9C%BA%E6%99%AF/Chatbox%20AI) |
| **Cherry Studio** | 添加或选择 `OpenAI` 兼容服务商 | 填 `https://www.fastaitoken.com` 或 `https://www.fastaitoken.com/v1`（看地址框下方灰字预览，确保最终是 `.../v1/chat/completions` 即可） | 点击「管理 / 添加模型」手动输入控制台复制的准确模型 ID |
| **沉浸式翻译（浏览器插件）** | 选择 `OpenAI` 或 `自定义 OpenAI 兼容接口` | 填 `https://www.fastaitoken.com/v1/chat/completions`（若字段名叫完整接口地址 Endpoint）或 `https://www.fastaitoken.com/v1`（若字段名叫 Base URL） | 翻译网页非常高频，建议单独建一把设好额度上限的 Key |
| **Cursor / Cline / Roo Code** | 选择 `OpenAI Compatible` | 填 `https://www.fastaitoken.com/v1` | 模型 ID 必须严格复制控制台里当前分组支持的 ID |
| **OpenAI Codex (终端 CLI)** | `config.toml` 中设 `wire_api = "responses"` | 填 `https://www.fastaitoken.com` **（不带 `/v1`）** | 详见 [第 05 章 Codex 专章](05-openai-codex.md) |
| **CC Switch** | 支持控制台一键导入 | 在控制台 [API 密钥页](https://www.fastaitoken.com/keys) 直接点密钥右侧的 **`ccs`** 按钮导入 | 详见 [官方简易使用教程](https://docs.fastaitoken.com/docs/easyuse) |

> 💡 **一秒判断带不带 `/v1` 的万能绝招**：
> 现代客户端（如 Chatbox、Cherry Studio）在地址输入框正下方，往往会显示一行浅灰色的**“实际请求预览地址”**。你只要盯着那行预览字看：
> - ✅ 只要预览长这样：`https://www.fastaitoken.com/v1/chat/completions` 👉 **完全正确！**
> - ❌ 如果预览长这样：`https://www.fastaitoken.com/v1/v1/chat/completions` 👉 **多了个 `/v1`，把你填的 `/v1` 删掉即可！**
> - ❌ 如果预览长这样：`https://www.fastaitoken.com/chat/completions` 👉 **少了个 `/v1`，在你填的地址后面加上 `/v1` 即可！**

---

## 二、Chatbox AI 手把手配置步骤

1. 打开 Chatbox 软件，点击左下角的 **「设置（Settings）」**。
2. 在「模型提供方（AI Provider）」中，选择 **OpenAI API** 或点击 **添加自定义提供方（OpenAI 兼容模式）**。
3. **API 密钥（API Key）**：粘贴你在 FastAiToken 控制台创建的 `sk-...` 密钥。
4. **API 域名 / 地址（API Host / Base URL）**：填入 `https://www.fastaitoken.com/v1`（同时看一眼下方预览地址，确保没有变成 `/v1/v1`）。
5. **模型（Model）**：点击获取模型列表，或者直接点击「自定义模型 / 手动添加」，把你从控制台复制的准确模型 ID（如 `gpt-6.1-sol` 等）粘贴进去并选中它。
6. 点击保存，新建一个对话，发送 `请只回复：连接成功` 测试。

---

## 三、Cherry Studio 手把手配置步骤

Cherry Studio 是目前桌面端非常受新手欢迎的免费客户端，配置同样只需 1 分钟：

1. 打开 Cherry Studio，点击左下角的 **「⚙️ 设置」→「模型服务」**。
2. 点击底部的 **「+ 添加」**，名称填 `FastAiToken`，类型选择 **`OpenAI`**。
3. 在 **「API 密钥」** 栏粘贴你的 `sk-...` 密钥。
4. 在 **「API 地址」** 栏输入 `https://www.fastaitoken.com`（观察输入框正下方的灰色预览地址，只要预览末尾显示为 `/v1/chat/completions` 就不用再手动加 `/v1`；如果某些版本需要手动加，以预览为准）。
5. 往下滑点击 **「+ 添加」** 按钮手动输入你在控制台复制的准确模型 ID（或者点击「管理」从列表中勾选你所在分组支持的模型）。
6. 点击 API 密钥框旁边的 **「检测」** 按钮，选择刚刚添加的模型，提示连接成功即可去聊天界面愉快使用了！

---

## 四、为什么点了“获取模型列表”却是空的，或者搜不到我想用的模型？

不用慌！这通常**不是**你的账号坏了，而是下面两个原因之一：

1. **客户端不知道你选了哪个分组，或者需要你手动填名字**：
   很多第三方客户端自带的下拉菜单只写死了 OpenAI 几年前的老模型名字（比如 `gpt-4o`），根本没有收录平台最新的优惠分组模型。**解决办法**：不要管自带下拉菜单，直接点软件里的 **「+ 手动添加模型 / 自定义模型 ID」**，把你在 FastAiToken 控制台复制的模型 ID 贴进去就能正常调用！
2. **Base URL 多写了或少写了 `/v1`，或者 Key 首尾多带了空格**：
   按照上面第一节的“预览地址核对法”检查一下地址和密钥即可。

---

## 五、软件里那些英文参数（Temperature / Max Tokens）看不懂怎么办？

**一句话建议：看不懂就全部保持软件默认，一个都不用改！**

如果你实在好奇它们是干嘛的，这里给你做个最通俗的翻译：

- **Temperature（温度 / 随机性）**：数值越低（如 `0.2`），AI 说话越严谨一板一眼，适合写代码和翻译；数值越高（如 `0.8` ~ `1.0`），AI 说话越发散有创意，适合头脑风暴。默认一般不用动。
- **Max Tokens（最大输出长度）**：给 AI 回答字数设个上限，防止它一次吐出几万字停不下来。它只是一个“天花板”，设成 4000 不代表每次简短回答都会扣你 4000 Token 的钱。
- **上下文消息数（Context Count / History）**：决定每次发消息时顺带把前面几轮历史聊天记录发过去。想省钱的话，可以调成只携带最近 `5 ~ 10` 条，或者养成聊完一个话题就点「新建对话」的习惯。
- **流式输出（Stream）**：开启后 AI 会像打字机一样一个字一个字往外蹦；关掉则会等整段话写完再一次性啪地显示出来。保持默认开启体验最好。

---

## 下一步

如果你在点击“检测”或发送第一条消息时遇到了报错代码（比如 `401`、`404`、`429`），请立刻翻到下一章，10 秒钟就能查出原因：

👉 **[07. 常见报错 10 秒速查与排查](07-troubleshooting.md)**

*参考资料：[FastAiToken 文档中心（聊天与翻译分类）](https://docs.fastaitoken.com/docs/) · [FastAiToken Chatbox AI 文档](https://docs.fastaitoken.com/docs/%E4%BD%BF%E7%94%A8%E5%9C%BA%E6%99%AF/Chatbox%20AI)*
