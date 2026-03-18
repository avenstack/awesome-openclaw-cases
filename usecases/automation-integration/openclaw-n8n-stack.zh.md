---
title: OpenClaw n8n Stack：自托管 AI 智能体与工作流自动化
slug: openclaw-n8n-stack
summary: 预配置的 Docker 栈，结合 OpenClaw AI 智能体与 n8n 工作流，支持自托管 AI 驱动的自动化，集成 400+ 外部服务。
whatItDoes: 通过 Docker Compose 部署自托管 AI 自动化平台，将 OpenClaw AI 智能体与 n8n 可视化工作流构建器结合。
category: automation-integration
difficulty: intermediate
tags:
  - 工作流自动化
  - docker栈
  - AI智能体
  - 自托管
  - OpenClaw
targetUser:
  - AI 自动化爱好者
  - 自托管工程师
  - 工作流设计师
skillsUsed:
  - name: openclaw-n8n-stack
    href: https://github.com/caprihan/openclaw-n8n-stack
  - name: automation-workflows
    href: https://clawhub.ai/JK-0001/automation-workflows
updatedAt: "2026-03-18"
published: true
---

## 这个案例做什么
- 通过 Docker Compose 在单个栈中部署 OpenClaw（Claude 驱动的 AI 智能体网关）和 n8n（可视化工作流自动化）
- 提供预配置的 AI 智能体与工作流触发器之间的 webhook 通信
- 包含 4 个即用型工作流模板，涵盖邮件分类、社交媒体监控和多 LLM 验证
- 支持 AI 智能体触发 n8n 工作流、调用外部服务并自动处理数据

