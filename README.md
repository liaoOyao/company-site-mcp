# company-site-mcp · 世福源供应链企业官网开放数据 MCP Server

[![MCP Registry](https://img.shields.io/badge/MCP%20Registry-net.shifuyuan%2Fcompany--site--mcp-blue)](https://registry.modelcontextprotocol.io)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

海南世福源供应链科技有限公司官网的**开放数据 MCP（Model Context Protocol）接口**——冻品火锅食材供应链（牛羊肉/丸滑/毛肚/海鲜/底料全品类厂家直采，海口冷链仓储，海南省内餐饮配送到店）的企业公开信息，以标准 MCP 协议向 AI 应用开放。

- **官方 Registry 收录**：`net.shifuyuan/company-site-mcp`（[server.json](./server.json)）
- **接入说明页（API Key 自助申请，即申即用）**：https://gys.shifuyuan.net/mcp
- **端点形态**：远程 `streamable-http`，标准 JSON-RPC 2.0（支持批处理）

## 快速接入

```bash
# 1. 到 https://gys.shifuyuan.net/mcp 自助申请 API Key（即申即用）
# 2. 任意 MCP 客户端配置远程端点：
```

```json
{
  "mcpServers": {
    "shifuyuan-supply-chain": {
      "type": "streamable-http",
      "url": "https://gys.shifuyuan.net/api/mcp/v1/rpc",
      "headers": { "X-API-Key": "<你的 API Key>" }
    }
  }
}
```

也支持 `Authorization: Bearer <key>` 或 query 参数 `?api_key=<key>` 传凭据。

### 徒手验证（curl）

```bash
curl -X POST https://gys.shifuyuan.net/api/mcp/v1/rpc \
  -H "Content-Type: application/json" \
  -H "X-API-Key: <你的 API Key>" \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/list","params":{}}'
```

## 工具清单（6 个，全部只读）

| 工具 | 说明 |
|---|---|
| `search_site_content` | 全站智能检索：产品/案例/FAQ/招聘/新闻综合搜索，支持分类过滤 |
| `get_company_profile` | 企业官方概况：全称/Slogan/电话/邮箱/地址/ICP 备案/业务板块 |
| `list_products` | 产品与服务矩阵：名称/分类/特性/规格指标 |
| `list_cases` | 成功案例：客户项目背景、解决方案、应用亮点与实施成效 |
| `list_jobs` | 招聘职位：岗位/地点/经验学历/薪资范围/职责要求/HR 对接渠道 |
| `get_latest_news` | 新闻动态：企业动态、行业报道与通知公告 |

## 配额与封禁

- 每个 API Key 有每日调用配额与每分钟频次限制（令牌桶）；
- 超配额返回 JSON-RPC 标准错误（-32000，HTTP 429）；
- 滥用会被毫秒级封禁（封禁原因随 403 返回）。

## 合规声明

- 本接口仅暴露**官网公开可见**的信息，无用户隐私与交易数据；
- 本仓库为接入说明文档仓库（MIT），服务端实现为商业产品、不开源；
- 数据最终解释权归海南世福源供应链科技有限公司所有。
