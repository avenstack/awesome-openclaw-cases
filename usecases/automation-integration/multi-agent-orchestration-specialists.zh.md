---
title: OpenClaw 多智能体编排：14+ 专职智能体并行执行
slug: multi-agent-orchestration-specialists
summary: 使用 OpenClaw 的会话工具、沙箱和路由编排 14+ 专职 AI 智能体，在复杂多步骤任务中实现 15 秒人类时间。
whatItDoes: 配置多智能体编排系统，包含专职智能体、基于会话的委托、沙箱执行和并行任务路由，以自动化复杂工作流。
category: automation-integration
difficulty: advanced
tags:
  - 多智能体
  - 智能体编排
  - 并行执行
  - 沙箱隔离
  - 智能体路由
targetUser:
  - 构建 AI 团队的平台工程师
  - DevOps 团队
skillsUsed:
  - name: openclaw-multi-agent
    href: https://docs.openclaw.ai/concepts/multi-agent-routing
  - name: session-tools
    href: https://docs.openclaw.ai/concepts/session-tool
updatedAt: "2026-03-18"
published: true
---

## 这个案例做什么
- 编排 14+ 专职 AI 智能体（Kev 编排者 + Rex、Hawk、Scout、Dash、Dot、Pixel 等专家）
- 使用会话工具（`sessions_spawn`、`sessions_send`、`sessions_list`）进行并行智能体委托和结果聚合
- 配置每个智能体的沙箱隔离，支持 Docker 隔离、模式控制（off/non-main/all）和工作空间访问策略
- 通过绑定将不同通道（WhatsApp、Slack、Teams、webhooks）路由到特定智能体
- 在隔离环境（Clawdspace）中启用并行执行，实现并发任务处理
- 通过心跳和 webhook 触发的故障响应实现主动自动化
- 在复杂多步骤工作流中实现 15 秒人类时间 / 3 分钟智能体时间

