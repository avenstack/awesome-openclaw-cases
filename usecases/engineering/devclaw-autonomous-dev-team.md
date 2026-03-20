---
title: DevClaw: Turn OpenClaw into an Autonomous Multi-Project Development Team
slug: devclaw-autonomous-dev-team
summary: DevClaw plugin transforms OpenClaw into autonomous dev teams where each Telegram group operates as an isolated project with automated DEV→QA→review pipelines, reducing token usage by 60-80%.
whatItDoes: Converts Telegram groups into isolated development teams that autonomously execute GitHub/GitLab issues through role-based workers (Junior/Medior/Senior), session reuse, and token-free scheduling.
category: engineering
difficulty: intermediate
tags:
  - autonomous-development
  - multi-project-pipeline
  - github-integration
  - token-optimization
targetUser:
  - Solo developers
  - Small development teams
  - AI platform engineers
skillsUsed:
  - name: devclaw
    href: https://github.com/laurentenhoor/devclaw
updatedAt: '2026-03-20'
published: true
---

## What it does
- Each Telegram group becomes an autonomous dev team that ships code while you sleep
- Matches task complexity to model cost: cheap models for typos, powerful models for architecture—saves 60-80% on tokens
- Runs multiple projects in parallel with automatic issue→dev→review→merge pipelines

## Skills You Need
- [devclaw](https://github.com/laurentenhoor/devclaw) - OpenClaw plugin for development orchestration

## Pain Point
Agentic coding tools promise productivity but often require babysitting: checking if the agent picked the right model, transitioned labels correctly, maintained session references, or recovered from crashed workers. Developers spend more time managing the agent than doing the work themselves.

## Core value of this case
- **60-80% token savings**: Tier selection (Haiku for typos, Opus for architecture) + session reuse (40-60% per task) + token-free scheduling
- **True autonomy**: Workers self-report completion, heartbeat auto-merges approved PRs, failures loop back to DEV without human intervention
- **Multi-project parallelism**: Run multiple projects simultaneously with full isolation—separate queues, workers, sessions, and state per project
- **Audit trail**: Every code change links to a tracked issue via GitHub/GitLab, with full NDJSON audit.log
- **Right model for the job**: CSS typo gets Haiku (~$0.001), database migration gets Opus (~$0.20)

## Typical scenarios
- **Overnight shipping**: Create issues before bed, wake up to completed PRs across multiple projects
- **Multi-project maintenance**: Run independent dev teams for webapp, API, and mobile projects in parallel
- **Research tasks**: Architect workers investigate design questions ("how to migrate to OAuth2?") and post findings as issue comments
- **Bug fix loops**: QA fails → auto-dispatches DEV fix → re-test → auto-merge on pass

## How to setup
1. Install DevClaw: `openclaw plugins install @laurentenhoor/devclaw`
2. Start onboarding: `"Hey, can you help me set up DevClaw?"` in any OpenClaw channel
3. Configure model assignments (default: Junior→Haiku, Medior→Sonnet, Senior→Opus)
4. Register projects: link Telegram groups to GitHub/GitLab repositories
5. Create issues in your repo—the pipeline handles the rest

## Archived Materials

### Role to Model Mapping
DevClaw abstracts model selection behind developer roles:

| Role       | Level     | Tasks                          | Model    |
|------------|-----------|--------------------------------|----------|
| Developer  | Junior    | Typos, CSS fixes, renames      | Haiku    |
| Developer  | Medior    | Features, bug fixes            | Sonnet   |
| Developer  | Senior    | Architecture, migrations       | Opus     |
| Reviewer   | Junior    | Standard code review           | Sonnet   |
| Reviewer   | Senior    | Security review, edge cases    | Opus     |

### Pipeline State Machine
```
Planning → To Do → Doing → To Review → Done (auto-merge + close)
Planning → To Research → Researching → Planning (architect findings)
```

### Heartbeat Configuration Example
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

## Related Links
- [DevClaw GitHub](https://github.com/laurentenhoor/devclaw)
- [DevClaw Documentation](https://devclaw.dev/)
- [Show HN: Turn OpenClaw into a high performing development team](https://news.ycombinator.com/item?id=47010242)
- [Reddit: DevClaw v1.2.2 announcement](https://www.reddit.com/r/OpenClawDevs/comments/1r558vz/devclaw_v122_turns_openclaw_into_a_high/)

## FAQ
### Can I run multiple projects simultaneously?
Yes. Each project is fully isolated with its own queue, workers, sessions, and state. Projects run in parallel by default.

### What happens when a PR receives review feedback?
The heartbeat detects "changes requested" or merge conflicts, moves the label to "To Improve," and auto-dispatches the previous DEV level to fix it.

### Do I need to manage session references manually?
No. DevClaw creates and reuses persistent sessions per role per project. Workers accumulate codebase context across tasks automatically.

### Can I customize which model each role uses?
Yes. The role-to-model mapping is fully configurable in workspace and project-level settings.

### What if a worker crashes mid-task?
The heartbeat health pass detects workers stuck for >2 hours, reverts their labels back to queue, and deactivates them for retry.
