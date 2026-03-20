---
title: DevClaw：将 OpenClaw 转变为自主多项目开发团队
slug: devclaw-autonomous-dev-team
summary: DevClaw插件将OpenClaw转变为自主开发团队，每个Telegram群组作为独立项目运行自动化DEV→QA→review管线，减少60-80%的token消耗。
whatItDoes: 将Telegram群组转变为独立开发团队，通过基于角色的worker（初级/中级/高级）自动执行GitHub/GitLab issue，支持会话复用和无token调度。
category: engineering
difficulty: intermediate
tags:
  - 自主开发
  - 多项目管线
  - GitHub集成
  - Token优化
targetUser:
  - 独立开发者
  - 小型开发团队
  - AI平台工程师
skillsUsed:
  - name: devclaw
    href: https://github.com/laurentenhoor/devclaw
updatedAt: '2026-03-20'
published: true
---

## 这个案例做什么
- 每个Telegram群组自动变成独立开发团队，你睡觉时代码自己写完
- 智能分配任务：简单改样式用便宜的模型，重构架构用强的模型，节省60-80%费用
- 多个项目同时跑，互不干扰，每个项目自动处理issue→开发→审查→合并的全流程

## 所需技能
- [devclaw](https://github.com/laurentenhoor/devclaw) - 用于开发编排的OpenClaw插件

## 痛点
AI编码工具承诺提升生产力，但往往需要人工看管：检查agent是否选择了正确的模型、是否正确转换了标签、是否维护了会话引用、是否从崩溃的worker中恢复。开发者花在管理agent上的时间比实际工作还多。

## 这个案例的核心价值
- **60-80% token节省**：分层选择（Haiku处理拼写错误，Opus处理架构）+ 会话复用（每任务40-60%）+ 无token调度
- **真正的自主性**：worker自报告完成，heartbeat自动合并已批准的PR，失败自动循环回DEV无需人工干预
- **多项目并行**：同时运行多个项目且完全隔离——每个项目独立队列、worker、会话和状态
- **审计追踪**：每次代码变更通过GitHub/GitLab链接到追踪的issue，完整NDJSON审计日志
- **合适的模型做合适的事**：CSS拼写错误用Haiku（~$0.001），数据库迁移用Opus（~$0.20）

## 典型应用场景
- **隔夜交付**：睡前创建issue，醒来后看到跨多个项目的已完成PR
- **多项目维护**：为webapp、API和移动项目并行运行独立开发团队
- **研究任务**：架构师worker调研设计问题（"如何迁移到OAuth2？"）并将发现作为issue评论发布
- **Bug修复循环**：QA失败 → 自动分发DEV修复 → 重新测试 → 通过后自动合并

## 如何设置
1. 安装DevClaw：`openclaw plugins install @laurentenhoor/devclaw`
2. 开始引导：在任何OpenClaw频道中说`"嘿，能帮我设置DevClaw吗？"`
3. 配置模型分配（默认：初级→Haiku，中级→Sonnet，高级→Opus）
4. 注册项目：将Telegram群组链接到GitHub/GitLab仓库
5. 在仓库中创建issue——管线自动处理其余工作

## 归档材料

### 角色到模型映射
DevClaw将模型选择抽象为开发者角色：

| 角色       | 级别     | 任务                          | 模型    |
|------------|-----------|--------------------------------|----------|
| Developer  | 初级    | 拼写错误、CSS修复、重命名      | Haiku    |
| Developer  | 中级    | 功能、bug修复            | Sonnet   |
| Developer  | 高级    | 架构、迁移       | Opus     |
| Reviewer   | 初级    | 标准代码审查           | Sonnet   |
| Reviewer   | 高级    | 安全审查、边缘情况    | Opus     |

### 管线状态机
```
Planning → To Do → Doing → To Review → Done（自动合并+关闭）
Planning → To Research → Researching → Planning（架构师发现）
```

### Heartbeat配置示例
```json
{
  "work_heartbeat": {
    "enabled": true,
    "intervalSeconds": 60,
    "maxPickupsPerTick": 4
  },
  "projectExecution": "parallel"
}
```

## 相关链接
- [DevClaw GitHub](https://github.com/laurentenhoor/devclaw)
- [DevClaw 官方文档](https://devclaw.dev/)
- [Show HN: Turn OpenClaw into a high performing development team](https://news.ycombinator.com/item?id=47010242)
- [Reddit: DevClaw v1.2.2 公告](https://www.reddit.com/r/OpenClawDevs/comments/1r558vz/devclaw_v122_turns_openclaw_into_a_high/)

## 常见问题
### 能否同时运行多个项目？
可以。每个项目完全隔离，拥有自己的队列、worker、会话和状态。默认情况下项目并行运行。

### PR收到审查反馈后会发生什么？
heartbeat检测到"请求更改"或合并冲突后，将标签移至"To Improve"，并自动分发之前的DEV级别进行修复。

### 是否需要手动管理会话引用？
不需要。DevClaw为每个项目的每个角色创建和复用持久会话。worker自动跨任务积累代码库上下文。

### 能否自定义每个角色使用的模型？
可以。角色到模型的映射在工作和项目级别设置中完全可配置。

### 如果worker在任务中途崩溃怎么办？
heartbeat健康检查检测卡住超过2小时的worker，将其标签恢复到队列，并停用它们以重试。
