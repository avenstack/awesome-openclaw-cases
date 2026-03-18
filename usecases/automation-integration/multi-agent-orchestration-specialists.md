---
title: "OpenClaw Multi-Agent Orchestration: 14+ Specialist Agents with Parallel Execution"
slug: multi-agent-orchestration-specialists
summary: "Orchestrate 14+ specialist AI agents with OpenClaw's session tools, sandboxing, and routing to achieve 15-second human time for complex multi-step tasks."
whatItDoes: "Configures a multi-agent orchestration system with specialized agents, session-based delegation, sandboxed execution, and parallel task routing to automate complex workflows."
category: automation-integration
difficulty: advanced
tags:
  - multi-agent
  - orchestration
  - parallel-execution
  - sandboxing
  - agent-routing
targetUser:
  - Platform engineers building AI teams
  - DevOps teams automating workflows
  - AI orchestration system architects
skillsUsed:
  - name: openclaw-multi-agent
    href: https://docs.openclaw.ai/concepts/multi-agent-routing
  - name: session-tools
    href: https://docs.openclaw.ai/concepts/session-tool
updatedAt: "2026-03-18"
published: true
---

## What it does
- Orchestrates 14+ specialized AI agents (Kev the orchestrator + specialists like Rex, Hawk, Scout, Dash, Dot, Pixel)
- Uses session tools (`sessions_spawn`, `sessions_send`, `sessions_list`) for parallel agent delegation and result aggregation
- Configures per-agent sandboxing with Docker isolation, mode controls (off/non-main/all), and workspace access policies
- Routes different channels (WhatsApp, Slack, Teams, webhooks) to specific agents via bindings
- Enables parallel execution in isolated environments (Clawdspace) for concurrent task processing
- Implements proactive automation via heartbeats and webhook-triggered incident response
- Achieves 15 seconds human time / 3 minutes agent time for complex multi-step workflows

