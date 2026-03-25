---
title: OpenClaw AI营养分析：用 Haver 把食物照片变成营养记录
slug: food-photo-nutrition-logging
summary: 该案例通过 openclaw-nutrition 与 Haver 服务，让用户通过聊天或餐食照片自动记录热量、宏量营养与体重数据，而不必手动维护饮食日志。
whatItDoes: 通过 openclaw-nutrition 技能调用 Haver 后端，接收餐食文字或图片输入并自动写入每日营养记录。
category: automation-integration
difficulty: intermediate
tags:
  - 食物照片分析
  - 营养追踪
  - 饮食记录
  - 热量记录
  - 健康教练
targetUser:
  - 营养教练
  - 健康管理用户
  - 健康产品团队
skillsUsed:
  - name: openclaw-nutrition
    href: https://clawhub.ai/Yuvasee/openclaw-nutrition
updatedAt: "2026-03-25"
published: true
---

## 这个案例做什么
`openclaw-nutrition` 通过 Haver 后端接收饮食文字描述或餐食照片，记录热量、蛋白质、碳水、脂肪等数据，并按日期归档为每日营养记录，同时支持体重追踪、营养摘要和 AI 教练式反馈。

## 所需技能
- [openclaw-nutrition](https://clawhub.ai/Yuvasee/openclaw-nutrition)

## 痛点
传统饮食记录工具的问题不是“算不出营养”，而是用户必须反复打开 App、检索食物、估算份量、维护日志。持续录入的操作成本，往往就是习惯中断的原因。

## 这个案例的核心价值
这个案例把“饮食记录”从独立 App 操作改成了 OpenClaw 里的自然对话。用户发一句话或一张照片即可完成记录、查看当天进度，并继续获取上下文相关的营养建议，比手工记账更容易持续使用。

## 典型应用场景
- 个人用户把餐食照片或一句话描述发送给 OpenClaw 代理，快速记录当天的热量和宏量营养。
- 营养教练为客户配置聊天式打卡入口，让用户先把饮食记录下来，再结合摘要做后续建议。
- 做健康产品验证的团队用该技能快速搭建“拍照记饮食 + AI 教练”原型，而不是先开发完整 App。

## 如何设置
1. 安装公开技能：`clawhub install Yuvasee/openclaw-nutrition`，或在 ClawHub 中安装 `openclaw-nutrition`。
2. 按技能文档注册 Haver 用户，调用 `POST /api/register` 获取以 `hv_` 开头的个人 API key。
3. 根据技能说明完成 onboarding，补齐时区、身高、体重、活动水平和目标等基础信息。
4. 开始记录饮食：文字输入走 `POST /api/me/nutrition/log`，图片输入也可以通过同一接口里的 `images` 字段提交。
5. 需要查看进度时，调用 `GET /api/me/nutrition/summary` 获取当天或指定时间段的营养汇总。
6. 也可以直接通过 Telegram 机器人 `@haver_sheli_bot` 使用同一套后端能力。

## 相关链接
- [Haver 官网](https://haver.dev/)
- [ClawHub：openclaw-nutrition](https://clawhub.ai/Yuvasee/openclaw-nutrition)
- [GitHub：Yuvasee/openclaw-nutrition](https://github.com/Yuvasee/openclaw-nutrition)
- [Telegram：@haver_sheli_bot](https://t.me/haver_sheli_bot)
- [OpenClaw Docs：技能安装与管理](https://docs.openclaw.ai/cli/skills)

## 常见问题

### 这个案例支持食物照片输入吗？
支持。Haver 官网提供 `Photo Recognition`，技能文档也说明 `POST /api/me/nutrition/log` 和 `POST /api/me/chat` 都可以接收 `images` 输入。

### 它会把数据自动记到 Google Sheets 或 n8n 吗？
没有 Google Sheets 或 n8n 的现成公开集成。饮食数据会自动写入 Haver 的营养追踪后端，并支持汇总与教练反馈。

### 这个案例的边界是什么？
它不是医疗营养建议工具，也不支持运动记录、饮水记录、条码扫描或删除已记录饮食，因此更适合日常营养追踪，而不是完整健康档案系统。
