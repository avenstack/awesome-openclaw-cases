---
title: "OpenClaw 自动化业务报表聚合：多源数据采集与定时分发"
slug: openclaw-automated-business-reports
summary: "部署 OpenClaw 代理聚合数据库、API 和分析平台数据，按计划生成结构化报表，并通过 Telegram、Discord 或邮件自动分发。"
whatItDoes: "自动化多源商业智能报表生成，定时分发到沟通渠道。"
category: operations
difficulty: intermediate
tags:
  - 报表自动化
  - 数据聚合
  - 定时任务
  - 商业智能
  - 多源集成
targetUser:
  - 业务运营经理
  - 数据分析师
  - 创业公司创始人
skillsUsed:
  - name: biz-reporter
    href: https://github.com/chainstack/awesome-openclaw-skills/tree/main/skills/biz-reporter
  - name: ga4-analytics
    href: https://github.com/chainstack/awesome-openclaw-skills/tree/main/skills/ga4-analytics
  - name: sql-agent
    href: https://github.com/chainstack/awesome-openclaw-skills/tree/main/skills/sql-agent
updatedAt: "2026-03-22"
published: true
---

## 这个案例做什么

**自动把数据库、API、分析平台的数据变成定时报表，推送到你的 Telegram/Discord/邮箱。**

不再需要手动登录各平台复制数据，LLM 自动识别异常和趋势，每天早上 8 点报表自动送达。

## 所需技能

