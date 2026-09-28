---
name: write
description: Writes a feature design doc (technical design document / TDD) following the Vesta team template. Use when the user asks to write a design doc, draft a TDD, turn a PRD into a technical plan, or bring an existing draft up to the team template format. 按 Vesta 团队模板写功能技术方案。当用户要「写技术方案」「出一份设计文档」「根据 PRD 写方案」「起草 tdd」，或要把已有草稿补齐成团队模板格式时使用。
disable-model-invocation: true
---

# 写功能技术方案

模板：`../../templates/vesta-design-doc-template.md`

**先完整读一遍模板**，按它的章节顺序写，每节照着该节的注释提示填。
模板里的注释是给作者看的说明，产出时删掉；`{{ }}` 占位全部替换掉。

## 动手之前：先摸现状

这一步花的时间通常比写字多，也是这份模板最看重的：

- 读 PRD（飞书链接用 `lark-doc` skill 读）
- **去代码里核实**现有接口、数据模型、配置 —— §3.1 现状能力盘点的价值全在可核对性。
  没读到的就写「未找到对应接口，需确认」，**不要按常见做法猜一个接口名填进去**

只问这几件你自己查不到的，一次问完，不要挤牙膏：

1. 本次**不包含**什么 —— 模板里最容易漏、评审时最容易吵的一项
2. 涉及哪几个服务 / 仓库

## 几处规则

- **不要替用户做产品决策。** 需求边界、优先级、业务规则拿不准，就列进「评审 TODO」并写上 owner，
  不要自己拍一个写进正文。技术选型可以给建议，而且根据情况可以给多个供用户决策。
- **不要为了填满模板而写。** 本次确实用不上的节，写一句「不适用：{{理由}}」，比硬凑三行废话好
- 图用 PlantUML 源码写进文档，不要贴截图

## 产出

默认写成本地 markdown：`{{功能名}}-tdd.md`，放用户指定的目录；没指定就跟随仓库惯例（`docs/` 或 `design/`）。

用户要发飞书时用 `lark-doc` skill。PlantUML 代码块需要人工用 `/文本绘图` 小组件渲染。
