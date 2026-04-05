# LLM Wiki 使用说明

## 简介

LLM Wiki 是一种用 LLM 构建个人知识库的方法论。与传统 RAG（每次查询从头检索）不同，LLM 会**持续构建并维护一个结构化的 Markdown Wiki**，知识随每次导入和查询不断积累，形成复利效应。

> 类比：Obsidian 是 IDE，LLM 是程序员，Wiki 是代码库。
<img width="540" height="369" alt="image" src="https://github.com/user-attachments/assets/62e7f1f1-c167-4186-ac4f-0e5a596bacb3" />
<img width="673" height="959" alt="image" src="https://github.com/user-attachments/assets/e940afda-fe57-4e2d-8734-b2b6ca1baa87" />
---

## 安装 Skill

Skill 文件已位于 `~/.claude/skills/llm-wiki/SKILL.md`，Claude Code 会自动识别。

如果从 GitHub 克隆恢复，将 `skill/SKILL.md` 复制到对应位置即可：

```bash
mkdir -p ~/.claude/skills/llm-wiki
cp skill/SKILL.md ~/.claude/skills/llm-wiki/SKILL.md
```

---

## 目录结构

```
项目根目录/
  raw/                  # 原始资料（不可变，LLM 只读）
    assets/             # 图片、附件
    文章标题.md          # 剪藏的文章
  wiki/                 # LLM 生成维护的知识库页面
    index.md            # 内容索引目录
    log.md              # 操作日志（按时间追加）
    source-xxx.md       # 资料摘要页
    实体名.md            # 实体页（工具、产品、人物）
    概念名.md            # 概念页（方法论、模式）
    xxx-workflow.md     # 工作流页面
  skill/                # Skill 文件备份
    SKILL.md
```

### 页面命名规范

| 页面类型 | 命名格式 | 示例 |
|----------|---------|------|
| 资料摘要 | `source-{关键词}.md` | `source-claude-code-n8n-workflow.md` |
| 实体页 | `{实体名}.md` | `claude-code.md`、`n8n.md` |
| 概念页 | `{概念名}.md` | `two-layer-automation.md` |
| 工作流 | `{场景}-workflow.md` | `competitive-analysis-workflow.md` |

### 页面 Frontmatter 模板

```yaml
# 资料摘要页
---
tags: [source-summary, 领域标签1, 领域标签2]
source: "原文标题"
author: 作者名
date: YYYY-MM-DD
url: "原始链接"
---

# 实体页
---
tags: [entity, tool]
type: entity
---

# 概念页
---
tags: [concept]
type: concept
---
```

---

## 三大操作

### 1. Ingest（导入资料）

#### 如何获取资料

**推荐方式：Obsidian Web Clipper**

微信公众号等网站有反爬机制，无法直接通过命令行抓取。推荐流程：

1. 在浏览器安装 **Obsidian Web Clipper** 扩展
2. 打开文章，点击扩展图标剪藏为 Markdown
3. 将 `.md` 文件放入项目的 `raw/` 目录

剪藏后的文件自带 YAML frontmatter（title、source、author、created、tags），可直接利用。

#### 导入流程

将资料放入 `raw/` 目录后，告诉 Claude：

```
请导入 raw/文章标题.md 到知识库
```

Claude 会执行以下操作（一篇 2000-3000 字的文章通常触及 5-8 个文件）：

1. 阅读资料，与你讨论关键要点
2. 创建摘要页 `wiki/source-xxx.md`
3. 创建/更新相关实体页和概念页（通常 1-3 个新页面）
4. 在所有页面之间建立 `[[双向链接]]` 交叉引用
5. 更新 `wiki/index.md` 索引
6. 在 `wiki/log.md` 追加导入记录
7. 标注新资料与已有内容的矛盾或补充关系

#### 导入第二篇及以后的资料

知识库的价值在于积累。从第二篇开始，Claude 会额外做：

- **更新已有页面**：新案例/数据补充到已有的实体页和概念页，而非只创建新页面
- **标注跨资料关联**：多篇资料出现相似观点时在页面中明确标注
- **标注矛盾**：不同资料的冲突观点会被标注，不会偷偷覆盖

> 这就是复利——第 10 篇资料导入时，知识库的交叉引用和综合分析已经远超单篇文章能给你的。

### 2. Query（查询）

直接向 Claude 提问：

```
根据知识库，对比 X 和 Y 的区别
知识库里关于 XX 有什么要点？
总结一下目前所有资料的核心观点
```

Claude 会先读 `wiki/index.md` 定位相关页面，再深入阅读后综合回答。

