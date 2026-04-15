# yyapi.cc OpenAI 兼容格式 API · 完整对接文档

> 支持市面上所有主流 IDE / CLI / 应用，零门槛即插即用

---

# 一、快速开始

## 1.1 获取 API 密钥

1. 访问平台：**https://yyapi.cc**
2. 进入 **令牌管理 → API Keys**
3. 点击 **新建令牌**，复制生成的密钥（格式：`sk-xxxx`）

## 1.2 通用配置参数

| 配置项 | 值 |
|--------|-----|
| **基础地址（Base URL）** | `https://yyapi.cc/v1` |
| **API 密钥（API Key）** | `sk-xxxx`（你的密钥） |
| **协议** | OpenAI v1 兼容 |

---

# 二、IDE 对接教程

## 2.1 Cursor（最简单）

1. 打开 Cursor → 右下角 **设置图标**
2. 选择 **Models** → 下滑到 **OpenAI Compatible**
3. 点击 **Add Model**，填写：

| 配置项 | 值 |
|--------|-----|
| API Type | `OpenAI Compatible` |
| API Base URL | `https://yyapi.cc/v1` |
| API Key | `sk-xxxx` |
| Model ID | `claude-3.5-sonnet` |

4. 保存即可使用

---

## 2.2 VS Code + 插件对接

### CodeGPT（推荐）

1. 安装 **CodeGPT** 插件
2. `Ctrl+Shift+P` → `CodeGPT: Set API Key`
3. 填入：`sk-xxxx`
4. 设置 Provider 为 `OpenAI`，API Base URL：`https://yyapi.cc/v1`
5. 选择模型即可使用

### Cline（强大 CLI 工具）

1. 安装 **Cline** 插件
2. 点击 Cline 设置 → **Provider: OpenAI Compatible**
3. 配置：

```json
{
  "openaiApiKey": "sk-xxxx",
  "openaiBaseUrl": "https://yyapi.cc/v1"
}
```

### Continue（开源 AI 助手）

1. 安装 **Continue** 插件
2. 点击齿轮图标 → **Add Model** → **OpenAI Compatible**
3. 填写：

| 配置项 | 值 |
|--------|-----|
| Base URL | `https://yyapi.cc/v1` |
| API Key | `sk-xxxx` |
| Model | `claude-3.5-sonnet` |

### Roo Code（前身 Cody）

1. 安装 **Roo Code** 插件
2. 配置 Custom Endpoint：`https://yyapi.cc/v1`
3. 填入 API Key：`sk-xxxx`

### GitHub Copilot（第三方 Endpoint）

> 需要配合 **Fauxpaw** 或 **Copilot Gateway** 使用

---

## 2.3 JetBrains 全家桶（IDEA / PyCharm / WebStorm 等）

### 方式 1：内置 AI Assistant

1. `Settings → Tools → AI Assistant`
2. 选择 `Third-party providers → OpenAI-compatible`
3. 配置：

| 配置项 | 值 |
|--------|-----|
| API Key | `sk-xxxx` |
| API Endpoint | `https://yyapi.cc/v1` |

4. 点击 **Test Connection** → 成功即可

### 方式 2：Maxim（强烈推荐）

1. 安装 **Maxim** 插件（支持 JetBrains 全家桶）
2. 配置：

| 配置项 | 值 |
|--------|-----|
| API Key | `sk-xxxx` |
| Base URL | `https://yyapi.cc/v1` |

3. 支持所有 OpenAI 兼容模型

---

## 2.4 Claude Desktop / Claude Code

### Claude Desktop（Mac/Windows）

1. 打开 Claude Desktop 设置
2. 选择 **Developer Options**
3. 点击 **Edit Config File**，编辑 `claude_desktop_config.json`：

```json
{
  "mcpServers": {
    "claude": {
      "command": "npx",
      "args": ["-y", "@anthropic-ai/claude-code"],
      "env": {
        "ANTHROPIC_BASE_URL": "https://yyapi.cc/v1",
        "ANTHROPIC_AUTH_TOKEN": "sk-xxxx"
      }
    }
  }
}
```

