---
title: "OpenClaw n8n Stack: Self-Hosted AI Agents with Workflow Automation"
slug: openclaw-n8n-stack
summary: "Pre-configured Docker stack combining OpenClaw AI agents with n8n workflows for self-hosted automation, enabling AI-driven workflows with 400+ external service integrations."
whatItDoes: "Deploys a self-hosted AI automation platform by combining OpenClaw AI agents with n8n visual workflow builder via Docker Compose."
category: automation-integration
difficulty: intermediate
tags:
  - workflow-automation
  - docker-stack
  - ai-agents
  - self-hosted
  - openclaw
targetUser:
  - AI automation enthusiasts
  - Self-hosting engineers
  - Workflow designers
skillsUsed:
  - name: openclaw-n8n-stack
    href: https://github.com/caprihan/openclaw-n8n-stack
  - name: automation-workflows
    href: https://clawhub.ai/JK-0001/automation-workflows
updatedAt: "2026-03-18"
published: true
---

## What it does
- Deploys OpenClaw (Claude-powered AI agent gateway) and n8n (visual workflow automation) in a single Docker Compose stack
- Provides pre-configured communication between AI agents and workflow triggers via webhooks
- Includes 4 ready-to-use workflow templates for email triage, social media monitoring, and multi-LLM validation
- Enables AI agents to trigger n8n workflows, call external services, and process data automatically

