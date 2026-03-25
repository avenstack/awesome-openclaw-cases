# Awesome OpenClaw 案例集

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](https://choosealicense.com/licenses/mit/)
[![Cases](https://img.shields.io/badge/cases-34-green.svg)](#案例)
[![Languages](https://img.shields.io/badge/languages-EN%2FCN-lightgrey.svg)](#语言)

**中文版 | [English](README.md)**

精选的真实 OpenClaw 用例集合，提供详细实施指南（中英文双语）。

> **在线浏览：[clawindex.app](https://clawindex.app)** - 探索、筛选和发现 OpenClaw 案例的交互式平台。

## 🎯 项目简介

本仓库包含结构化、详尽的案例研究，展示 OpenClaw 的真实应用场景。每个案例包括：

- **清晰的问题定义** - 解决什么痛点？
- **核心价值主张** - 这种方法的价值何在？
- **实施细节** - 所需技能、设置步骤、代码示例
- **典型应用场景** - 何时及如何应用此模式
- **常见问题** - 常见问题与解答
- **提供中英文版本** - 案例以两种语言提供

这些案例从社区展示、官方文档、博客文章和真实实现中提取，并结构化以实现最大复用性。

## 📚 按分类浏览案例

### 🔧 自动化集成
- [家庭数字剪贴簿](usecases/automation-integration/family-digital-scrapbook.zh.md) - 带日历上下文的自动照片日记
- [AI营养分析：Haver 餐食照片记录](usecases/automation-integration/food-photo-nutrition-logging.zh.md) - 用聊天和餐食照片记录营养数据
- [PDF文章转播客](usecases/automation-integration/pdf-articles-to-podcast.zh.md) - 通过 OpenClaw 技能把 PDF 链接转成可分享的双主持播客音频
- [OpenClaw 自我改进闭环](usecases/automation-integration/openclaw-self-improvement-loop.zh.md) - 把错误、纠正与能力缺口沉淀为可复用的工作流记忆
- [OpenClaw 三层记忆系统](usecases/automation-integration/openclaw-three-tier-memory-system.zh.md) - 跨会话上下文管理
- [RosClaw 机器人控制](usecases/automation-integration/rosclaw-robot-control.zh.md) - 通过消息应用实现自然语言 ROS2 机器人控制
- [微信自动发布流水线](usecases/automation-integration/wechat-auto-publishing-pipeline.zh.md) - 从选题到草稿的一键内容流水线
- [小红书全链路运营自动化](usecases/automation-integration/xiaohongshu-full-ops-automation.zh.md) - 端到端小红书运营
- [TweetClaw Twitter 自动化](usecases/automation-integration/tweetclaw-twitter-automation.zh.md) - 从聊天实现完整的 X/Twitter 自动化
- [OpenClaw n8n Stack](usecases/automation-integration/openclaw-n8n-stack.zh.md) - 自托管 AI 智能体与工作流自动化（400+ 服务集成）
- [多智能体编排专家](usecases/automation-integration/multi-agent-orchestration-specialists.zh.md) - 14+ 专职 AI 智能体并行执行（15 秒人类时间）
- [OpenClaw Home Assistant 插件](usecases/automation-integration/openclaw-home-assistant-addon.zh.md) - 智能家居 AI 网关，支持浏览器自动化
- [OpenClaw 自动化预测市场交易](usecases/automation-integration/openclaw-prediction-market-trading.zh.md) - 周收益 11.5 万美元的 Polymarket 自动化交易

### 📊 数据分析
- [语义记忆搜索](usecases/data-analytics/semantic-memory-search.zh.md) - 语义检索的知识召回
- [网络延迟基准测试](usecases/data-analytics/network-latency-benchmark.zh.md) - 多节点协调延迟分位数分析

### 🛠 工程实践
- [OpenClaw Opik 可观测性实践](usecases/engineering/openclaw-opik-observability.zh.md) - Opik 可观测性实践
- [Swift 日志包（TDD）](usecases/engineering/swift-logger-package-tdd.zh.md) - Swift 库的测试驱动开发
- [DevClaw 自主开发团队](usecases/engineering/devclaw-autonomous-dev-team.zh.md) - 多项目开发团队，节省 60-80% Token

### ⚙ 运维实践
- [Agent Ruler 审批门与审计回执](usecases/operations/agent-ruler-approval-gates.zh.md) - 为更安全的 OpenClaw 运行增加确定性审批与审计能力
- [活动嘉宾确认 Supercall](usecases/operations/event-guest-confirmation-supercall.zh.md) - 自动化嘉宾确认工作流
- [GitHub 长期 Issue 清理](usecases/operations/github-stale-issue-cleanup.zh.md) - 周期化 issue 管理与清理
- [日志异常检测](usecases/operations/log-anomaly-detection.zh.md) - 基于滚动基线的异常识别与告警
- [OpenClaw 自动化业务报表聚合](usecases/operations/openclaw-automated-business-reports.zh.md) - 多源数据采集与定时报表分发

### 🚀 产品增长
- [市场调研产品工厂](usecases/product-growth/market-research-product-factory.zh.md) - 从调研到产品化的流水线
- [社媒自动发布](usecases/product-growth/automated-social-media-posting.zh.md) - 内容起草、审核与定时发布一体化流程
- [比价购物助手](usecases/product-growth/price-comparison-shopping-assistant.zh.md) - 跨电商平台总成本比价
- [客户信号扫描器](usecases/product-growth/customer-signal-scanner.zh.md) - 社区反馈信号扫描与增长优先级提取
- [预构建想法验证器](usecases/product-growth/pre-build-idea-validator.zh.md) - 编码前多源竞争度校验
- [内容工厂](usecases/product-growth/content-factory.zh.md) - 多智能体内容生产与调研-写作-视觉链式编排
- [多渠道存在同步](usecases/product-growth/multi-channel-presence-sync.zh.md) - 跨平台内容分发与互动追踪
- [OpenClaw 商业化用例雷达](usecases/product-growth/openclaw-commercial-usecase-radar.zh.md) - 多来源热门用例信号整合
- [OpenClaw 产品经理助手](usecases/product-growth/openclaw-product-manager-copilot.zh.md) - 自托管 AI 助手：迭代评审、文档撰写与竞品情报

### 💬 客户支持
- [邮件自动分类器](usecases/support-success/email-auto-classifier.zh.md) - 按紧急度分流邮件并触发优先提醒
- [邮件沟通助手](usecases/support-success/email-communications-copilot.zh.md) - 收件箱清零、会议纪要提取与回复草稿

## 🚀 快速开始

### 1. 探索案例
浏览上述分类或访问 [clawindex.app](https://clawindex.app) 以获得：
- 按分类、难度、标签交互式筛选
- 全文搜索所有案例
- 可视化案例卡片及快速摘要

### 2. 适配你的需求
每个案例设计为：
- **可复用** - 清晰的结构和模式可供复制
- **可适配** - 根据特定需求修改
- **完整** - 包含设置步骤、所需技能和 FAQ

### 3. 贡献你自己的案例
有用例让社区受益？欢迎你的贡献！

**轻松提交**：您只需要提交**一种语言**（英文或中文）。我们会用机器翻译生成另一种语言版本！

参见 [贡献指南](#贡献指南) 了解详情。

## 🤝 贡献指南

欢迎 OpenClaw 社区贡献！我们的目标是构建全面的真实用例集合。

### 贡献内容

- **新案例** - 分享你独特的 OpenClaw 工作流（提交一种语言，我们处理翻译）
- **案例改进** - 增强现有案例的细节或结构
- **翻译** - 添加翻译或改进现有翻译
- **Bug 修复** - 修复拼写错误、断链或事实错误

### 案例编写规范

所有案例应遵循我们的结构化格式。**Frontmatter 是可选的** - 同步到 [clawindex.app](https://clawindex.app) 时会自动生成。

1. **Frontmatter**（可选）：
   ```yaml
   ---
   title: "SEO 友好标题：对象 + 动作 + 价值"
   slug: kebab-case-slug
   summary: 一句话摘要（中文 45-90 字，英文 20-35 词）
   whatItDoes: 动作 + 对象 + 输出结果（一句话）
   category: engineering | documentation | operations | security-compliance | data-analytics | product-growth | support-success | automation-integration
   difficulty: beginner | intermediate | advanced
   tags: [3-5 个标签，kebab-case]
   targetUser: [1-3 种用户类型]
   skillsUsed:
     - name: 技能名称
       href: /skills/skill-slug-or-https-url
   updatedAt: "YYYY-MM-DD"
   published: true
   ---
   ```

2. **正文结构**（必需）：
   - 这个案例做什么 / 所需技能 / 痛点 / 这个案例的核心价值 / 典型应用场景 / 相关链接 / 常见问题
   - 可选：如何设置（仅当来源有可靠设置流程时）

3. **语言支持**：
   - 创建 `slug.md`（英文）或 `slug.zh.md`（中文）- 您只需提交一种语言
   - 我们会用机器翻译自动生成另一种语言版本

4. **质量标准**：
   - 仅包含来源支撑的事实
   - 不虚构功能或数据
   - 技能必须是真实、可追溯的实体

### 提交流程

1. Fork 本仓库
2. 创建分支：`git checkout -b feature/your-case-slug`
3. 将案例文件添加到相应的 `usecases/` 分类目录
4. 提交并推送更改
5. 创建 Pull Request 并包含：
   - 清晰描述案例的标题
   - 原始来源链接（如适用）
   - 说明此案例的价值

## 📖 文档

有关案例编写的详细指南：

- 确保清晰的结构：问题陈述、价值主张、实施细节和常见问题
- 只需提交一种语言（英文或中文）；我们会处理翻译
- 仅包含可靠来源支撑的事实信息

## 🔗 相关链接

- [clawindex.app](https://clawindex.app) - 交互式案例浏览器
- [OpenClaw 文档](https://docs.openclaw.ai) - 官方 OpenClaw 文档
- [ClawHub](https://clawhub.ai/skills) - OpenClaw 技能市场
- [OpenClaw GitHub](https://github.com/openclaw/openclaw) - OpenClaw 源代码

## 📄 许可证

本项目采用 MIT 许可证 - 详见 [LICENSE](LICENSE) 文件。

## 📚 数据来源

本案例集的案例来源于：
- **社区展示** - 用户分享的真实 OpenClaw 工作流
- **官方文档** - OpenClaw 文档和指南
- **博客文章和教程** - 相关文章和实施指南
- **公开仓库** - 使用 OpenClaw 的 GitHub 项目

所有案例均基于真实用例和实现。
