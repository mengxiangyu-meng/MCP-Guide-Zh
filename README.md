# 🔌 MCP 中文完全指南

> Model Context Protocol 教程 - 让 AI 连接一切

[![MCP](https://img.shields.io/badge/MCP-v1.0-blue?style=flat-square)](https://modelcontextprotocol.io)
[![Stars](https://img.shields.io/github/stars/modelcontextprotocol/modelcontextprotocol?style=flat-square)](https://github.com/modelcontextprotocol)
[![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)

---

## 📖 这是什么？

**MCP（Model Context Protocol）** 是 Anthropic 在 2024 年推出的开放标准，专门用来**连接 AI 和外部世界**。

简单说：
> **MCP = AI 的 USB-C 接口**

以前每个 AI 工具都要单独开发一套对接方式，就像手机充电 - 苹果用 Lightning，安卓用 Type-C，出门要带好几根线。

现在统一标准，一次对接，处处可用 - 就像 USB-C，一根线充所有！

---

## ✨ 为什么学 MCP？

| 特性 | 说明 |
|------|------|
| 🔗 统一标准 | 一次对接，处处运行 |
| 🛠️ 工具扩展 | AI 可以调用各种外部工具 |
| 📁 资源访问 | 读取文件、数据库、数据 |
| 🏠 自主可控 | 自己搭建 MCP 服务器 |
| 🌐 生态丰富 | 500+ 社区服务器可用 |

---

## 📚 教程目录

| 序号 | 章节标题 | 难度 | 描述 |
|:---:|---------|:---:|------|
| 01 | [MCP 简介](/docs/01-MCP简介.md) | 🟢 | 什么是 MCP？为什么重要？ |
| 02 | [MCP 原理](/docs/02-MCP原理.md) | 🟢 | 架构解析、三角色、通信流程 |
| 03 | [MCP 客户端](/docs/03-MCP客户端.md) | 🟡 | Claude/Cursor/VS Code/OpenClaw 配置 |
| 04 | [MCP 服务器](/docs/04-MCP服务器.md) | 🟡 | 官方服务器、社区服务器 |
| 05 | [自建 MCP 服务器](/docs/05-自建MCP服务器.md) | 🔴 | 从零开发自己的 MCP 服务 |
| 06 | [MCP 生态](/docs/06-MCP生态.md) | 🟢 | 生态一览、未来展望 |

> 🕐 预计学习时间：**新手 1 小时 → 熟练 半天**

---

## 🚀 快速开始

### 1. 安装 Node.js

```bash
# macOS
brew install node

# Ubuntu/Debian
curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash -
sudo apt-get install -y nodejs
```

### 2. 配置 Claude Desktop

创建配置文件：

```bash
# macOS
~/Library/Application\ Support/Claude/claude_desktop_config.json

# Linux
~/.config/Claude/claude_desktop_config.json
```

添加 MCP 服务器：

```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/你的文档路径"]
    }
  }
}
```

### 3. 重启 Claude

然后试试：

```
请列出我文档目录下的文件
```

如果能返回文件列表，说明 MCP 工作正常！🎉

---

## 🛠️ 核心概念

### 三角色

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

### 三种能力

| 能力 | 说明 | 示例 |
|------|------|------|
| 🔧 **Tools** | AI 可调用的函数 | 搜网页、算数学 |
| 📁 **Resources** | AI 可读取的数据 | 文件、数据库 |
| 💬 **Prompts** | 预设的提示模板 | 代码审查模板 |

---

## 📦 常用 MCP 服务器

| 服务器 | 功能 | 安装命令 |
|--------|------|----------|
| filesystem | 读写本地文件 | `npx -y @modelcontextprotocol/server-filesystem /path` |
| git | Git 操作 | `npx -y @modelcontextprotocol/server-git` |
| github | GitHub API | `npx -y @modelcontextprotocol/server-github` |
| slack | Slack 消息 | `npx -y @modelcontextprotocol/server-slack` |
| postgres | PostgreSQL | `npx -y @modelcontextprotocol/server-postgres` |
| sqlite | SQLite | `npx -y @modelcontextprotocol/server-sqlite` |

---

## 🎯 适合谁？

- ✅ 想让 AI 访问本地文件的开发者
- ✅ 想集成各种工具到 AI 的技术人员
- ✅ 想打造自己 AI 工具生态的团队
- ✅ 对 AI 工具连接感兴趣的任何人

---

## 🔧 环境要求

| 项目 | 要求 |
|------|------|
| Node.js | 18+ (推荐 22 LTS) |
| npm / npx | 随 Node.js 一起安装 |
| AI 客户端 | Claude Desktop / Cursor / VS Code / OpenClaw |

---

## 🏢 谁在用 MCP？

### 客户端

| 客户端 | 支持情况 |
|--------|----------|
| Claude (Anthropic) | ✅ 官方支持 |
| Claude Code | ✅ 官方支持 |
| ChatGPT (OpenAI) | ✅ 官方支持 |
| Cursor | ✅ 官方支持 |
| VS Code | ✅ 官方支持 |
| OpenClaw | ✅ 官方支持 |
| Zed | ✅ 官方支持 |

### 企业应用

| 类别 | 应用 |
|------|------|
| 💬 通讯 | Slack, Discord, Teams |
| 📁 文件 | Google Drive, Notion, Dropbox |
| 📊 数据库 | PostgreSQL, MySQL, MongoDB |
| 🔧 开发 | GitHub, GitLab, Jira |

---

## 📚 配套资源

- 🌐 [官网](https://modelcontextprotocol.io)
- 📚 [官方文档](https://docs.modelcontextprotocol.io)
- 💻 [GitHub](https://github.com/modelcontextprotocol)
- 💬 [Discord 社区](https://discord.gg/mcp)
- 📦 [服务器列表](https://github.com/topics/model-context-protocol)

---

## 🤝 贡献指南

欢迎提交 Issue 和 PR！

- 🐛 发现 bug → 提 [Issue](https://github.com/mengxiangyu-meng/MCP-Guide-Zh/issues)
- 💡 有建议 → 提 [PR](https://github.com/mengxiangyu-meng/MCP-Guide-Zh/pulls)
- 💬 讨论交流 → [Discussions](https://github.com/mengxiangyu-meng/MCP-Guide-Zh/discussions)

---

## 📄 License

MIT License

---

⭐ **有帮助的话，欢迎 Star！**

📢 **觉得有用就分享给朋友~**