## 所需技能
- [openclaw-multi-agent](https://docs.openclaw.ai/concepts/multi-agent-routing) - 多智能体路由和通道绑定
- [session-tools](https://docs.openclaw.ai/concepts/session-tool) - 会话管理、生成和跨智能体消息传递
- [sandboxing](https://docs.openclaw.ai/gateway/sandboxing) - Docker 沙箱配置、模式/作用域/workspaceAccess

## 痛点
构建可靠的多智能体系统面临根本性挑战：

- **协调混乱**：没有明确协议时，智能体会发送状态更新垃圾信息、重复工作、丢失交接
- **安全风险**：给予多个智能体完整系统访问权限会为模型错误造成不受控制的爆炸半径
- **性能瓶颈**：顺序智能体执行浪费可并行运行任务的时间
- **路由复杂性**：管理不同通道（Slack、WhatsApp、webhooks）到适当智能体的路由变得临时化
- **状态隔离**：没有适当的会话管理，智能体上下文会相互渗漏
- **成本低效**：在常规任务上运行高级模型会消耗预算而不产生价值

本案例展示了 OpenClaw 的会话工具、沙箱和路由原语如何将混乱的多智能体设置转变为具有可测量性能（15 秒人类 / 3 分钟智能体时间）的可靠工作流。

## 这个案例的核心价值
使用 OpenClaw 进行多智能体编排提供：

- **可测量的生产力**：15 秒人类努力即可实现跨越 7+ 专家的 3 分钟自动化智能体工作
- **专业化经济**：分配 Flash 进行总结（$0.02）、Codex 进行重构（$0.10）、Opus 进行编排（$0.30）——仅在关键之处支付高级推理
- **爆炸半径控制**：在 Docker 沙箱内运行 Rex（`mode: all`），而 Kev 在主机上操作——即使被恶意提示，Rex 也无法逃脱
- **并行吞吐量**：通过 Clawdspace 生成 100 个并发 Rex 实例，每个实例在隔离环境中处理不同的工单
- **可靠的委托**：带有自动结果聚合的 `sessions_spawn` 防止丢失交接——子智能体在完成时自动回复
- **始终在线的自动化**：心跳以固定节拍主动轮询；hooks 在外部系统触发时立即注入工作

## 典型应用场景
- **GitHub 驱动开发**：Kev 分类问题，生成 Rex 实现实施，委托 Hawk 进行安全审查，通过 PR 链接回复
- **故障响应工作流**：监控 webhook → 触发智能体调查 → AWS CLI + 日志分析 → 如需操作则通过 WhatsApp 升级
- **研究流水线**：Scout 通过 Flash 的海量上下文摄取整个 API 文档集，提炼为摘要供更智能的智能体综合
- **并行代码审查**：生成 N 个 Hawk 实例，每个审查不同的微服务，通过聚合报告合并输出
- **设计-开发交接**：Pixel 生成 UI 规范，Rex 实现组件，Hawk 验证安全性——全部由 Kev 编排，最小化人工监督

## 如何设置

### 1. 定义具有专业化的智能体名册

```yaml
agents:
  defaults:
    model:
      primary: google-antigravity/gemini-3-pro-high
    workspace: /Users/you/agents/kev
    sandbox:
      mode: non-main
      workspaceAccess: rw
      scope: agent
  list:
    - id: kev
      name: Kev
      model: anthropic/claude-opus-4-5
      sandbox:
        mode: off  # 编排者需要完整访问
    - id: rex
      name: Rex
      model: openai-codex/gpt-5.2-codex
      sandbox:
        mode: all  # 隔离编码任务
    - id: hawk
      name: Hawk
      model: anthropic/claude-opus-4-5
      tools:
        exec:
          allow: false  # 安全审查只读
    - id: scout
      name: Scout
      model: google-vertex/gemini-3-flash-preview  # 速度 + 海量上下文
```

### 2. 配置多智能体路由

```yaml
bindings:
  - agentId: kev
    match:
      channel: whatsapp
  - agentId: kev
    match:
      channel: slack
      accountId: kev
  - agentId: rex
    match:
      channel: slack
      channelId: engineering-reviews
```

### 3. 启用会话工具进行委托

```yaml
agents:
  list:
    - id: kev
      subagents:
        maxConcurrent: 10  # 控制并行生成
        allowedTargetIds: [rex, hawk, scout, dash, dot, pixel]
```

### 4. 按安全配置文件配置沙箱

```yaml
agents:
  list:
    - id: rex
      sandbox:
        mode: all
        backend: docker
        scope: session
        workspaceAccess: rw
    - id: hawk
      sandbox:
        mode: non-main
        workspaceAccess: ro  # 审查只读
```

### 5. 设置主动自动化

**心跳用于轮询：**
```yaml
agents:
  list:
    - id: kev
      heartbeat:
        every: 5m
        prompt: |
          检查标记为 'priority:high' 的新 GitHub 问题。
          如果发现，生成 Rex 实施，Hawk 审查。
```

**Webhook 用于事件驱动触发器：**
```yaml
hooks:
  enabled: true
  path: /hooks
  mappings:
    - match:
        path: alert
      action: agent
      sessionKey: hook:alert:{{id}}
      messageTemplate: |
        [ALERT]
        {{details}}
      deliver: true
```

### 6. 使用 Clawdspace 并行执行

```yaml
# 为并发智能体生成 N 个隔离环境
clawdspace:
  environments:
    - name: rex-1
      workspace: /tmp/rex-1
      image: openclaw-sandbox-common:bookworm-slim
    - name: rex-2
      workspace: /tmp/rex-2
      image: openclaw-sandbox-common:bookworm-slim
    # ... 最多 100 个并发 Rex 实例
```

### 7. 智能体身份和行为文件

每个智能体工作空间包含：
- `IDENTITY.md` — 名称、角色、表情符号、氛围
- `SOUL.md` — 行为规则、操作风格
- `AGENTS.md` — 操作合约（交接、安全、报告）

共享团队协议：
- `TEAM_PROTOCOL.md` — 无垃圾规则、可交付格式
- `TEAM.md` — 名册、所有权矩阵、升级路径
- `GLOSSARY.md` — 共享术语

## 归档材料

### 会话工具参考

**编排的关键会话工具：**

- `sessions_list` — 列出跨智能体的所有活动会话
- `sessions_history` — 从任何智能体会话获取记录
- `sessions_send` — 支持回复的跨智能体消息传递
- `sessions_spawn` — 在并行通道中启动子智能体

**子智能体行为：**
- 在具有唯一会话密钥的隔离会话中运行
- 完成时自动公告结果
- 无法生成另一个子智能体（深度=1 强制执行）
- 通过 `agent.subagents.maxConcurrent` 控制并发

### 沙箱配置

**模式（何时沙箱）：**
- `off` — 无沙箱（主机执行）
- `non-main` — 仅对非主会话沙箱（安全默认值）
- `all` — 每个会话在沙箱中运行

**作用域（多少容器）：**
- `session` — 每个会话一个容器
- `agent` — 每个智能体一个容器（跨会话共享）
- `shared` — 所有沙箱会话一个容器

**工作空间访问（沙箱看到什么）：**
- `none` — 工具仅看到沙箱工作空间
- `ro` — 在 `/agent` 只读挂载智能体工作空间
- `rw` — 在 `/workspace` 读写挂载智能体工作空间

**安全默认值：**
- 网络默认关闭（通过 `sandbox.docker.network` 覆盖）
- 工具允许/拒绝策略在沙箱规则之前应用
- `tools.elevated` 在主机上运行（打破玻璃逃生口）
- 危险路径的绑定挂载被阻止（`docker.sock`、`/etc`、`/proc`）

### 多智能体路由

**通道绑定将源映射到智能体：**
```yaml
bindings:
  - agentId: kev
    match:
      channel: whatsapp
  - agentId: rex
    match:
      channel: slack
      channelId: engineering
```

**路由优先级：**
1. 特定 `channel + accountId` 首先匹配
2. 通配符 `channel` 其次匹配
3. 回退到默认智能体

### 性能指标

**生产使用中的测量性能：**
- 人类时间：15 秒（发送初始消息）
- 智能体时间：3 分钟（并行专家执行）
- 并发：100 个隔离环境中的 Rex 实例
- 成本节约：使用 Flash 进行总结比 Opus 节省 10 倍

**模型选择策略：**
- OpenAI Codex (GPT-5.2) — 代码准确性 > 速度
- Claude Opus 4.5 — 长上下文状态的最佳编排器
- Gemini 3 Pro — 前端和视觉设计
- Gemini 3 Flash — 研究的速度 + 海量上下文

## 相关链接
- [Kev's Dream Team - 完整架构指南](https://github.com/adam91holt/orchestrated-ai-articles/blob/main/KEVS_DREAM_TEAM.md) — 包含 14+ 智能体的完整系统架构
- [OpenClaw 会话工具](https://docs.openclaw.ai/concepts/session-tool) — sessions_list/sessions_history/sessions_send/sessions_spawn 参考
- [OpenClaw 沙箱](https://docs.openclaw.ai/gateway/sandboxing) — Docker 沙箱模式/作用域/workspaceAccess 配置
- [OpenClaw 多智能体路由](https://docs.openclaw.ai/concepts/multi-agent-routing) — 通道绑定和智能体选择
- [Clawdbot 文档](https://docs.clawd.bot) — 本地优先 AI 编排的产品文档

## 常见问题

### 沙箱中的会话作用域和智能体作用域有什么区别？

**会话作用域**（`scope: session`）为每个智能体会话创建一个 Docker 容器——每个对话获得隔离的工作空间和进程空间。**智能体作用域**（`scope: agent`）在该智能体的所有会话之间共享一个容器——更便宜但会话共享文件系统状态。**共享作用域**（`scope: shared`）对所有沙箱智能体全局使用一个容器——最大共享但智能体之间零隔离。

### 子智能体如何不阻塞编排者而报告回来？

通过 `sessions_spawn` 生成的子智能体在并行通道中运行，并在完成时**自动公告结果**。编排器不轮询——网关聚合回复并将其作为消息传递。这支持扇出工作流（Kev 生成 Rex、Hawk、Scout；三者都在完成时报告）。

### 子智能体可以生成其他子智能体吗？

**不可以。** 子智能体无法生成另一个子智能体（深度=1 强制执行）。这防止不受控制的智能体链。只有编排者（Kev）可以生成专家。如果需要更深层次的委托，配置编排者直接生成正确的智能体。

### 到处运行 Opus 与模型选择有什么成本差异？

巨大。基于生产使用：在 Flash（$0.02）vs Opus（$0.30）上运行总结是 **15 倍更便宜**。在 Codex vs 通用模型上运行代码重构减少了估计 40% 的错误返工。该架构实现了**智能套利**——仅在关键之处支付高级推理（编排、安全审计），对常规任务使用更便宜/更快的模型（总结、基本研究）。

### 如何防止智能体发送状态更新垃圾信息？

在 `TEAM_PROTOCOL.md` 中配置严格的可交付规则：
- 仅 `DELIVERABLE:` 或 `BLOCKER:` 消息
- 仅在工作完成或被阻止时标记编排者
- 无状态垃圾信息

智能体每次会话都读取这些文件，因此交接保持一致，噪声保持低水平。以 GitHub 为中心的执行模型强化了这一点：可交付成果是 PR 链接或内联输出，而不是聊天垃圾信息。

### Docker 沙箱是完美的安全边界吗？

**不是。** OpenClaw 文档明确说明这是"不是完美的安全边界，但当模型做蠢事时，它实质性地限制了文件系统和进程访问。" 沙箱逃脱仍然可能（Docker 漏洞、内核漏洞）。对于敏感工作负载，结合使用：
- 工具允许/拒绝策略（对不受信任的智能体完全拒绝 exec）
- 只读工作空间访问（`workspaceAccess: ro`）
- 针对真正不受信任工作负载的独立物理或 VM 隔离
- `tools.elevated` 打破玻璃仅用于授权发件人

### 心跳和 webhook 有什么区别？

**心跳**是在固定节拍主动轮询的计划智能体轮次（`agent.heartbeat.every: 5m`）。适用于：收件箱监控、常规检查、提醒。**Webhook** 是事件驱动的——外部系统推送到 `/hooks/*` 端点以触发立即智能体运行。适用于：警报、CRM 更新、监控系统集成。对基于轮询的工作使用心跳；对事件驱动的工作使用 webhook。

### 我可以并行运行 100 个 Rex 实例吗？

**可以。** Clawdspace 为智能体提供远程隔离沙箱。每个 Rex 实例获得自己的：
- 工作空间（仓库克隆或项目目录）
- Docker 容器（隔离进程空间）
- 工具和依赖项（预烘焙在镜像中）

编排者（Kev）通过带有 `maxConcurrent: 100` 的 `sessions_spawn` 生成它们。它们独立运行，然后通过 PR 或输出报告。这将"我的 AI 助手"转变为"可部署智能单元"——将预配置团队放入客户端基础设施，让它们在安全、沙箱集群中自主工作。

### 如果生成的智能体失败或超时会发生什么？

编排者通过相同的结果聚合通道接收错误消息。配置带有升级规则的 `TEAM_PROTOCOL.md`：如果 Rex 失败，Kev 可以生成后备智能体或通知人类。超时在网关级别控制——长时间运行的任务应使用异步模式（生成 → 稍后通过 `sessions_history` 轮询）。
