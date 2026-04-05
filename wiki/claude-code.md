---
tags: [entity, tool]
type: entity
---

# Claude Code

Anthropic 出品的命令行 AI 助手。在终端里用自然语言交互，能写代码、操作文件、调 API、安装依赖、运行脚本。

## 核心特点

- 不是聊天机器人，是能**直接执行操作**的 AI
- 通过 [[MCP 协议]] 可连接外部工具（如 [[n8n MCP Server]]）
- 支持 [[Skills]] 文件（.md），读取后理解用户的业务环境和习惯
- 命令行界面，所有操作通过终端完成

## 在工作流场景中的角色

传统 AI（ChatGPT、Gemini 等）是**顾问**——告诉你怎么做，操作还是你自己来。
Claude Code 是**操盘手**——直接上手建工作流、改参数、跑测试。

与 [[n8n]] 配合构成 [[两层自动化]]：
- Claude Code 负责搭建（需要动脑子的部分）
- n8n 负责执行（固定流程的部分）

## 实战案例

- **搭建 n8n 工作流**：用自然语言描述需求，直接调 n8n API 创建工作流、配节点、测试（见 [[source-claude-code-n8n-workflow]]）
- **竞品分析**：配合 [[agent-browser]] 实时抓取竞品网页信息，配合分析 Skill 生成结构化报告，5 个竞品从 2 天压缩到 2 小时（见 [[source-competitive-analysis-skill]]）
- **产品图批量生成**：读取飞书表格 → 调 AI 生图 → 自动裁剪 → 回写，成本降低 99%

## 来源

- [[source-claude-code-n8n-workflow|Claude Code + n8n = 工作流神器]]
- [[source-competitive-analysis-skill|竞品分析 Skill 实战]]
