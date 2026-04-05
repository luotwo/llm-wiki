---
tags: [concept, workflow]
type: concept
---

# 竞品分析工作流

基于 [[Claude Code]] + [[agent-browser]] + competitive-profile-builder 的自动化竞品分析流程。

## 目录结构

```
competitive/
  competitors.md              # 竞品清单（长期维护）
  profiles/
    competitor_a_2026Q1.md    # 各竞品信息档案（带日期版本）
    competitor_b_2026Q1.md
  comparison_report.md         # 完整对比报告
  executive_summary.md         # 一页纸摘要
```

## 流程

1. **准备**（5 分钟）：维护 `competitors.md`，列出链接和关注维度
2. **抓取**（30-40 分钟）：AI 逐个访问链接，生成竞品档案
3. **分析**（20 分钟）：横向对比，输出报告 + 摘要
4. **判断**（你来做）：验证数据、结合业务做战略决策

## 输出物

- **功能对比矩阵**：用 ✓ / ✗ / △ 标注各竞品功能覆盖
- **定价对比**：套餐结构、价格区间、性价比定位
- **差异化特征**：每个竞品最突出的方向
- **市场空白**：竞品都没覆盖好的方向
- **行动建议**：值得关注或借鉴的具体建议

## 最佳实践

- 竞品档案带日期命名，积累变化历史，辅助判断战略走向
- 竞品清单长期维护，季度更新只需改"重点关注"方向
- 不要追求 100% 自动化，抓不到的手动补充

## 与其他模式的共性

与 [[两层自动化]] 理念一致：让信息收集和格式整理回归低成本，把时间放在真正需要人来做的**判断**上。

## 来源

- [[source-competitive-analysis-skill|竞品分析 Skill 实战]]
