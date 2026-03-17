---
title: 用 SuperCall 在 OpenClaw 中自动完成活动来宾电话确认
slug: event-guest-confirmation-supercall
summary: 通过 OpenClaw + SuperCall 自动拨打 RSVP 确认电话，收集出席结果与备注，并输出结构化汇总。
whatItDoes: 使用 SuperCall 批量执行来宾电话确认，采集出席状态与备注信息，最终生成活动出席汇总报告。
category: operations
difficulty: intermediate
tags:
  - 活动运营
  - RSVP自动化
  - 外呼电话
  - 出席追踪
targetUser:
  - 活动组织者
  - 运营团队
  - 个人助理
skillsUsed:
  - name: SuperCall
    href: https://clawhub.ai/xonder/supercall
updatedAt: '2026-03-11'
published: true
---

## 这个案例做什么
- 按预设来宾名单逐个电话确认是否出席。
- 采集饮食禁忌、携伴人数、到场时间等结构化备注。
- 输出已确认、已拒绝、未接听三类结果汇总。

## 所需技能
- [SuperCall](https://clawhub.ai/xonder/supercall)

## 痛点
当来宾人数上升后，人工电话跟进成本高且容易漏记。电话触达通常比纯文本更容易获得回复，但批量执行对组织者负担很重。

## 这个案例的核心价值
- 提升中大型名单的 RSVP 完成效率。
- 将出席状态和个性化需求集中沉淀到同一报告。
- 降低活动组织者在重复沟通上的时间消耗。

## 典型应用场景
- 婚礼、聚会、私宴等活动来宾确认。
- 团建、工作坊、线下会议出席核对。
- 活动前一周的集中提醒与二次确认。

## 如何设置
1. 按官方配置文档在 OpenClaw 中安装并配置 SuperCall。
2. 接通所需通话基础设施（Twilio 号码、OpenAI Realtime Key、Webhook 隧道）。
3. 准备包含姓名、电话和活动信息的来宾名单。
4. 让 OpenClaw 执行逐个电话确认并返回结构化 RSVP 汇总。

## 相关链接
- [SuperCall on ClawHub](https://clawhub.ai/xonder/supercall)
- [SuperCall on GitHub](https://github.com/xonder/supercall)

## 常见问题
### 为什么用 SuperCall 而不是通用语音工具？
来源案例强调 SuperCall 的通话人格隔离机制，更适合批量、标准化的确认任务。

### 对未接听来宾能处理吗？
可以。流程可记录未接听状态，并在汇总中标注，便于后续补拨。

### 小型活动也有必要使用吗？
有。可先用小批量验证话术，再扩展到完整名单。