- [biz-reporter](https://github.com/chainstack/awesome-openclaw-skills/tree/main/skills/biz-reporter) - 业务报表生成技能，支持多源数据采集
- [ga4-analytics](https://github.com/chainstack/awesome-openclaw-skills/tree/main/skills/ga4-analytics) - Google Analytics 4 数据提取和报表
- [sql-agent](https://github.com/chainstack/awesome-openclaw-skills/tree/main/skills/sql-agent) - 数据库查询和聚合能力

## 痛点

**周报花 4 小时，其中 3.5 小时在搬运数据。**

登录 GA4、Stripe、数据库复制数据到 Excel，漏一个平台重来。n8n/Zapier 需要画流程图，API 变更就得改。BI 仪表板要自己登录查看，忙起来就忘了。

## 这个案例的核心价值

**周报从 4 小时减到 15 分钟。**

代理自动采集所有数据源，LLM 发现异常（收入突降 20%）、趋势（某产品销量暴增）。数据源挂了自动重试，添加新平台改两行提示词就行。

真实用户：代理商从 10 个客户扩展到 25 个，没招人。

## 典型应用场景

### 每日业务简报

**需求**：高管每天 8 点要看昨天的 DAU、收入、订单量，从 5 个系统汇总要 90 分钟。

**配置**：cron `0 8 * * *`，采集 PG/GA4/Stripe/SendGrid，生成指标表 + 异常标注，推送到 Slack。

**结果**：早上 8 点简报自动到达，团队喝咖啡时扫一眼就行。

### 每周营销报表

**需求**：周五下午统计 Google Ads、Facebook Ads、GA4 的投放效果，找出表现好坏的 campaign。

**配置**：cron `0 17 * * Fri`，拉取 3 个平台数据，按 ROAS 排序，优化建议邮件至 marketing-team。

**结果**：营销团队每周省 4 小时，专注优化广告策略。

### 多客户代理商报表

**需求**：服务 20+ 客户，每个需要定制周报（不同 KPI 权重），客户经理 60% 时间在做报表。

**配置**：cron `0 9 * * Mon`，遍历 `config/clients.yaml`，应用各客户 KPI 配置，分别邮件发送。

**结果**：从 10 个客户扩展到 25 个，无需额外招人。

### 电商库存告警

**需求**：每天早上检查哪些产品库存 < 10，哪些销量突然暴增。

**配置**：cron `0 7 * * *`，查询数据库，缺货的 @inventory-team，爆款的发到运营群。

**结果**：运营团队在缺货影响收入前就知道了。

## 如何设置

### 1. 在云基础设施上部署 OpenClaw

OpenClaw 可在任何 VPS 或云实例运行。腾讯云轻量应用服务器提供预配置镜像：

```bash
# 在腾讯云轻量应用服务器
# 选择：OpenClaw 镜像（Ubuntu 22.04 + OpenClaw 预装）
# 最低规格：2 vCPU, 4GB RAM
```

或手动部署：

```bash
curl -fsSL https://get.openclaw.ai/install.sh | bash
openclaw init
```

### 2. 配置数据源连接

```yaml
# config/channels.yaml
channels:
  - type: postgresql
    host: db.example.com
    database: analytics
    username: ${DB_USER}
    password: ${DB_PASSWORD}

  - type: rest_api
    base_url: https://api.stripe.com/v1
    auth:
      type: bearer
      token: ${STRIPE_API_KEY}

  - type: google_analytics
    property_id: ${GA4_PROPERTY_ID}
    credentials_json: /path/to/service-account.json
```

### 3. 安装报表技能

```bash
clawhub install biz-reporter
clawhub install ga4-analytics
clawhub install sql-agent
```

### 4. 定义定时报表工作流

```yaml
# config/crons/daily-briefing.yaml
workflows:
  - name: daily-metrics-briefing
    schedule: "0 8 * * *"
    prompt_file: prompts/daily-briefing.md
    output:
      - type: discord_webhook
        url: ${DISCORD_WEBHOOK_URL}
      - type: email
        to: ops-team@example.com
```

### 5. 创建报表生成提示词

```markdown
# prompts/daily-briefing.md

使用以下数据源生成每日业务指标简报：

**数据库查询：**
- SELECT COUNT(DISTINCT user_id) as dau, SUM(revenue) as revenue FROM events WHERE date = yesterday
- SELECT COUNT(*) as new_signups FROM users WHERE created_at = yesterday

**GA4 API：**
- 获取昨天的 sessions、active_users、bounce_rate
- 与上周同日比较

**Stripe API：**
- 检索昨天的charges、refunds、net revenue
- 从活跃订阅计算 MRR

**输出格式：**
1. 高管摘要（2-3 句话）
2. 指标表：Metric | Yesterday | WoW Change |
3. 显著异常：任何 >20% 变化的指标
4. 流量来源前 5
5. 一个洞察或建议
```

### 6. 启用并启动

```bash
openclaw cron enable daily-metrics-briefing
openclaw cron list
openclaw logs follow --workflow daily-metrics-briefing
```

## 归档材料

### 数据库查询技能示例

```yaml
# skills/sql-agent/config.yaml
name: sql-agent
description: 对 PostgreSQL/MySQL 数据库执行 SQL 查询

parameters:
  connection_string: ${DATABASE_URL}
  timeout_seconds: 30
  max_rows: 10000

actions:
  - name: execute_query
    description: 运行 SELECT 查询并返回结果
    inputs:
      query: SQL SELECT 语句
    outputs:
      rows: 结果对象数组
      columns: 列名和类型
      execution_time: 查询持续时间（秒）

safety:
  read_only: true  # 阻止 INSERT/UPDATE/DELETE
  max_execution_time: 60
  allowed_tables: [analytics_events, users, orders]
```

### 成本控制配置

```yaml
# config/cost-controls.yaml
limits:
  max_api_calls_per_day: 1000
  max_llm_tokens_per_report: 8000
  max_execution_time_minutes: 10

alerts:
  daily_spend_threshold: 5.00  # USD
  alert_webhook: ${COST_ALERT_WEBHOOK}
```

## 相关链接

- [AgentMail: AI Daily Briefings](https://agentmail.ai/blog/daily-briefings) - AI 生成每日简报的业务用例
- [腾讯云：数据可视化与报表创建](https://cloud.tencent.com/developer/article/2466440) - 5 阶段工作流：Trigger、Collect、Decide、Act、Observe
- [腾讯云：n8n 多源聚合](https://cloud.tencent.com/developer/article/2468574) - 集成多个数据源用于自动化报表
- [awesome-openclaw-skills: biz-reporter](https://github.com/chainstack/awesome-openclaw-skills/tree/main/skills/biz-reporter) - Business Reporter 技能源代码
- [Sparkco.ai: Cron Job Scheduling](https://sparkco.ai/blog/openclaw-cron-jobs) - 使用 cron 调度自动化工作流

## 常见问题

### API 密钥放哪？安全吗？

存环境变量，别进 git。支持 Bearer Token、OAuth2（自动刷新）、Service Account。用只读账户，最小权限。

### 数据源挂了怎么办？

自动重试 3 次（指数退避），可用缓存数据加警告标记。

### 老板要不同格式的报表？

```yaml
prompt: |
  ${recipient_role} == "executive": 一页 3 个指标
  ${recipient_role} == "analyst": 完整数据表
```

### 要花多少钱？

**$15/月**：VPS $5 + LLM API $10（每日报表 30 次，8k tokens/次，Claude Haiku）。报表越频繁、分析越深越贵。

### 能同时发多个地方吗？

能。一个工作流配置多个 output：Discord + 邮件 + Slack，各自独立格式。

### 怎么测试？

```bash
openclaw workflow run daily-briefing --dry-run
openclaw workflow run daily-briefing  # 立即执行
```
用 `--context '{"date": "2026-03-15"}'` 测试特定日期。
