# 🌐 CF-Worker-AI-Translator

基于 **Cloudflare Workers** 构建的高性能 AI 翻译助手。集成了流式传输 (SSE)、长句翻译、单词深度解析以及 Cloudflare Turnstile 安全校验。

### ✨ 项目特性

* **⚡ 边缘加速**：运行在 Cloudflare 全球边缘网络，响应极速。
* **🤖 AI 智能识别**：自动判断输入内容：
    * **输入单词/短语**：自动转为“词典模式”，输出含义、词性、搭配及例句。
    * **输入长句/段落**：自动转为“翻译模式”，输出纯净、自然的译文。
* **🌊 流式输出**：基于 Server-Sent Events (SSE)，结果逐字呈现，无需漫长等待。
* **🛡️ 安全防护**：内置 **Cloudflare Turnstile** 人机验证，防止 API 接口被恶意刷取。
* **🌓 极致体验**：支持暗黑模式切换、翻译历史本地存储、一键复制。

---

### 🚀 快速部署 (极简版)

本项目采用**单文件部署**模式，无需本地开发环境。

#### 第一步：创建 Worker
1.  登录 [Cloudflare 控制台](https://dash.cloudflare.com/)。
2.  进入 **Workers & Pages** -> **Create application** -> **Create Worker**。
3.  设置名称（如 `ai-translator`）并点击 **Deploy**。
4.  点击 **Edit Code**，将本仓库 `worker.js` 中的全部代码复制并替换掉原有代码。
5.  点击右上角 **Save and Deploy**。

#### 第二步：配置环境变量 (必需)
在 Worker 管理界面，进入 **Settings** -> **Variables**，添加以下环境变量：

| 变量名称 | 类型 | 说明 | 示例值 |
| :--- | :--- | :--- | :--- |
| **`BASE_URL`** | Text | AI 接口的基础地址 | `https://api.openai.com/v1` |
| **`TURNSTILE_SITE_KEY`** | Text | Turnstile 的站点密钥 | `0x4AAAAAA...` |
| **`API_KEY`** | **Secret** | 你的 AI 接口密钥 | `sk-xxxxxx` |
| **`TURNSTILE_SECRET_KEY`** | **Secret** | Turnstile 的私钥 | `0x4AAAAAA...` |
| **`SESSION_SECRET`** | **Secret** | 随机字符串，用于会话签名 | `随便输入一段长字符` |

> **注意**：敏感信息请务必使用 **Secret** 类型存储（点击 `Encrypt` 加密）。

#### 第三步：设置 Turnstile
1.  在 Cloudflare 侧边栏进入 **Turnstile**。
2.  添加站点，域名填写你的 Worker 域名（例如 `xxx.workers.dev`）。
3.  将生成的 `Site Key` 和 `Secret Key` 填入上方的环境变量中。

---

### 🛠️ 进阶配置

如果你想更换使用的 AI 模型，只需在 `worker.js` 中搜索 `model` 字段（默认为 `gpt-4o-mini`），修改为你接口支持的模型名称即可。

### 📜 开源协议

本项目基于 **MIT** 协议开源。

---

**完成部署后，直接访问你的 Worker 链接即可开启你的专属 AI 翻译站！**
