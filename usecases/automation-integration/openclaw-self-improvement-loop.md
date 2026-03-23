---
title: "OpenClaw Self-Improvement Loop: Turn Errors and Corrections into Reusable Workflow Memory"
slug: openclaw-self-improvement-loop
summary: "This case uses the self-improving-agent skill to log failures, corrections, and feature gaps, then promotes recurring patterns into OpenClaw workspace files for cross-session improvement."
whatItDoes: "Captures agent mistakes, user corrections, and missing capabilities in structured logs, then promotes recurring patterns into reusable OpenClaw workspace memory."
category: automation-integration
difficulty: intermediate
tags:
  - continuous-improvement
  - error-learning
  - workflow-memory
  - prompt-governance
  - session-handoff
targetUser:
  - Agent builders
  - Platform engineers
  - Automation engineers
skillsUsed:
  - name: self-improving-agent
    href: https://clawhub.ai/pskoett/self-improving-agent
updatedAt: "2026-03-23"
published: true
---

## What it does
- Logs command failures, user corrections, knowledge gaps, and missing features into `.learnings/ERRORS.md`, `.learnings/LEARNINGS.md`, and `.learnings/FEATURE_REQUESTS.md`.
- Promotes recurring lessons into `AGENTS.md`, `TOOLS.md`, or `SOUL.md` so OpenClaw injects them into future sessions automatically.
- Uses OpenClaw session tools to share learnings across active sessions instead of trapping them inside one chat.
- Keeps project-specific learnings lightweight while turning stable patterns into reusable team rules or new skills.

## Skills You Need
- [self-improving-agent](https://clawhub.ai/pskoett/self-improving-agent)

## Pain Point
Without a structured feedback loop, OpenClaw sessions repeat avoidable mistakes. Corrections stay buried in chat history, tool failures are rediscovered by trial and error, and team conventions drift because nothing promotes one-off fixes into durable workspace rules.

## Core value of this case
This case turns scattered feedback into operating memory. The agent stops treating corrections as disposable conversation and starts routing them into the right layer: unresolved items stay in `.learnings/`, reusable workflow rules move to `AGENTS.md`, tool gotchas move to `TOOLS.md`, and behavioral guidance moves to `SOUL.md`.

That gives teams three practical gains:
- Fewer repeated failures on the same commands, APIs, or output formats.
- Faster session recovery because stable rules are injected at bootstrap instead of re-explained manually.
- Cleaner governance for multi-agent work, because handoff lessons become shared protocol instead of private memory.

## Typical scenarios
- A coding agent keeps formatting commit messages the wrong way. The correction is logged once, then promoted to `SOUL.md` so later sessions follow the same style by default.
- A recurring tool failure needs the same workaround every week. The failure goes into `ERRORS.md`, the verified fix moves into `TOOLS.md`, and future sessions avoid the same dead end.
- A multi-agent team loses context during handoff. The delegation mistake is promoted to `AGENTS.md`, so later spawned sessions inherit the same reporting contract.
- Repeated feature requests reveal a stable workflow pattern. Instead of leaving it as notes, the team extracts it into a reusable skill scaffold.

## How to setup
1. Install the skill:

```bash
clawdhub install self-improving-agent
```

Or install manually:

```bash
git clone https://github.com/peterskoett/self-improving-agent.git ~/.openclaw/skills/self-improving-agent
```

2. Create the learning directory in the OpenClaw workspace:

```bash
mkdir -p ~/.openclaw/workspace/.learnings
```

3. Add the three log files, either by copying the skill templates or creating them yourself:
   - `LEARNINGS.md` for corrections, knowledge gaps, and best practices
   - `ERRORS.md` for command failures and exceptions
   - `FEATURE_REQUESTS.md` for missing capabilities users ask for

4. Define promotion rules in workspace memory:
   - `AGENTS.md` for workflow and delegation improvements
   - `TOOLS.md` for tool-specific gotchas and verified fixes
   - `SOUL.md` for behavioral preferences and communication rules

5. If you want reminders at session start, install the optional hook:

```bash
cp -r hooks/openclaw ~/.openclaw/hooks/self-improvement
openclaw hooks enable self-improvement
```

6. Verify the setup:

```bash
openclaw hooks list
openclaw status
```

## Archived Materials
The minimal file layout matters because it separates raw learnings from promoted rules:

```text
~/.openclaw/
├── workspace/
│   ├── AGENTS.md
│   ├── SOUL.md
│   ├── TOOLS.md
│   └── .learnings/
│       ├── LEARNINGS.md
│       ├── ERRORS.md
│       └── FEATURE_REQUESTS.md
```

Promotion targets from the source:
- Workflow improvements -> `AGENTS.md`
- Tool gotchas -> `TOOLS.md`
- Behavioral patterns -> `SOUL.md`
- Repeated patterns -> extract into a reusable skill with `scripts/extract-skill.sh`

## Related Links
- [ClawHub: self-improving-agent](https://clawhub.ai/pskoett/self-improving-agent)
- [OpenClaw Skills Repo: self-improving-agent](https://github.com/openclaw/skills/tree/main/skills/pskoett/self-improving-agent)
- [OpenClaw integration reference](https://github.com/openclaw/skills/blob/main/skills/pskoett/self-improving-agent/references/openclaw-integration.md)
- [Aliyun guide: OpenClaw deployment with self-improving-agent](https://developer.aliyun.com/article/1714943)
- [CNBlogs guide recommending self-improving-agent as a starter skill](https://www.cnblogs.com/shanren/p/19685473)

## FAQ
### When should a learning stay in `.learnings/`?
Keep it there when the issue is project-specific, still unverified, or not useful outside the original task. Promote only rules that should shape future sessions.

### Is this the same as semantic memory search?
No. This case governs what gets logged and promoted. Memory search helps retrieve stored context, but it does not decide which corrections become durable operating rules.

### Do I need the hook for this to work?
No. The hook only adds automatic reminders. The core loop still works if you log entries manually and review them during normal OpenClaw work.

### When does it make sense to extract a new skill?
When the same fix or workflow pattern keeps recurring across tasks, repos, or teammates. At that point, the source repo's `extract-skill.sh` script is a better long-term container than another note in `.learnings/`.
