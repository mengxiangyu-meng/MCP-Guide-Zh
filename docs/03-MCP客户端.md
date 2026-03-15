# MCP 客户端

> 在 Claude Desktop、Cursor、VS Code 中使用 MCP

---

## 3.1 Claude Desktop 配置

### 3.1.1 配置文件位置

```bash
# macOS
~/Library/Application\ Support/Claude/claude_desktop_config.json

# Windows
%APPDATA%\Claude\claude_desktop_config.json

# Linux
~/.config/Claude/claude_desktop_config.json
```

### 3.1.2 添加 MCP 服务器

```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/Users/你的用户名/Desktop"]
    },
    "git": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-git"]
    }
  }
}
```

### 3.1.3 重启 Claude

配置完成后，**重启 Claude Desktop** 才能生效。

---

## 3.2 Cursor 配置

### 3.2.1 打开设置

```
Cursor → Settings → Features → MCP Servers
```

### 3.2.2 添加服务器

点击 "+" 按钮，填入：

```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/path/to/folder"]
    }
  }
}
```

### 3.2.3 验证

添加后，在 Cursor 右侧可以看到 MCP 工具按钮。

---

## 3.3 VS Code 配置

### 3.3.1 安装扩展

1. 打开 VS Code
2. 搜索 "MCP"
3. 安装 `MCP Extension` 或 `Model Context Protocol`

### 3.3.2 配置

```json
// settings.json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/path"]
    }
  }
}
```

---

## 3.4 OpenClaw 配置

### 3.4.1 查看现有 MCP

```bash
openclaw mcp list
```

### 3.4.2 添加 MCP 服务器

```bash
# 添加官方服务器
openclaw mcp add filesystem --path /home/user/docs

# 添加社区服务器
openclaw mcp add github --token your-token
```

### 3.4.3 配置文件

```json
{
  "mcp": {
    "servers": {
      "filesystem": {
        "command": "npx",
        "args": ["-y", "@modelcontextprotocol/server-filesystem", "/path"]
      }
    }
  }
}
```

---

## 3.5 常用 MCP 服务器推荐

| 服务器 | 功能 | 安装命令 |
|--------|------|----------|
| filesystem | 读写本地文件 | npx -y @modelcontextprotocol/server-filesystem /path |
| git | Git 操作 | npx -y @modelcontextprotocol/server-git |
| github | GitHub API | npx -y @modelcontextprotocol/server-github |
| slack | Slack 消息 | npx -y @modelcontextprotocol/server-slack |
| postgres | 数据库 | npx -y @modelcontextprotocol/server-postgres |

---

## 3.6 验证 MCP 是否工作

### 在 Claude/Cursor 中测试

```
请列出我桌面上的文件
```

如果能看到文件列表，说明 MCP 工作正常！

---

## 3.7 常见问题

### Q1: MCP 不工作？

1. 检查配置文件格式是否正确
2. 重启 AI 客户端
3. 检查 npx 是否安装

### Q2: 权限被拒绝？

```bash
# 确保有执行权限
chmod +x ~/.npm-global/bin/*
```

---

## 3.8 下一章

想了解更多 MCP 服务器？ → [04-MCP服务器](./04-MCP服务器.md)
