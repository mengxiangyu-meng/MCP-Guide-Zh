# 自建 MCP 服务器

> 从零开始开发自己的 MCP 服务器

---

## 5.1 准备工作

### 5.1.1 环境要求

```bash
# Node.js
node --version  # 需要 18+

# 或 Python
python --version  # 需要 3.10+
```

### 5.1.2 创建项目

```bash
# Node.js 项目
mkdir my-mcp-server && cd my-mcp-server
npm init -y
npm install @modelcontextprotocol/sdk

# Python 项目
mkdir my-mcp-server && cd my-mcp-server
pip install mcp
```

---

## 5.2 快速示例（Node.js）

### 5.2.1 主代码

```javascript
import { Server } from '@modelcontextprotocol/sdk/server/index.js';
import { StdioServerTransport } from '@modelcontextprotocol/sdk/server/stdio.js';
import { CallToolRequestSchema, ListToolsRequestSchema } from '@modelcontextprotocol/sdk/types.js';

// 定义工具
const tools = [
  {
    name: 'hello',
    description: '打招呼',
    inputSchema: {
      type: 'object',
      properties: {
        name: { type: 'string', description: '名字' }
      },
      required: ['name']
    }
  }
];

// 创建服务器
const server = new Server(
  { name: 'my-hello-server', version: '1.0.0' },
  { capabilities: { tools: {} } }
);

// 列出工具
server.setRequestHandler(ListToolsRequestSchema, async () => {
  return { tools };
});

// 调用工具
server.setRequestHandler(CallToolRequestSchema, async (request) => {
  const { name, arguments: args } = request.params;
  
  if (name === 'hello') {
    return {
      content: [
        { type: 'text', text: `你好，${args.name}！` }
      ]
    };
  }
  
  throw new Error(`未知工具: ${name}`);
});

// 启动
const transport = new StdioServerTransport();
await server.connect(transport);
```

### 5.2.2 运行

```bash
node index.js
```

---

## 5.3 快速示例（Python）

### 5.3.1 主代码

```python
from mcp.server import Server
from mcp.types import Tool, TextContent
import asyncio

# 创建服务器
app = Server("my-hello-server")

# 列出工具
@app.list_tools()
async def list_tools():
    return [
        Tool(
            name="hello",
            description="打招呼",
            inputSchema={
                "type": "object",
                "properties": {
                    "name": {"type": "string", "description": "名字"}
                },
                "required": ["name"]
            }
        )
    ]

# 调用工具
@app.call_tool()
async def call_tool(name: str, arguments: dict):
    if name == "hello":
        return [TextContent(type="text", text=f你好，{arguments['name']}！")]
    raise ValueError(f未知工具: {name}")

# 启动
if __name__ == "__main__":
    import mcp.server.stdio
    asyncio.run(mcp.server.stdio.run(app))
```

### 5.3.2 运行

```bash
python server.py
```

---

## 5.4 进阶：连接数据库

### 5.4.1 PostgreSQL 示例

```javascript
import pg from 'pg';
const { Pool } = pg;

const pool = new Pool({
  connectionString: process.env.DATABASE_URL
});

server.setRequestHandler(CallToolRequestSchema, async (request) => {
  const { name, arguments: args } = request.params;
  
  if (name === 'query_db') {
    const result = await pool.query(args.sql);
    return {
      content: [
        { type: 'text', text: JSON.stringify(result.rows) }
      ]
    };
  }
});
```

---

## 5.5 进阶：REST API

```javascript
server.setRequestHandler(CallToolRequestSchema, async (request) => {
  if (name === 'fetch_url') {
    const response = await fetch(args.url);
    const text = await response.text();
    return { content: [{ type: 'text', text }] };
  }
});
```

---

## 5.6 测试自己的服务器

### 5.6.1 配置到 Claude

```json
{
  "mcpServers": {
    "my-server": {
      "command": "node",
      "args": ["/path/to/your/server.js"]
    }
  }
}
```

### 5.6.2 测试

```
帮我调用一下我的服务器，打个招呼
```

---

## 5.7 发布到 npm（可选）

```bash
# 登录 npm
npm login

# 发布
npm publish
```

---

## 5.8 下一章

看看 MCP 生态有什么好玩的东西 → [06-MCP生态](./06-MCP生态.md)