## Skills You Need
- [openclaw-n8n-stack](https://github.com/caprihan/openclaw-n8n-stack) - Pre-configured Docker stack combining OpenClaw AI agents with n8n workflows
- [automation-workflows](https://clawhub.ai/JK-0001/automation-workflows) - Design and implement automation workflows across n8n and other platforms

## Pain Point
Building an AI automation platform from scratch typically involves:

- Manually configuring AI agents with multiple service integrations
- Setting up webhook infrastructure to connect AI reasoning with workflow triggers
- Managing separate deployment pipelines for AI components and automation tools
- Lack of pre-built workflow templates for common use cases

This stack addresses the integration complexity by providing a pre-configured environment where OpenClaw and n8n work together out of the box.

## Core value of this case
OpenClaw n8n Stack provides a fast path to self-hosted AI automation by combining reasoning capabilities with visual workflows. For developers and automation enthusiasts, the direct value includes:

- Skip manual configuration of OpenClaw-n8n integration (webhooks, networking, volumes)
- Get started with 4 production-ready workflow templates immediately
- Deploy a complete AI automation platform in under 10 minutes
- Maintain full control over data and API keys (self-hosted)

## Typical scenarios
- Email triage: AI agent reads and summarizes emails, triggers Slack notifications via n8n workflows
- Content pipeline: Research → write → fact-check → publish, orchestrated by AI and workflows
- Social media monitoring: Track mentions and trends, generate AI-powered responses automatically
- Automated reporting: Generate reports using natural language queries with data processing
- Multi-model AI validation: Use Claude, ChatGPT, and Gemini together for cross-model fact-checking

## How to setup

### Prerequisites
- Docker and Docker Compose installed
- Anthropic API key (for Claude)
- Optional: OpenAI and/or Google AI keys for multi-model workflows

### Installation Steps

```bash
git clone https://github.com/caprihan/openclaw-n8n-stack.git
cd openclaw-n8n-stack
cp .env.template .env
nano .env
docker-compose up -d
```

### Access Points

| Service | URL | Default Credentials |
|---------|-----|---------------------|
| n8n | http://localhost:5678 | admin / (your password) |
| OpenClaw | http://localhost:3456 | — |

### Import Workflow Templates

1. Open n8n at http://localhost:5678
2. Go to Workflows → Import from File
3. Import any workflow from the workflows/ directory
4. Configure credentials and activate

### Configuration

- Edit config/openclaw.json to customize default model, thinking level, skills, and channel configurations
- Set up credentials in n8n UI (Credentials → Add Credential)
- Update N8N_WEBHOOK_URL in .env for production deployments with public URLs

### Example: Call n8n from OpenClaw

```bash
curl -X POST "http://n8n:5678/webhook/my-workflow" \
  -H "Content-Type: application/json" \
  -d '{"data": "from openclaw"}'
```

The N8N_WEBHOOK_BASE environment variable is pre-configured so OpenClaw knows where to find n8n.

### Maintenance

```bash
docker-compose pull
docker-compose up -d
docker run --rm -v openclaw-n8n-stack_openclaw-data:/data -v $(pwd):/backup alpine tar czf /backup/openclaw-backup.tar.gz -C /data .
docker run --rm -v openclaw-n8n-stack_n8n-data:/data -v $(pwd):/backup alpine tar czf /backup/n8n-backup.tar.gz -C /data .
```

### Production Security Checklist

- Use strong passwords for n8n
- Put behind a reverse proxy with HTTPS
- Don't expose ports directly to the internet
- Keep API keys secure (never commit .env)
- Review n8n's security best practices

### Troubleshooting

- Ensure both containers are on the same network
- Check docker-compose logs openclaw for errors
- Verify API keys are set correctly
- Ensure port 5678 is accessible for n8n webhooks
- Check Docker volumes: docker system df
- Prune unused: docker system prune -a

## Archived Materials

### Workflow Templates
The workflows/ directory includes 4 ready-to-use templates:

- ripr-chatgpt-validator.json - Multi-LLM fact-checking (ChatGPT)
- ripr-gemini-validator.json - Multi-LLM fact-checking (Gemini)
- email-triage.json - AI-powered email summarization
- social-monitor.json - Track mentions and trends

### Architecture Diagram

```
┌─────────────────────────────────────────────────────────────┐
│                     Docker Network                           │
│                                                              │
│  ┌─────────────────┐         ┌─────────────────┐           │
│  │   OpenClaw      │◄───────►│      n8n        │           │
│  │   (AI Agent)    │ webhook │  (Workflows)    │           │
│  │   Port 3456     │         │   Port 5678     │           │
│  └────────┬────────┘         └────────┬────────┘           │
│           │                           │                      │
│           ▼                           ▼                      │
│  ┌──────────────┐          ┌──────────────┐                  │
│  │  workspace/  │          │  workflows/   │                  │
│  │ (your files) │          │ (n8n exports)│                  │
│  └──────────────┘          └──────────────┘                  │
│                                                              │
└─────────────────────────────────────────────────────────────┘
           │                           │
           ▼                           ▼
     Anthropic API              External Services
     OpenAI API                  (Slack, Gmail, etc.)
     Google AI API
```

## Related Links
- [OpenClaw n8n Stack](https://github.com/caprihan/openclaw-n8n-stack) — Pre-configured Docker deployment stack
- [OpenClaw](https://github.com/openclaw/openclaw) — AI agent framework
- [n8n](https://n8n.io) — Workflow automation platform
- [n8n Security Best Practices](https://docs.n8n.io/hosting/security/) — Production deployment security guide

## FAQ
### Do I need both Anthropic and OpenAI API keys?
No. Anthropic API key is required (for Claude). OpenAI and Google AI keys are optional, only needed if you want to use multi-model workflows.

### Can I run this on a remote server?
Yes. For remote deployment, update N8N_WEBHOOK_URL in .env to your public domain or IP address so OpenClaw can reach n8n webhooks. Consider using a reverse proxy with HTTPS for security.

### How do I add my own workflows?
Create workflows in n8n's visual editor, then export them to the workflows/ directory. You can also import existing n8n workflows and connect them to OpenClaw via webhooks.

### Is this suitable for production use?
The stack provides a solid foundation, but for production you should implement additional security measures: reverse proxy with HTTPS, strong passwords, firewall rules, and regular backups. Review n8n's security documentation for best practices.

### Can I customize OpenClaw's behavior?
Yes. Edit config/openclaw.json to configure default model, thinking level, enabled skills/tools, and channel configurations. This allows you to tailor the AI agent to your specific use cases.

### What resources does this stack require?
Minimum requirements depend on your workflow complexity. For basic use cases, 2GB RAM and 2 CPU cores should be sufficient. For heavier AI processing or multiple concurrent workflows, consider 4GB+ RAM and dedicated resources.
