---
title: Agent Ruler for OpenClaw：用审批门与审计回执约束高风险工作流
slug: agent-ruler-approval-gates
summary: 该案例为 OpenClaw 运行过程增加确定性策略控制、审批门与审计回执，让本地智能体在保持执行力的同时显著降低误操作与越权风险。
whatItDoes: 将 OpenClaw 运行在 Agent Ruler 之后，对工作区操作做边界约束，并把高风险动作转为可审批、可审计的执行流程。
category: operations
difficulty: advanced
tags:
  - 审批门
  - 审计回执
  - 安全治理
  - Telegram桥接
  - prompt-injection防护
targetUser:
  - 平台工程师
  - SRE团队
  - 自托管运营者
skillsUsed:
  - name: Agent Ruler
    href: https://github.com/steadeepanda/agent-ruler
updatedAt: '2026-03-22'
published: true
---

## 这个案例做什么
- 在 OpenClaw 外层增加一个确定性的 reference monitor 与 confinement runner，而不是把安全判断交给模型自己决定。
- 把执行环境拆成 workspace、shared-zone、system-critical、secrets 等边界区域，减少误删和误写带来的损害。
- 对网络访问、文件导出或投递、提权、敏感写入等高风险动作增加审批门。
- 通过本地控制面板集中展示 approvals、receipts、policy 和 runtime 状态，并可选接入 Telegram 审批流。
- 让操作者在保持本地优先部署的前提下，不必全程盯着智能体，也能审阅关键动作。

## 所需技能
- [Agent Ruler](https://github.com/steadeepanda/agent-ruler)

## 痛点
OpenClaw 只有接触真实文件、工具和外部服务时才真正有价值，但这也会放大 prompt injection、工具误调用和长时间无人值守自动化带来的风险。没有额外治理层时，操作者往往只能在“限制太死不好用”和“放得太开不安全”之间二选一。

## 这个案例的核心价值
这个案例的价值不在于把 OpenClaw 变慢，而在于把“该快的动作”和“该审的动作”分开。普通工作区操作继续保持流畅；真正跨边界的高风险动作则被显式审批、记录和追踪。这样更适合把本地智能体工作流放到长期运行环境中。

## 典型应用场景
- 在个人工作站或家庭服务器上运行 OpenClaw，附近同时存在敏感目录、账号凭证和日常数据。
- 以 Telegram 作为主要交互入口，但希望高风险批准统一回到受控界面处理。
- 允许智能体先在工作区内准备文件，再在导出到真实目标位置前加入审批步骤。
- 同时运行多个本地智能体 runner，希望边界规则和审批模型保持一致。

## 如何设置
1. 准备 Linux 主机，安装 `bubblewrap`，并先在 Agent Ruler 之外把 OpenClaw 本体跑通。
2. 通过最新 release 安装 Agent Ruler，然后执行 `agent-ruler init` 创建其托管工作区。
3. 执行 `agent-ruler setup`，导入或配置 OpenClaw runner。
4. 使用 `agent-ruler run -- openclaw gateway` 让 OpenClaw 通过 Agent Ruler 启动。
5. 打开终端输出的本地控制面板地址；文档中的默认回退地址是 `http://127.0.0.1:4622`。
6. 默认保持 local-only 暴露，再按需要在 setup 中启用 Telegram 或 Tailscale 辅助远程访问。

## 相关链接
- [Agent Ruler（GitHub）](https://github.com/steadeepanda/agent-ruler)
- [Agent Ruler：about this project](https://github.com/steadeepanda/agent-ruler/blob/master/about-this-project.md)
- [Show HN：Deterministic security solution for AI agents – OpenClaw and 2 more](https://news.ycombinator.com/item?id=47466968)

## 常见问题
### 这能替代 OpenClaw 自带的 sandbox 吗？
不能。它是在 runner 外层增加治理与审计能力。项目本身也明确说明这是降低损害面，而不是绝对安全保证。

### 是不是每个动作都要人工审批？
不是。其设计是让普通 workspace 操作保持快速，而跨边界高风险动作才进入 `allow`、`deny` 或 `pending_approval` 流程。

### 一定要配 Telegram 吗？
不需要。官方说明里本地 control panel 才是 canonical operator surface，Telegram 只是可选桥接渠道。
