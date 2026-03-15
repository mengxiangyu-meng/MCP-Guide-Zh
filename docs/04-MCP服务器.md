# MCP 服务器

> 现成的 MCP 服务器推荐与配置

---

## 4.1 官方服务器

Anthropic 官方维护的服务器：

| 服务器 | 功能 | 安装 |
|--------|------|------|
| filesystem | 本地文件读写 | npx -y @modelcontextprotocol/server-filesystem /path |
| git | Git 操作 | npx -y @modelcontextprotocol/server-git |
| gitmoji | Git 提交 emoji | npx -y @modelcontextprotocol/server-gitmoji |
| postgres | PostgreSQL 数据库 | npx -y @modelcontextprotocol/server-postgres |
| mysql | MySQL 数据库 | npx -y @modelcontextprotocol/server-mysql |
| sqlite | SQLite 数据库 | npx -y @modelcontextprotocol/server-sqlite |

---

## 4.2 社区热门服务器

### 4.2.1 GitHub

```bash
npx -y @modelcontextprotocol/server-github
```

功能：
- 查看 Issues/PR
- 创建/关闭 Issue
- 评论 PR

### 4.2.2 Slack

```bash
npx -y @modelcontextprotocol/server-slack
```

功能：
- 发送消息
- 读取频道
- 搜索历史

### 4.2.3 Notion

```bash
npx -y @notionhq/server-notion
```

功能：
- 读/写页面
- 搜索数据库
- 创建任务

### 4.2.4 Google Drive

```bash
npx -y @modelcontextprotocol/server-google-drive
```

功能：
- 读取文件
- 搜索文档
- 管理文件夹

---

## 4.3 配置示例

### 4.3.1 文件系统 + GitHub

```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/Users/用户名/Projects"]
    },
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_TOKEN": "ghp_xxx"
      }
    }
  }
}
```

### 4.3.2 数据库

```json
{
  "mcpServers": {
    "postgres": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-postgres"],
      "env": {
        "DATABASE_URL": "postgresql://user:pass@localhost:5432/db"
      }
    }
  }
}
```

---

## 4.4 中国区可用服务器

| 服务器 | 说明 | 地址 |
|--------|------|------|
| 飞书 | 飞书消息/文档 | 需自行配置 |
| 钉钉 | 钉钉消息 | 需自行配置 |
| 微信 | 企业微信 | 社区版 |

---

## 4.5 服务器列表资源

- 📚 [Awesome MCP Servers](https://github.com/topics/model-context-protocol)
- 🔗 [MCP Gallery](https://glmr.tv/s/mcp)
- 💬 [MCP Discord](https://discord.gg/mcp)

---

## 4.6 选择服务器的考虑

| 因素 | 说明 |
|------|------|
| 🔒 安全性 | 是否需要 API Key？数据是否本地处理？ |
| ⚡ 性能 | 本地 vs 远程 |
| 🛠️ 维护 | 官方 vs 社区（可能不再维护） |
| 📦 依赖 | 需要安装什么依赖？ |

---

## 4.7 下一章

想自己开发 MCP 服务器？ → [05-自建MCP服务器](./05-自建MCP服务器.md)
