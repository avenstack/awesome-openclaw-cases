# 为 Awesome OpenClaw 案例贡献

感谢您对 Awesome OpenClaw 案例集的贡献兴趣！本文档提供贡献的指南和说明。

## 🎯 我们的使命

我们正在构建全面的真实世界 OpenClaw 用例集合，帮助用户：

- **发现** OpenClaw 的实际应用
- **学习** 社区实现
- **适配** 经过验证的模式到自己的需求
- **回馈** 到生态系统

## 🤝 贡献方式

### 1. 添加新案例

有 OpenClaw 用例可以让他人受益？提交为新案例！

**重要提示**：您只需要提交**一种语言**（英文或中文）。我们会用机器翻译生成另一种语言版本！

**步骤：**
1. 查看相同分类的现有案例以了解风格
2. 遵循 [案例编写指南](#案例编写指南) 撰写案例
3. 用案例文件打开 Pull Request
4. 您的 PR 审核通过后，案例将自动同步到 [clawindex.app](https://clawindex.app)

**关于 Frontmatter 的说明**：提交时 Frontmatter **不是必需的**。当您的案例同步到 [clawindex.app](https://clawindex.app) 时，平台会自动为两种语言生成标准化的 frontmatter。

### 2. 改进现有案例

发现可以更好的案例？帮助改进它！

**改进类型：**
- 添加更多实施细节
- 澄清模糊的部分
- 添加缺失的 FAQ 条目
- 修复拼写或语法问题
- 更新过时的信息
- 添加更好的示例或代码片段

**步骤：**
1. Fork 本仓库
2. 找到您想改进的案例文件
3. 进行更改
4. 打开 Pull Request 并清晰描述改进内容

### 3. 添加翻译

**您可以通过两种方式翻译：**

#### 选项 A：翻译现有案例
1. 选择只存在于一种语言的案例
2. 创建 `slug.<lang>.md`（例如中文用 `slug.zh.md`）
3. 按相同结构翻译所有内容
4. 打开 Pull Request

#### 选项 B：机器翻译辅助
如果您只提交一种语言的案例，我们会用机器翻译生成另一种语言版本。这有助于我们：
- 接受可能不熟练使用两种语言的用户的贡献
- 快速扩展案例覆盖
- 通过审查保持语义对齐

**注意**：人工翻译始终优于机器翻译，但我们欢迎社区可以审查和改进的机器翻译草稿。

### 4. 报告问题

发现 Bug 或有建议？

- 打开 Issue 并包含：
  - 清楚描述问题的标题
  - 复现步骤（针对 Bug）
  - 预期 vs 实际行为
  - 如适用，提供截图

## 📝 案例编写指南

### 结构要求

您的案例应包含以下章节（frontmatter 可选）：

1. **标题**（顶部，H1）：清晰、描述性的标题
2. **正文**（英文案例必需章节）：
   - What it does
   - Skills You Need
   - Pain Point
   - Core value of this case
   - Typical scenarios
   - How to setup（可选，仅当来源有可靠设置流程）
   - Related Links
   - FAQ

3. **正文**（中文案例必需章节）：
   - 这个案例做什么
   - 所需技能
   - 痛点
   - 这个案例的核心价值
   - 典型应用场景
   - 如何设置（可选）
   - 相关链接
   - 常见问题

### Frontmatter（可选）

您**不需要在提交时包含 frontmatter**。但是，如果您想包含它，结构如下：

```yaml
---
title: "SEO 友好标题：对象 + 动作 + 价值"
slug: unique-kebab-case-slug
summary: 一句话摘要（英文 20-35 词，中文 45-90 字）
whatItDoes: 动作 + 对象 + 输出结果（一句话）
category: engineering | documentation | operations | security-compliance | data-analytics | product-growth | support-success | automation-integration
difficulty: beginner | intermediate | advanced
tags: [3-5 个标签，kebab-case]
targetUser: [1-3 种用户类型]
skillsUsed:
  - name: 技能名称
    href: /skills/slug-or-https-url
updatedAt: "YYYY-MM-DD"
published: true
---
```

**注意**：当您的 PR 审核通过后，[clawindex.app](https://clawindex.app) 会自动为两种语言版本生成标准化的 frontmatter。

### 内容指南

#### 应该做 ✅

- 使用真实来源：官方文档、博客文章、GitHub 仓库、发布说明
- 仅包含来源支持的事实
- 具体：什么问题、什么解决方案、什么价值
- 使用清晰、简洁的语言
- 添加相关链接且至少包含 1 个真实可访问的 URL
- 包含使用直接问答格式的 FAQ

#### 不应该做 ❌

- 不要虚构功能、数据或用户证言
- 不要使用模糊的营销语言，如"提升效率"但没有具体细节
- 不要从来源复制粘贴大段内容（摘要和结构化）
- 如果来源缺少可靠设置流程，不要添加"如何设置"
- 不要添加不存在或无法追溯的技能

### Skills Used 规则

如果您引用技能，它们必须是：
- 来自 ClawHub 或 GitHub 的真实、可追溯实体
- 使用有效 URL 引用
- 直接参与案例的核心工作流

### 分类选择

根据案例的**主要价值**选择一个主分类：

| 分类 | 焦点 | 示例 |
|------|---------|-----------|
| `engineering` | 软件开发、构建、测试、CI/CD | 代码质量、自动化、测试 |
| `documentation` | 文档生成、维护、工具链 | API 文档、自动文档、知识管理 |
| `operations` | 运维、监控、告警、故障排查 | 监控、日志、事故 |
| `security-compliance` | 安全扫描、合规、权限 | 漏洞扫描、审计、访问控制 |
| `data-analytics` | 数据收集、处理、分析 | 数据管道、指标、报表 |
| `product-growth` | 用户增长、优化、A/B 测试 | 用户分析、增长策略 |
| `support-success` | 客户服务、问题解决 | 自动支持、工单、FAQ |
| `automation-integration` | 第三方集成、工作流 | 服务集成、自动化、webhook |

### 标签指南

- 每个案例 **3-5 个标签**
- **kebab-case** 格式（小写、连字符）
- 使用行业标准术语（例如 `api-integration` 而非 `api-connect`）
- 至少包含 1 个场景标签 + 1 个结果标签

对于中文案例，翻译常用术语但保留：
- 品牌名：OpenClaw、GitHub、Docker
- 技术栈：React、FastAPI、LangGraph
- 行业术语：API、CI/CD

### 去重

创建新案例前：
1. 按 slug 和主题搜索现有案例
2. 如果主题显著重叠，**改进现有案例**而非创建重复条目
3. 使用 `slug` 作为唯一标识符

## 🌐 同步到 clawindex.app

您的 Pull Request 审核并批准后：

1. **自动 Frontmatter 生成**：平台会自动为英文和中文版本生成标准化的 frontmatter
2. **网站同步**：您的案例将出现在 [clawindex.app](https://clawindex.app) 并完成索引
3. **搜索集成**：用户可以通过平台上的搜索和筛选找到您的案例
4. **跨语言支持**：如果您只提交了一种语言，我们会用机器翻译生成另一种版本

**时间线**：PR 审批后，案例通常在 24-48 小时内同步。

## 📤 Pull Request 流程

1. **Fork** 本仓库
2. **创建分支**：`git checkout -b feature/your-case-slug`
3. **添加文件**：
   - 英文或中文：`usecases/category/slug.md` 或 `usecases/category/slug.zh.md`
   - 您只需要提交**一种语言**！
4. **提交**附带清晰消息：
   - `Add: [category] 案例名称`（针对新案例）
   - `Add translation: [category] 案例名称`（针对翻译）
   - `Fix: [category] 修正问题描述`（针对修复）
5. **推送**到您的 fork
6. **打开 PR**并包含：
   - 清晰标题：`[EN/ZH] Add/fix/improve: 案例名称`
   - 描述：
     - 此 PR 做什么
     - 原始来源链接（如适用）
     - 注明这是哪种语言（EN、ZH 或两者都有）
     - 任何额外上下文

**审批后**：您的案例将在 24-48 小时内自动同步到 [clawindex.app](https://clawindex.app)。

## 🎨 代码风格

- 对 frontmatter 使用 **YAML**（可选）
- 对正文使用 **Markdown**
- 遵循其他案例的现有格式
- 尽可能保持行在 100 字符以内
- 标题使用句子大小写（例如 "Pain Point" 而非 "pain point"）

## 📖 文档链接

- 确保清晰的结构：问题陈述、价值主张、实施细节和常见问题
- 您只需提交一种语言（英文或中文）；我们会处理翻译
- 仅包含可靠来源支撑的事实信息

## 🤝 社区指南

### 行为准则

- 尊重和包容
- 提供建设性反馈
- 假设善意
- 关注对社区最有利的方向

### 获取帮助

- 提问前检查现有案例
- 搜索相似问题的 Issue
- 加入 [OpenClaw Discord](https://discord.com/invite/clawd) 获取实时帮助

## 📊 影响

您的贡献通过以下方式帮助 OpenClaw 生态系统：

- **增长案例库** - 更多示例供用户学习
- **提高质量** - 通过同行评审改进文档
- **扩大覆盖** - 更多语言、更多领域
- **推动采用** - 经验证的模式帮助新用户更快上手
- **促进发现** - [clawindex.app](https://clawindex.app) 上的案例帮助用户更快找到解决方案

感谢您的贡献！🚀
