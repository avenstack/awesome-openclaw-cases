---
title: OpenClaw GitHub 陈旧 Issue 清理：用可审阅流程治理积压
slug: github-stale-issue-cleanup
summary: 该案例通过固定节奏识别长期无活动的 GitHub Issue，输出可审阅的关闭候选清单，在避免误关的前提下持续治理 issue 积压。
whatItDoes: 按 inactivity 规则识别陈旧 Issue，并输出可供人工审阅的清理候选，支持先提醒后关闭流程。
category: operations
difficulty: intermediate
tags:
  - issue治理
  - 积压清理
  - GitHub-Actions
  - 陈旧检测
targetUser:
  - 开源维护者
  - 工程团队负责人
  - 开发者体验团队
skillsUsed:
  - name: GitHub
    href: https://clawhub.ai/skills/git
updatedAt: '2026-03-12'
published: true
---

## 这个案例做什么
- 按固定调度扫描 GitHub open issues，识别超过阈值（如 30 天）无活动的问题。
- 输出“候选关闭列表”供维护者审阅，而不是直接批量关闭。
- 支持“先提醒再关闭”的节奏，为贡献者保留响应窗口。

## 所需技能
- [GitHub](https://clawhub.ai/skills/git)

## 痛点
Issue 积压会持续增长，人工清理又容易中断。大量长期无活动 issue 会淹没真正高优先级工作，导致维护决策变慢。

## 这个案例的核心价值
该案例把“临时清理”变成“稳定运营动作”：持续降低噪声 issue，保持人工最终决策权，并让仓库健康状态长期可见。

## 典型应用场景
- 中大型开源仓库的每周例行维护。
- 希望自动筛选但不希望自动误关的团队流程。
- 长期存在“无人跟进 issue”累积问题的仓库。

## 如何设置
1. 定义无活动策略（例如 30 天标记 stale，再过 14 天进入关闭候选）。
2. 配置定时工作流，自动打标并发送 stale 提醒评论。
3. 在最终关闭前加入维护者人工审阅步骤。

## 相关链接
- [GitHub 文档：用 actions/stale 关闭不活跃 Issue](https://docs.github.com/en/actions/tutorials/manage-your-work/close-inactive-issues)
- [actions/stale 仓库](https://github.com/actions/stale)

## 常见问题
### 陈旧 issue 一定要自动关闭吗？
不一定。对讨论周期较长的仓库，建议保留人工审阅关口。

### 阈值怎么定比较实用？
常见起点是“30 天标记 stale + 14 天后关闭”。

### 如何避免误关长期有价值的问题？
可在规则中排除 roadmap、安全、设计追踪等标签，再执行 stale 流程。