## 所需技能
- [openclaw-n8n-stack](https://github.com/caprihan/openclaw-n8n-stack) - 预配置的 Docker 栈，结合 OpenClaw AI 智能体与 n8n 工作流
- [automation-workflows](https://clawhub.ai/JK-0001/automation-workflows) - 设计和实现跨 n8n 等平台的工作流自动化

## 痛点
从零搭建 AI 自动化平台通常面临以下挑战：

- 手动配置 AI 智能体与多个服务集成的复杂性
- 设置 webhook 基础设施以连接 AI 推理与工作流触发器
- 分别管理 AI 组件和自动化工具的部署流程
- 缺乏常见用例的预构建工作流模板

这个栈通过提供预配置环境解决了集成复杂性问题，OpenClaw 和 n8n 可以开箱即用。

## 这个案例的核心价值
OpenClaw n8n Stack 通过结合推理能力与可视化工作流，提供了自托管 AI 自动化的快速路径。对开发者和自动化爱好者来说，最直接的价值包括：

- 跳过 OpenClaw-n8n 集成的手动配置（webhook、网络、卷挂载）
- 立即获得 4 个生产就绪的工作流模板
- 在 10 分钟内部署完整的 AI 自动化平台
- 保持对数据和 API 密钥的完全控制（自托管）

## 典型应用场景
- 邮件分类：AI 智能体读取并总结邮件，通过 n8n 工作流触发 Slack 通知
- 内容流水线：研究 → 撰写 → 事实核查 → 发布，由 AI 和工作流编排
- 社交媒体监控：追踪提及和趋势，自动生成 AI 驱动的回复
- 自动化报告：使用自然语言查询生成报告，配合数据处理
- 多模型 AI 验证：结合 Claude、ChatGPT 和 Gemini 进行跨模型事实核查

## 如何设置

### 前置条件
- 已安装 Docker 和 Docker Compose
- Anthropic API 密钥（用于 Claude）
- 可选：OpenAI 和/或 Google AI 密钥（用于多模型工作流）

### 安装步骤

```bash
git clone https://github.com/caprihan/openclaw-n8n-stack.git
cd openclaw-n8n-stack
cp .env.template .env
nano .env
docker-compose up -d
```

### 访问地址

| 服务 | URL | 默认凭据 |
|------|-----|----------|
| n8n | http://localhost:5678 | admin / （你的密码） |
| OpenClaw | http://localhost:3456 | — |

### 导入工作流模板

1. 在 http://localhost:5678 打开 n8n
2. 进入 Workflows → Import from File
3. 从 workflows/ 目录导入任意工作流
4. 配置凭据并激活

### 配置说明

- 编辑 config/openclaw.json 自定义默认模型、思考级别、技能和通道配置
- 在 n8n UI 中设置凭据（Credentials → Add Credential）
- 对于部署到生产环境，在 .env 中更新 N8N_WEBHOOK_URL 为你的公网 URL

### 示例：从 OpenClaw 调用 n8n

```bash
curl -X POST "http://n8n:5678/webhook/my-workflow" \
  -H "Content-Type: application/json" \
  -d '{"data": "from openclaw"}'
```

N8N_WEBHOOK_BASE 环境变量已预配置，OpenClaw 知道如何找到 n8n。

### 维护操作

```bash
docker-compose pull
docker-compose up -d
docker run --rm -v openclaw-n8n-stack_openclaw-data:/data -v $(pwd):/backup alpine tar czf /backup/openclaw-backup.tar.gz -C /data .
docker run --rm -v openclaw-n8n-stack_n8n-data:/data -v $(pwd):/backup alpine tar czf /backup/n8n-backup.tar.gz -C /data .
```

### 生产安全检查清单

- 为 n8n 使用强密码
- 放置在带 HTTPS 的反向代理后面
- 不要将端口直接暴露到互联网
- 保护 API 密钥安全（不要提交 .env）
- 参考 n8n 的安全最佳实践

### 故障排查

- 确保两个容器在同一网络中
- 检查 docker-compose logs openclaw 查看错误
- 验证 API 密钥设置正确
- 确保端口 5678 可被 n8n webhooks 访问
- 检查 Docker 卷：docker system df
- 清理未使用资源：docker system prune -a

## 归档材料

### 工作流模板
workflows/ 目录包含 4 个即用型模板：

- ripr-chatgpt-validator.json - 多 LLM 事实核查（ChatGPT）
- ripr-gemini-validator.json - 多 LLM 事实核查（Gemini）
- email-triage.json - AI 驱动的邮件总结
- social-monitor.json - 追踪提及和趋势

### 架构图

```
┌─────────────────────────────────────────────────────────────┐
│                     Docker 网络                              │
│                                                              │
│  ┌─────────────────┐         ┌─────────────────┐           │
│  │   OpenClaw      │◄───────►│      n8n        │           │
│  │   (AI 智能体)   │ webhook │   (工作流)      │           │
│  │   端口 3456     │         │   端口 5678     │           │
│  └────────┬────────┘         └────────┬────────┘           │
│           │                           │                      │
│           ▼                           ▼                      │
│  ┌──────────────┐          ┌──────────────┐                  │
│  │  workspace/  │          │  workflows/   │                  │
│  │ (你的文件)   │          │ (n8n 导出)    │                  │
│  └──────────────┘          └──────────────┘                  │
│                                                              │
└─────────────────────────────────────────────────────────────┘
           │                           │
           ▼                           ▼
     Anthropic API              外部服务
     OpenAI API                  (Slack, Gmail 等)
     Google AI API
```

## 相关链接
- [OpenClaw n8n Stack](https://github.com/caprihan/openclaw-n8n-stack) — 预配置的 Docker 部署栈
- [OpenClaw](https://github.com/openclaw/openclaw) — AI 智能体框架
- [n8n](https://n8n.io) — 工作流自动化平台
- [n8n 安全最佳实践](https://docs.n8n.io/hosting/security/) — 生产环境部署安全指南

## 常见问题
### 我是否需要同时拥有 Anthropic 和 OpenAI API 密钥？
不需要。Anthropic API 密钥是必需的（用于 Claude）。OpenAI 和 Google API 密钥是可选的，仅在使用多模型工作流时需要。

### 我可以在远程服务器上运行这个吗？
可以。对于远程部署，在 .env 中更新 N8N_WEBHOOK_URL 为你的公网域名或 IP 地址，这样 OpenClaw 可以访问 n8n webhooks。出于安全考虑，建议使用带 HTTPS 的反向代理。

### 如何添加自己的工作流？
在 n8n 可视化编辑器中创建工作流，然后导出到 workflows/ 目录。你也可以导入现有的 n8n 工作流，并通过 webhook 将其连接到 OpenClaw。

### 这适合生产环境使用吗？
该栈提供了坚实的基础，但对于生产环境，你应该实施额外的安全措施：带 HTTPS 的反向代理、强密码、防火墙规则和定期备份。参考 n8n 的安全文档了解最佳实践。

### 我可以自定义 OpenClaw 的行为吗？
可以。编辑 config/openclaw.json 配置默认模型、思考级别、启用的技能/工具和通道配置。这允许你根据特定用例定制 AI 智能体。

### 这个栈需要什么资源？
最低资源需求取决于工作流的复杂度。对于基本用例，2GB RAM 和 2 CPU 核心应该足够。对于更繁重的 AI 处理或多个并发工作流，建议 4GB+ RAM 和专用资源。
