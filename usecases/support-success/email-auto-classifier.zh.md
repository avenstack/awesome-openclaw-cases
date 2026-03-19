---
title: OpenClaw 邮件自动分类：在收件箱过载前优先处理紧急消息
slug: email-auto-classifier
summary: 该案例将新邮件分类为紧急、常规与垃圾三类，并优先推送时效性消息，帮助用户在高邮件量下更快处理关键沟通。
whatItDoes: 通过规则化邮件分流与紧急提醒机制，实现收件箱的优先级路由与高优先消息优先处理。
category: support-success
difficulty: intermediate
tags:
  - 邮件分流
  - 紧急提醒
  - 收件箱自动化
  - 优先级路由
targetUser:
  - 工程团队负责人
  - 客服负责人
skillsUsed:
  - name: AgentMail Wrapper
    href: https://clawhub.ai/skills/agentmail-wrapper
updatedAt: '2026-03-12'
published: true
---

## 这个案例做什么
- 按固定频率检查新邮件。
- 用可解释规则将邮件分类为紧急、常规、垃圾。
- 对高优先邮件触发提醒，其余邮件进入低优先级路径。

## 所需技能
- [AgentMail Wrapper](https://clawhub.ai/skills/agentmail-wrapper)

## 痛点
邮件高峰时，真正重要的信息容易被资讯订阅和低价值通知淹没。纯人工分类不稳定，紧急沟通容易延迟处理。

## 这个案例的核心价值
该案例在人工阅读前增加“稳定分流层”，减少注意力切换，提升紧急消息响应速度，并在高邮件量场景下保持收件箱可控。

## 典型应用场景
- 每日早晨处理隔夜累积邮件。
- 对会议变更、截止时间提醒等消息要求快速升级的团队。
- 希望将资讯类邮件与待行动邮件分开的个人用户。

## 如何设置
1. 定义分类规则（关键词、发件人优先级、时限信号）。
2. 配置周期扫描（例如每 15 分钟）。
3. 将结果路由到对应文件夹，并对紧急匹配触发提醒。

## 相关链接
- [OpenClaw 文档：Gmail Pub/Sub](https://docs.openclaw.ai/automation/gmail-pubsub.md)

## 常见问题
### 这个案例只能用于 Gmail 吗？
不是。分流逻辑本身与邮箱服务商无关，Gmail 只是已有文档路径之一。

### 这个流程适合全自动吗？
边界场景不建议完全自动。应保持紧急规则可审阅，并定期复盘误报。

### 如何降低“误判为紧急”的提醒噪声？
先用严格规则（高可信发件人 + 强时效关键词）起步，再根据复盘结果逐步扩展。