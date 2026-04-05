---
tags: [concept]
type: concept
---

# Skills 文件

给 AI 的"说明书"，以 Markdown (.md) 格式存储，让 AI 理解用户的业务环境和习惯。

## 作用

- 沉淀业务逻辑、常用配置、API 信息
- AI 读取后知道你的环境，搭出的工作流更贴合实际
- 随使用不断积累，AI 越来越懂你的业务
- **n8n Skills** 尤其关键：包含最佳实践和常见坑点，弥补通用 AI 对 n8n 节点配置和 Expression 语法不熟悉的短板

## 复利效应

Skills 文件积累了业务上下文（飞书表 ID、API 配置、输出规格等），每次搭建工作流都比上次更快、更准。

> 以前一个想法从冒出来到落地，可能折腾一两天。现在半小时就能看到原型。

## 具体 Skill 实例

- **n8n Skills**：n8n 节点配置最佳实践和常见坑点
- **[[agent-browser]]**：让 Claude Code 能打开网页抓取实时数据
- **competitive-profile-builder**：固定竞品分析框架，保证每次格式一致，可横向比较
- 安装方式：`npx skills add` 或 `claude plugin install`

## 来源

- [[source-claude-code-n8n-workflow|Claude Code + n8n = 工作流神器]]
- [[source-competitive-analysis-skill|竞品分析 Skill 实战]]