**关键**：有价值的回答可以回写为新 Wiki 页面，让探索也能积累。

### 3. Lint（维护健康）

定期让 Claude 检查：

```
请检查知识库的健康状态
```

检查项目：
- 页面间的矛盾内容
- 被新资料取代的过时信息
- 无入站链接的孤立页面
- 被提及但缺少专属页面的重要概念
- 缺失的交叉引用
- 可填补的数据空白

---

## 快速开始（5 分钟上手）

### Step 1：初始化

在空文件夹中打开 Claude Code：

```
请帮我初始化一个 LLM Wiki 知识库
```

### Step 2：放入第一份资料

用 Obsidian Web Clipper 剪藏一篇文章，放到 `raw/` 目录：

```
请导入 raw/文章标题.md 到知识库
```

### Step 3：开始提问

```
知识库中关于 XX 话题有哪些要点？
```

### 日常使用速查

| 你做什么 | 说什么 |
|----------|--------|
| 刚开始 | "初始化一个知识库" |
| 加了新资料 | "导入 raw/文件名.md" |
| 想了解什么 | 直接问 |
| 维护检查 | "检查知识库健康状态" |

核心就一句话：**你负责找资料和提问，Claude 负责整理和维护。**

---

## 推荐工具搭配

| 工具 | 用途 | 必要性 |
|------|------|--------|
| **Obsidian** | 浏览 Wiki、查看图谱视图、实时预览页面关联 | 强烈推荐 |
| **Obsidian Web Clipper** | 浏览器一键剪藏网页文章为 Markdown | 强烈推荐 |
| **Git** | 版本控制，天然拥有历史记录 | 推荐 |
| **Dataview** (Obsidian 插件) | 基于 frontmatter 生成动态表格和列表 | 可选 |
| **Marp** | 从 Wiki 内容生成演示文稿 | 可选 |
| **qmd** | Wiki 页面搜索引擎（BM25 + 向量混合检索） | 大规模时需要 |

### Obsidian 推荐设置

- **附件目录**：Settings → Files and links → Attachment folder path → 设为 `raw/assets/`
- **下载附件快捷键**：Settings → Hotkeys → 搜索 "Download" → 绑定 `Ctrl+Shift+D`
- **图谱视图**：查看 Wiki 结构——哪些是枢纽页、哪些是孤立页

---

## 适用场景

- **个人成长** — 追踪目标、健康、心理、自我提升
- **研究** — 深入某个主题，持续数周/月，逐步构建全面 Wiki
- **读书** — 按章节记录，构建人物、主题、情节线索页
- **商业/团队** — 从 Slack、会议、项目文档中维护内部 Wiki
- **竞品分析、尽职调查、旅行规划、课程笔记** — 任何需要长期积累的场景

---

## 备份与恢复

### 备份到 GitHub

```
把当前项目推送到 GitHub
```

### 从 GitHub 恢复

```bash
git clone https://github.com/你的用户名/llm-wiki.git
# 恢复 Skill 到 Claude Code
mkdir -p ~/.claude/skills/llm-wiki
cp skill/SKILL.md ~/.claude/skills/llm-wiki/SKILL.md
```

### 同步到飞书知识库

```
把 Wiki 内容同步到飞书知识库
```

Claude 会调用飞书 API 创建文档并组织为知识库树状结构。

---

## 核心理念

> 维护知识库的繁重工作不是阅读和思考，而是记账——更新交叉引用、保持摘要最新、标注矛盾、维护一致性。人类因维护负担增长快于价值而放弃 Wiki。LLM 不会厌倦，不会忘记更新引用，一次操作可以触及 15 个文件。维护成本趋近于零，Wiki 就能持续运转。

**人类的工作**：策划资料来源、引导分析方向、提出好问题、思考意义。

**LLM 的工作**：总结、交叉引用、归档、记账——其余一切。

- 如果需要了解，共创，学习相关亚马逊运营Skill，请添加我们公众号和相关联系方式，进行分享相关亚马逊相关运营Skill源文件
![9f453825a605ac5a92149be126636dc4](https://github.com/user-attachments/assets/9680fd49-0f0f-4642-8601-462ca28f1c77)
![8acbe748b4a2e09b088c6e2b5cdfa85e](https://github.com/user-attachments/assets/86f00f61-cac6-4da1-9b4d-e78f75aecbc8)
---<img width="844" height="376" alt="image" src="https://github.com/user-attachments/assets/0c809a29-8dad-4fd0-b5ce-d439e250a60a" />