## Skills You Need
- [openclaw-multi-agent](https://docs.openclaw.ai/concepts/multi-agent-routing) - Multi-agent routing and channel bindings
- [session-tools](https://docs.openclaw.ai/concepts/session-tool) - Session management, spawning, and cross-agent messaging
- [sandboxing](https://docs.openclaw.ai/gateway/sandboxing) - Docker sandbox configuration, mode/scope/workspaceAccess

## Pain Point
Building reliable multi-agent systems faces fundamental challenges:

- **Coordination chaos**: Without clear protocols, agents spam status updates, duplicate work, and drop handoffs
- **Security risks**: Giving full system access to multiple agents creates uncontrolled blast radius for model errors
- **Performance bottlenecks**: Sequential agent execution wastes time when tasks could run in parallel
- **Routing complexity**: Managing different channels (Slack, WhatsApp, webhooks) to appropriate agents becomes ad-hoc
- **State isolation**: Without proper session management, agent contexts bleed into each other
- **Cost inefficiency**: Running premium models on routine tasks burns budget without value

This case demonstrates how OpenClaw's session tools, sandboxing, and routing primitives transform chaotic multi-agent setups into reliable workflows with measured performance (15s human / 3min agent time).

## Core value of this case
Multi-agent orchestration with OpenClaw provides:

- **Measured productivity**: 15 seconds human effort achieves what takes 3 minutes of automated agent work across 7+ specialists
- **Specialization economics**: Assign Flash to summarization ($0.02), Codex to refactoring ($0.10), Opus to orchestration ($0.30)—pay premium reasoning only where it moves the needle
- **Blast radius control**: Run Rex inside Docker sandbox (`mode: all`) while Kev operates on host—Rex can't escape even if prompted maliciously
- **Parallel throughput**: Spin up 100 concurrent Rex instances via Clawdspace, each tackling separate tickets in isolated environments
- **Reliable delegation**: `sessions_spawn` with automatic result aggregation prevents dropped handoffs—sub-agents announce back when complete
- **Always-on automation**: Heartbeats poll proactively at fixed cadence; hooks inject work the moment external systems fire

## Typical scenarios
- **GitHub-driven development**: Kev triages issues, spawns Rex for implementation, delegates to Hawk for security review, reports back with PR link
- **Incident response workflow**: Monitoring webhook → trigger agent investigation → AWS CLI + log analysis → WhatsApp escalation if action needed
- **Research pipelines**: Scout ingests entire API documentation sets via Flash's massive context, distills to summaries for smarter agents to synthesize
- **Parallel code reviews**: Spin up N Hawk instances, each reviewing different microservices, merge outputs via aggregated reports
- **Design-dev handoffs**: Pixel generates UI specs, Rex implements components, Hawk validates security—all orchestrated by Kev with minimal human oversight

## How to setup

### 1. Define agent roster with specializations

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
        mode: off  # Orchestrator needs full access
    - id: rex
      name: Rex
      model: openai-codex/gpt-5.2-codex
      sandbox:
        mode: all  # Isolate coding tasks
    - id: hawk
      name: Hawk
      model: anthropic/claude-opus-4-5
      tools:
        exec:
          allow: false  # Read-only for security reviews
    - id: scout
      name: Scout
      model: google-vertex/gemini-3-flash-preview  # Speed + massive context
```

### 2. Configure multi-agent routing

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

### 3. Enable session tools for delegation

```yaml
agents:
  list:
    - id: kev
      subagents:
        maxConcurrent: 10  # Control parallel spawns
        allowedTargetIds: [rex, hawk, scout, dash, dot, pixel]
```

### 4. Configure sandboxing per security profile

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
        workspaceAccess: ro  # Read-only for audits
```

### 5. Set up proactive automation

**Heartbeats for polling:**
```yaml
agents:
  list:
    - id: kev
      heartbeat:
        every: 5m
        prompt: |
          Check for new GitHub issues tagged 'priority:high'.
          If found, spawn Rex to implement and Hawk to review.
```

**Webhooks for event-driven triggers:**
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

### 6. Parallel execution with Clawdspace

```yaml
# Spin up N isolated environments for concurrent agents
clawdspace:
  environments:
    - name: rex-1
      workspace: /tmp/rex-1
      image: openclaw-sandbox-common:bookworm-slim
    - name: rex-2
      workspace: /tmp/rex-2
      image: openclaw-sandbox-common:bookworm-slim
    # ... up to 100 concurrent Rex instances
```

### 7. Agent identity and behavior files

Each agent workspace contains:
- `IDENTITY.md` — name, role, emoji, vibe
- `SOUL.md` — behavioral rules, operating style
- `AGENTS.md` — operating contract (handoffs, safety, reporting)

Shared team protocols:
- `TEAM_PROTOCOL.md` — no-spam rules, deliverable formats
- `TEAM.md` — roster, ownership matrix, escalation paths
- `GLOSSARY.md` — shared terminology

## Archived Materials

### Session Tool Reference

**Key session tools for orchestration:**

- `sessions_list` — List all active sessions across agents
- `sessions_history` — Fetch transcripts from any agent session
- `sessions_send` — Cross-agent messaging with reply-back capability
- `sessions_spawn` — Launch sub-agents in parallel lanes

**Sub-agent behavior:**
- Run in isolated sessions with unique session keys
- Announce results back automatically when complete
- Cannot spawn another sub-agent (depth=1 enforcement)
- Concurrency controlled via `agent.subagents.maxConcurrent`

### Sandboxing Configuration

**Modes (when to sandbox):**
- `off` — No sandboxing (host execution)
- `non-main` — Sandbox only non-main sessions (default for safe defaults)
- `all` — Every session runs in sandbox

**Scope (how many containers):**
- `session` — One container per session
- `agent` — One container per agent (shared across sessions)
- `shared` — One container for all sandboxed sessions

**Workspace access (what sandbox sees):**
- `none` — Tools see only sandbox workspace
- `ro` — Mount agent workspace read-only at `/agent`
- `rw` — Mount agent workspace read/write at `/workspace`

**Security defaults:**
- Network off by default (override with `sandbox.docker.network`)
- Tool allow/deny policies apply before sandbox rules
- `tools.elevated` runs on host (break-glass escape hatch)
- Bind mounts blocked for dangerous paths (`docker.sock`, `/etc`, `/proc`)

### Multi-Agent Routing

**Channel bindings map sources to agents:**
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

**Routing precedence:**
1. Specific `channel + accountId` matches first
2. Wildcard `channel` matches second
3. Falls back to default agent

### Performance Metrics

**Measured performance from production usage:**
- Human time: 15 seconds (sending initial message)
- Agent time: 3 minutes (parallel specialist execution)
- Concurrency: 100 Rex instances in isolated environments
- Cost savings: 10x by using Flash for summaries vs Opus

**Model selection strategy:**
- OpenAI Codex (GPT-5.2) — Code accuracy > speed
- Claude Opus 4.5 — Best orchestrator for long-context state
- Gemini 3 Pro — Frontend and visual design
- Gemini 3 Flash — Speed + massive context for research

## Related Links
- [Kev's Dream Team - Full Architecture Guide](https://github.com/adam91holt/orchestrated-ai-articles/blob/main/KEVS_DREAM_TEAM.md) — Complete system architecture with 14+ agents
- [OpenClaw Session Tools](https://docs.openclaw.ai/concepts/session-tool) — sessions_list/sessions_history/sessions_send/sessions_spawn reference
- [OpenClaw Sandboxing](https://docs.openclaw.ai/gateway/sandboxing) — Docker sandbox mode/scope/workspaceAccess configuration
- [OpenClaw Multi-Agent Routing](https://docs.openclaw.ai/concepts/multi-agent-routing) — Channel bindings and agent selection
- [Clawdbot Documentation](https://docs.clawd.bot) — Product docs for local-first AI orchestration

## FAQ

### What's the difference between session scope and agent scope in sandboxing?

**Session scope** (`scope: session`) creates one Docker container per agent session—each conversation gets isolated workspace and process space. **Agent scope** (`scope: agent`) shares one container across all sessions for that agent—cheaper but sessions share filesystem state. **Shared scope** (`scope: shared`) uses one container for all sandboxed agents globally—maximum sharing but zero isolation between agents.

### How do sub-agents report back without blocking the orchestrator?

Sub-agents spawned via `sessions_spawn` run in parallel lanes and **automatically announce results** back when complete. The orchestrator doesn't poll—the gateway aggregates replies and delivers them as messages. This enables fan-out workflows (Kev spawns Rex, Hawk, Scout simultaneously; all three report back when done).

### Can sub-agents spawn other sub-agents?

**No.** Sub-agents cannot spawn another sub-agent (depth=1 enforcement). This prevents uncontrolled agent chains. Only the orchestrator (Kev) can spawn specialists. If you need deeper delegation, configure the orchestrator to spawn the right agent directly.

### What's the cost difference between running Opus everywhere vs model selection?

Massive. Based on production usage: running summaries on Flash ($0.02) vs Opus ($0.30) is **15x cheaper**. Running code refactoring on Codex vs general-purpose models reduces bug rework by estimated 40%. The architecture enables **intelligence arbitrage**—pay premium reasoning only where it moves the needle (orchestration, security audits), use cheaper/faster models for routine tasks (summarization, basic research).

### How do I prevent agents from spamming status updates?

Configure `TEAM_PROTOCOL.md` with strict deliverable rules:
- Only `DELIVERABLE:` or `BLOCKER:` messages
- Tag orchestrator only when work is done or blocked
- No status spam

Agents read these files every session, so handoffs stay consistent and noise stays low. The GitHub-centric execution model reinforces this: deliverables are PR links or inline output, not chat chatter.

### Is Docker sandboxing a perfect security boundary?

**No.** OpenClaw documentation explicitly states this is "not a perfect security boundary, but it materially limits filesystem and process access when the model does something dumb." Sandbox escape is still possible (Docker vulnerabilities, kernel exploits). For sensitive workloads, combine with:
- Tool allow/deny policies (deny exec entirely for untrusted agents)
- Read-only workspace access (`workspaceAccess: ro`)
- Separate physical or VM isolation for truly untrusted workloads
- `tools.elevated` break-glass only for authorized senders

### How do heartbeats differ from webhooks?

**Heartbeats** are scheduled agent turns that poll proactively at fixed cadence (`agent.heartbeat.every: 5m`). Good for: inbox monitoring, routine checks, reminders. **Webhooks** are event-driven—external systems push to `/hooks/*` endpoints to trigger immediate agent runs. Good for: alerts, CRM updates, monitoring system integration. Use heartbeats for polling-based work; use webhooks for event-driven work.

### Can I run 100 Rex instances in parallel?

**Yes.** Clawdspace provides remote, isolated sandboxes for agents. Each Rex instance gets its own:
- Workspace (repo clone or project directory)
- Docker container (isolated process space)
- Tools and dependencies (pre-baked in image)

Orchestrator (Kev) spawns them via `sessions_spawn` with `maxConcurrent: 100`. They run independently, then report back with PRs or outputs. This turns "My AI Assistant" into "Deployable Intelligence Units"—drop a pre-configured team into client infrastructure and let them work autonomously in secure, sandboxed clusters.

### What happens if a spawned agent fails or times out?

The orchestrator receives error messages via the same result aggregation channel. Configure `TEAM_PROTOCOL.md` with escalation rules: if Rex fails, Kev can spawn a fallback agent or notify human. Timeouts are controlled at the gateway level—long-running tasks should use async patterns (spawn → poll later via `sessions_history`).
