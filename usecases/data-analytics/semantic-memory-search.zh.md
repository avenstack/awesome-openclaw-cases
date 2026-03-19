---
title: 用 memsearch 为 OpenClaw 记忆增加语义检索，快速找回历史决策
slug: semantic-memory-search
summary: 为 OpenClaw 的 markdown 记忆增加语义检索能力，让你按“含义”而不是关键词快速找回过去决策。
whatItDoes: 将 OpenClaw 的 memory markdown 文件建立向量检索层，并通过自然语言查询返回语义相关的历史记忆片段。
category: data-analytics
difficulty: intermediate
tags:
  - 语义搜索
  - 记忆检索
  - 向量索引
  - 决策召回
targetUser:
  - Agent 构建者
  - Agent 构建者
  - 知识工作者
skillsUsed:
  - name: memsearch
    href: https://github.com/zilliztech/memsearch
updatedAt: '2026-03-11'
published: true
---

## 这个案例做什么
- 为 OpenClaw 的 markdown 记忆建立可检索的向量索引。
- 支持按语义检索，即使措辞不同也能找到相关历史决策。
- 结合语义检索与关键词检索，提升记忆召回准确性。

## 所需技能
- [memsearch](https://github.com/zilliztech/memsearch)

## 痛点
当记忆文件持续增长后，人工翻找和关键词检索很难稳定命中关键结论。语义检索可以把长期记忆真正变成可用资产。

## 这个案例的核心价值
- 减少人工回溯历史上下文的时间。
- 提升长期项目中的决策连续性。
- 在保留 markdown 原始存储的同时增强检索效率。

## 典型应用场景
- 回查数周前的架构或工具选型结论。
- 找回某次流程变更背后的原始理由。
- 在规划评审时快速回答“我们以前怎么定的”。

## 如何设置
1. 在运行环境安装 `memsearch`。
2. 初始化 memsearch 配置并选择 embedding 后端。
3. 对 OpenClaw 的 memory 目录执行索引。
4. 执行语义查询，并按需开启 watch 模式做自动增量索引。

## 相关链接
- [memsearch GitHub](https://github.com/zilliztech/memsearch)
- [memsearch Documentation](https://zilliztech.github.io/memsearch/)

## 常见问题
### 这会替代 OpenClaw 的 markdown 记忆文件吗？
不会。markdown 仍是主存储，检索索引只是派生层。

### 只有超大规模记忆库才需要吗？
不是。中等规模记忆在“措辞不一致”时也能明显受益。

### 不用外部 API Key 可以运行吗？
可以。来源用例中提到了本地 embedding 的可选方案。