### Claude Code CLI

**方式 1：环境变量**

```bash
# Linux/Mac（添加到 ~/.bashrc 或 ~/.zshrc）
export ANTHROPIC_BASE_URL="https://yyapi.cc/v1"
export ANTHROPIC_AUTH_TOKEN="sk-xxxx"
export ANTHROPIC_MODEL="claude-3.5-sonnet"

# Windows PowerShell
$env:ANTHROPIC_BASE_URL="https://yyapi.cc/v1"
$env:ANTHROPIC_AUTH_TOKEN="sk-xxxx"
```

**方式 2：配置文件**

编辑 `~/.claude/settings.json`：

```json
{
  "anthropic": {
    "baseURL": "https://yyapi.cc/v1",
    "apiKey": "sk-xxxx",
    "model": "claude-3.5-sonnet"
  }
}
```

---

## 2.5 Zed Editor

1. 打开设置 → **AI Providers**
2. 点击 **Add Provider** → 选择 **OpenAI Compatible**
3. 配置：

| 配置项 | 值 |
|--------|-----|
| Base URL | `https://yyapi.cc/v1` |
| API Key | `sk-xxxx` |

---

## 2.6 Sublime Text + AI 插件

1. 安装 **Superheated** 或 **CodeBoost** 插件
2. 配置 `Settings.sublime-settings`：

```json
{
  "api_key": "sk-xxxx",
  "base_url": "https://yyapi.cc/v1",
  "model": "claude-3.5-sonnet"
}
```

---

# 四、CLI / 终端工具对接

## 4.1 OpenAI CLI（官方命令行）

```bash
# 安装
pip install openai

# 配置环境变量
export OPENAI_API_KEY="sk-xxxx"
export OPENAI_API_BASE="https://yyapi.cc/v1"

# 使用
openai chat.completions.create \
  --model "gpt-4o" \
  --message "Hello"
```

## 4.2 Python 应用接入

```python
from openai import OpenAI

client = OpenAI(
    api_key="sk-xxxx",
    base_url="https://yyapi.cc/v1"
)

# 普通对话
response = client.chat.completions.create(
    model="claude-3.5-sonnet",
    messages=[
        {"role": "system", "content": "你是一个助手"},
        {"role": "user", "content": "你好"}
    ]
)
print(response.choices[0].message.content)

# 流式输出
stream = client.chat.completions.create(
    model="gpt-4o",
    messages=[{"role": "user", "content": "讲个笑话"}],
    stream=True
)
for chunk in stream:
    if chunk.choices[0].delta.content:
        print(chunk.choices[0].delta.content, end="", flush=True)
```

## 4.3 Node.js 应用接入

```javascript
import OpenAI from 'openai';

const client = new OpenAI({
  apiKey: 'sk-xxxx',
  baseURL: 'https://yyapi.cc/v1'
});

async function main() {
  const response = await client.chat.completions.create({
    model: 'claude-3.5-sonnet',
    messages: [{ role: 'user', content: '你好' }]
  });
  console.log(response.choices[0].message.content);
}

main();
```

## 4.4 LM Studio（本地 GUI）

1. 下载 **LM Studio**
2. 点击左侧 **AI Playgroud**
3. 选择 **OpenAI Compatible** 模式
4. 配置：

| 配置项 | 值 |
|--------|-----|
| Base URL | `https://yyapi.cc/v1` |
| API Key | `sk-xxxx` |

5. 选择模型即可使用

## 4.5 Jan（开源 ChatGPT 替代）

1. 下载 **Jan**
2. 进入 **Settings → OpenAI Keys**
3. 配置：

```json
{
  "base_url": "https://yyapi.cc/v1",
  "api_key": "sk-xxxx"
}
```

## 4.6 Ollama（本地模型管理）

配置远程 API：

