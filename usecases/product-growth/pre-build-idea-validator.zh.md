---
title: OpenClaw 开发前创意验证器：编码前先做竞争现实校验
slug: pre-build-idea-validator
summary: 该案例在编码前对创意做多源竞争度验证，帮助团队基于现实信号决定继续、转向或停止，避免在高拥挤赛道盲目投入开发。
whatItDoes: 在项目启动前对创意进行多数据源竞争度评估，并输出支持 build/no-build 决策的信号结果。
category: product-growth
difficulty: intermediate
tags:
  - 创意验证
  - 市场竞争度
  - 开发前校验
  - 产品决策
targetUser:
  - 独立创业者
skillsUsed:
  - name: idea-reality-mcp
    href: https://github.com/mnemox-ai/idea-reality-mcp
updatedAt: '2026-03-12'
published: true
---

## 这个案例做什么
- 在写代码前执行基于证据的创意现实校验。
- 汇总 GitHub、Hacker News、npm、PyPI、Product Hunt 等来源的竞争信号。
- 输出分数驱动的决策路径（继续、转向、停止）及头部竞品参考。

## 所需技能
- [idea-reality-mcp](https://github.com/mnemox-ai/idea-reality-mcp)

## 痛点
团队常在验证前就进入开发，等发现赛道已有强势竞品时，已经消耗了大量工程时间与机会成本。

## 这个案例的核心价值
该案例把“开发前验证”变成硬门槛，降低无效研发投入，提升立项质量，并在高竞争场景下强制讨论差异化策略。

## 典型应用场景
- 黑客松选题前批量筛选创意。
- 资源有限时对创业方向做优先级选择。
- 内部需求立项前进行竞争格局评估。

## 如何设置
1. 安装并在智能体运行环境中注册 idea-check MCP 服务。
2. 按竞争度分数设置继续/转向/停止阈值规则。
3. 规定所有新项目在编码前必须附带分数与竞品证据。

## 相关链接
- [原始案例：开发前创意验证器](https://github.com/AlexAnys/awesome-openclaw-usecases/blob/main/usecases/pre-build-idea-validator.md)
- [idea-reality-mcp（GitHub）](https://github.com/mnemox-ai/idea-reality-mcp)
- [idea-reality-mcp（PyPI）](https://pypi.org/project/idea-reality-mcp/)

## 常见问题
### 高竞争分数是否等于不能做？
不一定。它意味着必须先明确差异化路径，再决定是否投入开发。

### 这个方法适合中国市场项目吗？
适合，且建议在全球扫描结果基础上补充国内平台数据交叉验证。

### 为什么要在编码前做，而不是 MVP 后再看？
因为最便宜的转向时机就是投入工程成本之前。