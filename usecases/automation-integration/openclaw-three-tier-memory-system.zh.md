---
title: OpenClaw 三层记忆系统：跨会话保留上下文并控制 Token 成本
slug: openclaw-three-tier-memory-system
summary: 该案例将 OpenClaw 记忆拆分为长期记忆、每日日志与项目状态三层，并结合语义检索，让智能体在跨会话场景下更稳定地找回关键信息。
whatItDoes: 将智能体记忆按长期、每日、项目三层组织，并通过语义检索快速召回相关上下文。
category: automation-integration
difficulty: intermediate
tags:
  - 记忆管理
  - 会话连续性
  - 语义检索
  - 智能体工作流
targetUser:
  - AI智能体开发者
  - OpenClaw运维人员
  - 自动化工程师
skillsUsed:
  - name: memory_search
    href: https://clawhub.ai/skills/memory-search
updatedAt: '2026-03-12'
published: true
---

## 这个案例做什么
- 将记忆拆分为三层：`MEMORY.md`（长期）、`memory/YYYY-MM-DD.md`（每日）、`PROJECTS.md`（项目状态）。
- 定义迁移规则，把临时记录沉淀为可复用的长期信息。
- 结合 `memory_search` 与 `memory_get`，提高历史决策召回速度。

## 所需技能
- [memory_search](https://clawhub.ai/skills/memory-search)

## 痛点
把所有内容放进一个大记忆文件，容易出现信息噪声：长期偏好、短期执行记录混在一起，检索质量下降，跨会话连续性也会变差。

## 这个案例的核心价值
三层结构把“长期稳定信息”和“短期执行上下文”分开管理，既能保留关键记忆，也能减少无效上下文堆积，提升后续会话的可读性与可检索性。

## 典型应用场景
- 持续运行多天/多周的个人智能体。
- 会话压缩或重启后快速恢复项目上下文。
- 降低团队在智能体流程中反复确认历史决策的成本。

## 如何设置
1. 在工作区根目录建立结构：
   - `MEMORY.md`
   - `PROJECTS.md`
   - `memory/YYYY-MM-DD.md`
2. 约定三层职责：
   - 长期原则与偏好写入 `MEMORY.md`
   - 每日事件与决策写入 `memory/YYYY-MM-DD.md`
   - 项目目标、阻塞与下一步写入 `PROJECTS.md`
3. 建立会话节奏：
   - 会话开始读取长期记忆 + 今昨日日志 + 项目状态。
   - 会话结束把可长期复用的信息从日志迁移到 `MEMORY.md`。
4. 检索时优先语义召回：先 `memory_search`，再用 `memory_get` 精读片段。

## 归档材料
来源中的典型三层目录结构：

```text
workspace/
├── MEMORY.md
├── PROJECTS.md
└── memory/
    ├── 2026-02-19.md
    └── heartbeat-state.json
```

## 相关链接
- [OpenClaw 文档：Memory](https://docs.openclaw.ai/concepts/memory.md)

## 常见问题
### 三层结构会替代向量检索吗？
不会。三层结构解决“怎么存”，向量检索解决“怎么找”，两者是互补关系。

### 一开始必须把三层都建好吗？
不是强制，但完整三层更容易避免长期偏好和临时执行记录混写。

### 每日日志什么时候迁移到长期记忆？
当该信息在多天后仍有复用价值时（例如稳定偏好、已确认的执行规则）。