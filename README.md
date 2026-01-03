<p align="center">
  <img src="https://img.shields.io/badge/version-1.0.0-00d4aa?style=flat-square" alt="Version">
  <img src="https://img.shields.io/badge/license-MIT-f0b429?style=flat-square" alt="License">
  <img src="https://img.shields.io/badge/PRs-welcome-00d4aa?style=flat-square" alt="PRs Welcome">
</p>

<h1 align="center">🔧 MCP 配置工具</h1>

<p align="center">
  <strong>一个现代化的 Model Context Protocol (MCP) 服务器配置可视化管理工具</strong>
</p>

<p align="center">
  告别手动编辑 JSON 配置文件的繁琐，通过直观的图形界面轻松管理你的 MCP 服务器
</p>

---

## 📖 目录

- [项目简介](#-项目简介)
- [功能特性](#-功能特性)
- [快速开始](#-快速开始)
- [使用指南](#-使用指南)
- [配置说明](#-配置说明)
- [界面预览](#-界面预览)
- [技术架构](#-技术架构)
- [常见问题](#-常见问题)
- [贡献指南](#-贡献指南)
- [更新日志](#-更新日志)
- [许可证](#-许可证)

---

## 🎯 项目简介

### 什么是 MCP？

**Model Context Protocol (MCP)** 是一种开放协议，用于标准化 AI 应用程序与外部数据源和工具之间的通信方式。它允许 AI 助手（如 Claude、Kiro 等）安全地访问本地服务、API 和各种数据源。

### 为什么需要这个工具？

MCP 服务器的配置通常存储在 `mcp.json` 文件中，手动编辑这些 JSON 配置文件存在以下痛点：

- ❌ JSON 语法错误难以排查
- ❌ 配置项繁多，容易遗漏
- ❌ 缺乏直观的状态管理
- ❌ 多服务器配置管理混乱

**MCP 配置工具** 正是为解决这些问题而生，它提供：

- ✅ 可视化的服务器管理界面
- ✅ 实时 JSON 预览与编辑
- ✅ 一键启用/禁用服务器
- ✅ 配置导入导出功能
- ✅ 表单验证与错误提示

---

## ✨ 功能特性

### 核心功能

| 功能 | 描述 |
|------|------|
| 🖥️ **服务器管理** | 添加、编辑、删除 MCP 服务器配置 |
| 🔄 **状态切换** | 一键启用或禁用服务器 |
| 📝 **JSON 编辑** | 实时预览和直接编辑 JSON 配置 |
| 📥 **导入配置** | 从现有 mcp.json 文件导入配置 |
| 📋 **复制导出** | 一键复制配置到剪贴板 |
| 🎨 **格式化** | 自动格式化 JSON 代码 |

### 支持的传输类型

#### stdio (标准输入输出)

适用于本地命令行工具，通过标准输入输出进行通信。

```json
{
  "command": "npx",
  "args": ["-y", "@modelcontextprotocol/server-filesystem"],
  "transportType": "stdio"
}
```

#### sse (Server-Sent Events)

适用于远程 HTTP 服务，通过 SSE 协议进行通信。

```json
{
  "url": "https://example.com/mcp/sse",
  "transportType": "sse"
}
```

### 高级配置

- **环境变量**: 为服务器设置自定义环境变量
- **自动批准**: 配置无需确认即可执行的工具列表
- **超时设置**: 自定义服务器响应超时时间
- **描述信息**: 为服务器添加说明文档

---

## 🚀 快速开始

### 方式一：直接打开

这是一个纯前端的单文件应用，无需安装任何依赖：

1. 下载 `mcp-config-tool.html` 文件
2. 双击用浏览器打开
3. 开始配置你的 MCP 服务器

### 方式二：本地服务器

如果你需要在本地开发环境中使用：

```bash
# 使用 Python
python -m http.server 8080

# 使用 Node.js
npx serve .

# 使用 PHP
php -S localhost:8080
```

然后访问 `http://localhost:8080/mcp-config-tool.html`

### 方式三：集成到项目

将文件复制到你的项目目录中，作为配置管理工具使用。

---

## 📚 使用指南

### 添加新服务器

1. 点击右上角的 **「添加服务器」** 按钮
2. 填写服务器配置信息：
   - **服务器名称**: 唯一标识符，如 `my-mcp-server`
   - **传输类型**: 选择 `stdio` 或 `sse`
   - **命令/URL**: 根据传输类型填写
   - **参数**: stdio 类型的命令行参数
   - **环境变量**: JSON 格式的环境变量
   - **自动批准**: 无需确认的工具列表
3. 点击 **「保存」** 完成添加

### 导入现有配置

1. 点击 **「导入」** 按钮
2. 粘贴你的 `mcp.json` 配置内容
3. 选择是否与现有配置合并
4. 点击 **「导入」** 完成

### 编辑服务器

1. 在服务器列表中找到目标服务器
2. 点击 **「编辑」** 按钮
3. 修改配置信息
4. 点击 **「保存」** 应用更改

### 启用/禁用服务器

- 点击服务器卡片上的 **「禁用」** 或 **「启用」** 按钮
- 禁用的服务器会显示为半透明状态
- 禁用不会删除配置，只是暂时停用

### 导出配置

1. 在右侧 JSON 预览面板查看配置
2. 点击 **「复制」** 按钮复制到剪贴板
3. 粘贴到你的 `mcp.json` 文件中

---

## ⚙️ 配置说明

### 配置文件结构

```json
{
  "mcpServers": {
    "server-name": {
      "description": "服务器描述（可选）",
      "command": "命令（stdio 类型必填）",
      "args": ["参数1", "参数2"],
      "url": "URL（sse 类型必填）",
      "env": {
        "API_KEY": "your-api-key"
      },
      "transportType": "stdio | sse",
      "autoApprove": ["tool1", "tool2"],
      "disabled": false
    }
  }
}
```

### 配置项详解

| 字段 | 类型 | 必填 | 描述 |
|------|------|------|------|
| `description` | string | 否 | 服务器的描述信息 |
| `command` | string | stdio 必填 | 要执行的命令 |
| `args` | string[] | 否 | 命令行参数数组 |
| `url` | string | sse 必填 | SSE 服务端点 URL |
| `env` | object | 否 | 环境变量键值对 |
| `transportType` | string | 是 | 传输类型：`stdio` 或 `sse` |
| `autoApprove` | string[] | 否 | 自动批准的工具名称列表 |
| `disabled` | boolean | 否 | 是否禁用此服务器 |
| `timeout` | number | 否 | 超时时间（秒） |

### 常用 MCP 服务器示例

#### 文件系统服务器

```json
{
  "filesystem": {
    "command": "npx",
    "args": ["-y", "@modelcontextprotocol/server-filesystem", "/path/to/allowed/dir"],
    "transportType": "stdio"
  }
}
```

#### GitHub 服务器

```json
{
  "github": {
    "command": "npx",
    "args": ["-y", "@modelcontextprotocol/server-github"],
    "env": {
      "GITHUB_PERSONAL_ACCESS_TOKEN": "your-token"
    },
    "transportType": "stdio"
  }
}
```

#### Playwright 浏览器服务器

```json
{
  "playwright": {
    "command": "npx",
    "args": ["-y", "@playwright/mcp-server"],
    "transportType": "stdio"
  }
}
```

#### 自定义 Python 服务器

```json
{
  "my-python-server": {
    "command": "uvx",
    "args": ["my-mcp-package@latest"],
    "env": {
      "FASTMCP_LOG_LEVEL": "ERROR"
    },
    "transportType": "stdio"
  }
}
```

---

## 🖼️ 界面预览

### 主界面布局

```
┌─────────────────────────────────────────────────────────────────┐
│  🔧 MCP 配置工具                          [导入] [添加服务器]    │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌─────────────────────┐    ┌─────────────────────┐            │
│  │   📡 服务器列表      │    │   { } JSON 预览     │            │
│  ├─────────────────────┤    ├─────────────────────┤            │
│  │                     │    │                     │            │
│  │  ┌───────────────┐  │    │  {                  │            │
│  │  │ server-1  ✓   │  │    │    "mcpServers": {  │            │
│  │  │ stdio | npx   │  │    │      "server-1": {  │            │
│  │  │ [编辑][禁用]  │  │    │        ...          │            │
│  │  └───────────────┘  │    │      }              │            │
│  │                     │    │    }                │            │
│  │  ┌───────────────┐  │    │  }                  │            │
│  │  │ server-2  ✗   │  │    │                     │            │
│  │  │ sse | https   │  │    │                     │            │
│  │  │ [编辑][启用]  │  │    │  [格式化] [复制]    │            │
│  │  └───────────────┘  │    │                     │            │
│  │                     │    │                     │            │
│  └─────────────────────┘    └─────────────────────┘            │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 设计特点

- **深色主题**: 护眼的深色配色方案
- **响应式布局**: 适配不同屏幕尺寸
- **状态指示**: 清晰的启用/禁用状态显示
- **实时同步**: 表单与 JSON 预览实时同步

---

## 🏗️ 技术架构

### 技术栈

| 技术 | 用途 |
|------|------|
| HTML5 | 页面结构 |
| CSS3 | 样式与动画 |
| Vanilla JavaScript | 交互逻辑 |
| IBM Plex 字体 | 界面排版 |

### 设计原则

- **零依赖**: 不依赖任何外部框架或库
- **单文件**: 所有代码集成在一个 HTML 文件中
- **离线可用**: 无需网络连接即可使用
- **隐私优先**: 所有数据仅在本地处理

### 文件结构

```
mcp-config-tool.html
├── <head>
│   └── <style>           # 所有 CSS 样式
├── <body>
│   ├── .header           # 页眉区域
│   ├── .main-layout      # 主布局
│   │   ├── .panel        # 服务器列表面板
│   │   └── .panel        # JSON 预览面板
│   ├── #modal            # 添加/编辑模态框
│   ├── #importModal      # 导入模态框
│   └── #toast            # 提示消息
└── <script>              # JavaScript 逻辑
```

### 核心函数

| 函数 | 功能 |
|------|------|
| `updateUI()` | 更新整体界面 |
| `renderServerList()` | 渲染服务器列表 |
| `updateJsonPreview()` | 更新 JSON 预览 |
| `saveServer()` | 保存服务器配置 |
| `toggleServer()` | 切换服务器状态 |
| `deleteServer()` | 删除服务器 |
| `doImport()` | 执行配置导入 |
| `copyJson()` | 复制 JSON 到剪贴板 |

---

## ❓ 常见问题

### Q: 配置保存在哪里？

A: 本工具不会自动保存配置到文件系统。你需要手动复制 JSON 配置并粘贴到你的 `mcp.json` 文件中。

常见的 MCP 配置文件位置：
- **Kiro**: `~/.kiro/settings/mcp.json` 或 `.kiro/settings/mcp.json`
- **Claude Desktop**: `~/Library/Application Support/Claude/claude_desktop_config.json` (macOS)
- **VS Code**: 项目根目录的 `.vscode/mcp.json`

### Q: 支持哪些浏览器？

A: 支持所有现代浏览器：
- Chrome 80+
- Firefox 75+
- Safari 13+
- Edge 80+

### Q: 如何添加自定义 MCP 服务器？

A: 
1. 确保你的 MCP 服务器已正确实现 MCP 协议
2. 在工具中添加新服务器
3. 填写正确的命令和参数
4. 导出配置并应用到你的 AI 应用

### Q: 环境变量格式是什么？

A: 环境变量需要使用 JSON 对象格式：

```json
{
  "API_KEY": "your-api-key",
  "DEBUG": "true",
  "CUSTOM_VAR": "value"
}
```

### Q: 如何处理敏感信息？

A: 
- 本工具完全在本地运行，不会上传任何数据
- 建议使用环境变量引用敏感信息
- 不要将包含 API 密钥的配置提交到公开仓库

---

## 🤝 贡献指南

欢迎贡献代码、报告问题或提出建议！

### 如何贡献

1. Fork 本仓库
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 开启 Pull Request

### 开发规范

- 保持代码简洁，遵循现有代码风格
- 添加必要的注释
- 测试所有更改
- 更新相关文档

### 问题反馈

如果你发现了 bug 或有功能建议，请：

1. 检查是否已有相关 issue
2. 创建新 issue，详细描述问题或建议
3. 如果可能，提供复现步骤或截图

---

## 📝 更新日志

### v1.0.0 (2026-01-03)

**首次发布**

- ✨ 服务器配置的增删改查
- ✨ 支持 stdio 和 sse 两种传输类型
- ✨ JSON 实时预览与编辑
- ✨ 配置导入导出功能
- ✨ 服务器启用/禁用切换
- ✨ 现代化深色主题界面
- ✨ 响应式布局设计

---

## 👨‍💻 作者 & 团队

<table>
  <tr>
    <td align="center" width="200">
      <a href="https://www.xudaozai.cn/">
        <img src="https://avatars.githubusercontent.com/u/xudao" width="100px;" alt="徐道"/>
        <br />
        <sub><b>徐道 (Xu Dao)</b></sub>
      </a>
      <br />
      <sub>🎯 总策划 & 产品设计</sub>
      <br /><br />
      <a href="https://www.xudaozai.cn/" title="Blog">🌐</a>
      <a href="https://github.com/xudao" title="GitHub">💻</a>
    </td>
    <td align="center" width="200">
      <a href="https://kiro.dev/">
        <img src="https://img.shields.io/badge/AI-Kiro-00d4aa?style=for-the-badge&logo=amazon-aws&logoColor=white" alt="Kiro"/>
        <br />
        <sub><b>Kiro</b></sub>
      </a>
      <br />
      <sub>🤖 AI 编程协助</sub>
      <br /><br />
      <a href="https://kiro.dev/" title="Kiro">🔗</a>
    </td>
  </tr>
</table>

### 关于项目团队

#### 🎯 总策划 - 徐道

> 一个热爱折腾的全栈开发者，专注于提升开发效率和用户体验。
> 
> 负责项目的整体规划、需求定义、产品设计和最终决策。
>
> 相信好的工具应该是简单、直观、优雅的。

#### 🤖 AI 协助 - Kiro

> [Kiro](https://kiro.dev/) 是由 AWS 推出的 AI 编程助手，专为开发者打造。
>
> 在本项目中，Kiro 协助完成了：
> - 💻 代码实现与优化
> - 🎨 UI/UX 设计建议
> - 📝 文档编写
> - 🐛 问题排查与修复
>
> 这是一次人机协作的完美实践，展示了 AI 辅助编程的无限可能。

---

### 联系方式

- 🌐 博客：[xudaozai.cn](https://www.xudaozai.cn/)
- 📧 邮箱：[联系作者]

> 如果你觉得这个工具有用，欢迎请我喝杯咖啡 ☕

---

## 📄 许可证

本项目采用 MIT 许可证 - 查看 [LICENSE](LICENSE) 文件了解详情。

```
MIT License

Copyright (c) 2026

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

<p align="center">
  <strong>如果这个工具对你有帮助，请给个 ⭐ Star 支持一下！</strong>
</p>

<p align="center">
  Made with ❤️ for the MCP Community
</p>
