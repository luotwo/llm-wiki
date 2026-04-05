---
tags: [entity, tool]
type: entity
---

# agent-browser

浏览器自动化 Skill，让 [[Claude Code]] 能直接打开网页、提取页面内容。

## 安装

```
npx skills add vercel-labs/agent-browser@agent-browser -g -y
```

## 核心价值

解决 AI 数据新鲜度问题。传统 AI（ChatGPT、Deep Research）依赖训练数据，可能是几个月前的旧信息。agent-browser 是**真正打开浏览器访问页面**，拿到当天的实时数据。

## 应用场景

- **竞品分析**：访问竞品官网、定价页、App Store，抓取最新产品信息和定价
- **数据采集**：任何需要实时网页数据的场景

## 局限性

- 有反爬机制的网站可能无法完整抓取
- 需要登录的页面可能拿不到数据
- 遇到这类情况需手动补充

## 来源

- [[source-competitive-analysis-skill|竞品分析 Skill 实战]]