```bash
# 设置代理到中转平台
export OLLAMA_HOST="https://yyapi.cc/v1"

# 或使用 OpenAI 兼容模式
ollama run gpt-4o
```

## 4.7 Tabby（AI 代码助手）

编辑 `~/.tabby/config.toml`：

```toml
[server]
endpoint = "https://yyapi.cc/v1"
api_key = "sk-xxxx"

[model]
name = "claude-3.5-sonnet"
```

## 4.8 Sourcegraph Cody

1. 安装 Cody 插件
2. 配置自定义 Endpoint：`https://yyapi.cc/v1`
3. 填入 API Key：`sk-xxxx`

---

# 五、cURL 快速测试

## 普通对话

```bash
curl https://yyapi.cc/v1/chat/completions \
  -H "Authorization: Bearer sk-xxxx" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "claude-3.5-sonnet",
    "messages": [
      {"role": "system", "content": "你是一个有帮助的助手"},
      {"role": "user", "content": "你好，请介绍一下自己"}
    ]
  }'
```

## 流式输出

```bash
curl https://yyapi.cc/v1/chat/completions \
  -H "Authorization: Bearer sk-xxxx" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gpt-4o",
    "messages": [{"role": "user", "content": "写一个 Python 快速排序"}],
    "stream": true
  }'
```

---

# 六、应用层接入

## 6.1 LangChain

```python
from langchain_openai import ChatOpenAI

llm = ChatOpenAI(
    openai_api_key="sk-xxxx",
    openai_api_base="https://yyapi.cc/v1",
    model="claude-3.5-sonnet"
)

response = llm.invoke("你好")
print(response.content)
```

## 6.2 LlamaIndex

```python
from llama_index.llms import OpenLike

llm = OpenLike(
    model="claude-3.5-sonnet",
    api_key="sk-xxxx",
    api_base="https://yyapi.cc/v1"
)

response = llm.complete("你好")
print(response.text)
```

## 6.3 CrewAI

```python
from crewai import Agent, Task, Crew

agent = Agent(
    role="AI Assistant",
    goal="提供帮助",
    backstory="你是一个有用的AI助手",
    llm="claude-3.5-sonnet",
    api_key="sk-xxxx",
    base_url="https://yyapi.cc/v1"
)
```

## 6.4 Dify（低代码平台）

1. 进入 **设置 → 模型供应商**
2. 选择 **OpenAI Compatible**
3. 配置：

| 配置项 | 值 |
|--------|-----|
| API Base URL | `https://yyapi.cc/v1` |
| API Key | `sk-xxxx` |

## 6.5 Coze / 扣子

1. 进入 **平台设置 → 自定义渠道**
2. 配置 OpenAI 兼容 Endpoint：`https://yyapi.cc/v1`
3. 填入 API Key

---

# 七、常见问题

## 7.1 401 未授权

**原因**：API Key 错误或已过期
**解决**：去平台重新复制密钥

## 7.2 404 Not Found

**原因**：Base URL 错误
**解决**：确保填写 `https://yyapi.cc/v1`（必须带 `/v1`）

## 7.3 模型不存在

**原因**：模型名称拼写错误
**解决**：使用本文档中的模型名称

## 7.4 请求超时

**原因**：网络问题或代理冲突
**解决**：
- 关闭本地代理
- 检查防火墙设置
- 平台国内可直连

## 7.5 余额不足

**原因**：账户余额耗尽
**解决**：去平台充值或查看套餐

## 7.6 流式输出无响应

**原因**：部分应用不支持 SSE
**解决**：在代码中设置 `stream: true`，或使用普通模式

---

# 八、注意事项

1. **API Key 安全**：不要在公开场合分享你的 API Key
2. **用量监控**：在平台仪表盘查看余额和请求统计
3. **模型选择**：根据需求选择合适模型，平衡性能和成本
4. **国内访问**：平台已优化，国内可直接访问

---

> 文档版本：v2.0 | 最后更新：2025年4月
