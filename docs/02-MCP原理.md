# MCP 原理

> 深入理解 MCP 的架构和工作方式

---

## 2.1 MCP 三角色

MCP 有三个核心角色：

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│   AI 模型   │────▶│   MCP 主机   │────▶│  MCP 服务器  │
│  (Claude)  │     │ (你的电脑)  │     │ (工具服务)   │
└─────────────┘     └─────────────┘     └─────────────┘
```

| 角色 | 说明 | 示例 |
|------|------|------|
| 🤖 **MCP 主机** | 运行 AI 的程序 | Claude Desktop, Cursor |
| 🔌 **MCP 客户端** | 主机内部的连接器 | Claude 内部组件 |
| 🛠️ **MCP 服务器** | 提供工具/数据的外部服务 | 天气服务器、文件系统 |

---

## 2.2 通信流程

### 步骤 1: 初始化连接

```
主机 ──▶ 服务器: "你好，我能连接你吗？"
服务器 ──▶ 主机: "可以！这是我的能力列表（tools）"
```

### 步骤 2: AI 需要工具

```
用户 ──▶ AI: "帮我查下北京天气"

AI ──▶ 主机: "我需要调用天气工具"

主机 ──▶ 服务器: "调用 get_weather(北京)"

服务器 ──▶ 主机: "结果：25°C，晴天"

主机 ──▶ AI: "天气查到了，25度晴天"

AI ──▶ 用户: "北京今天25度，晴天哦~"
```

---

## 2.3 三种能力

### 2.3.1 Tools（工具）

AI 可以调用的函数：

```json
{
  "name": "get_weather",
  "description": "查询城市天气",
  "inputSchema": {
    "type": "object",
    "properties": {
      "city": {
        "type": "string",
        "description": "城市名称"
      }
    },
    "required": ["city"]
  }
}
```

### 2.3.2 Resources（资源）

AI 可以读取的数据：

```json
{
  "uri": "file:///home/user/README.md",
  "name": "用户自述文件",
  "description": "关于这个项目的说明"
}
```

### 2.3.3 Prompts（提示模板）

预设的提示词：

```json
{
  "name": "review-code",
  "description": "代码审查模板",
  "arguments": [
    {
      "name": "language",
      "description": "编程语言"
    }
  ]
}
```

---

## 2.4 连接方式

### 方式一：Stdio（本地进程）

适合本地工具：

```json
{
  "command": "npx",
  "args": ["-y", "@modelcontextprotocol/server-filesystem", "/path"]
}
```

### 方式二：SSE（远程服务）

适合远程服务器：

```json
{
  "url": "https://api.example.com/mcp"
}
```

---

## 2.5 安全性

| 安全机制 | 说明 |
|----------|------|
| 🔒 沙箱隔离 | MCP 服务器在隔离环境运行 |
| 📋 权限确认 | 调用前会询问用户 |
| ⏱️ 超时限制 | 防止长时间占用 |
| 🔑 密钥管理 | API Key 不暴露给 AI |

---

## 2.6 JSON-RPC 通信

MCP 使用 **JSON-RPC** 协议通信：

```json
// 请求
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "get_weather",
    "arguments": {"city": "北京"}
  }
}

// 响应
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "content": [
      {
        "type": "text",
        "text": "25°C，晴天"
      }
    ]
  }
}
```

---

## 2.7 下一章

了解了原理，怎么在常用工具里用 MCP？ → [03-MCP客户端](./03-MCP客户端.md)
