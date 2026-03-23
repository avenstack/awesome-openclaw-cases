---
title: OpenClaw 自我改进闭环：把错误、纠正与经验沉淀为长期工作记忆
slug: openclaw-self-improvement-loop
summary: 该案例使用 self-improving-agent 技能记录失败、纠正和能力缺口，再把重复出现的模式提升到 OpenClaw 工作区文件中，形成跨会话持续改进闭环。
whatItDoes: 以结构化日志记录智能体错误、用户纠正和缺失能力，再把重复模式提升为 OpenClaw 可复用的工作区记忆。
category: automation-integration
difficulty: intermediate
tags:
  - 持续改进
  - 错误复盘
  - 工作流记忆
  - 提示词治理
  - 会话交接
targetUser:
  - 智能体开发者
  - 平台工程师
  - 自动化工程师
skillsUsed:
  - name: self-improving-agent
    href: https://clawhub.ai/pskoett/self-improving-agent
updatedAt: "2026-03-23"
published: true
---

## 这个案例做什么
- 把命令失败、用户纠正、知识缺口和缺失能力分别记录到 `.learnings/ERRORS.md`、`.learnings/LEARNINGS.md`、`.learnings/FEATURE_REQUESTS.md`。
- 将重复出现且可复用的经验提升到 `AGENTS.md`、`TOOLS.md` 或 `SOUL.md`，让 OpenClaw 在后续会话启动时自动注入这些规则。
- 利用 OpenClaw 的会话工具在多个活动会话之间共享经验，而不是把修正埋在单次聊天记录里。
- 保留项目级临时经验的轻量性，同时把稳定模式沉淀为团队规则或新的技能脚手架。

## 所需技能
- [self-improving-agent](https://clawhub.ai/pskoett/self-improving-agent)

## 痛点
如果没有结构化反馈闭环，OpenClaw 很容易重复犯同样的错。用户纠正停留在聊天记录里，工具故障每次都要重新踩坑，团队约定也不会自动升级成稳定规则，导致长期使用越久，重复解释和重复试错越多。

## 这个案例的核心价值
这个案例把零散反馈变成可运营的工作记忆。智能体不再把纠正当作一次性对话，而是把不同类型的信息送到对应层级：待验证的问题留在 `.learnings/`，可复用的工作流规则进入 `AGENTS.md`，工具规避经验进入 `TOOLS.md`，行为与表达偏好进入 `SOUL.md`。

它直接带来三类收益：
- 同一类命令、API 或输出格式错误不再反复重演。
- 会话重开后能在启动阶段自动读入稳定规则，减少人工重复说明。
- 多智能体协作中的交接经验会变成共享协议，而不是留在某个会话的私有上下文里。

## 典型应用场景
- 编码智能体总是把 commit message 写错格式。团队记录一次纠正后，将规则提升到 `SOUL.md`，后续会话默认沿用同样风格。
- 某个工具每周都会遇到同样的报错。失败先进入 `ERRORS.md`，确认有效的解决办法后再提升到 `TOOLS.md`，后续会话直接绕开旧坑。
- 多智能体交接时经常漏掉结果格式或汇报约定。团队把这类交接失误提升到 `AGENTS.md`，后续 spawned session 自动继承同一套协作契约。
- 重复出现的功能诉求已经形成稳定模式。团队不再只记笔记，而是把模式提炼成可复用技能脚手架。

## 如何设置
1. 安装技能：

```bash
clawdhub install self-improving-agent
```

也可以手动安装：

```bash
git clone https://github.com/peterskoett/self-improving-agent.git ~/.openclaw/skills/self-improving-agent
```

2. 在 OpenClaw 工作区中创建学习目录：

```bash
mkdir -p ~/.openclaw/workspace/.learnings
```

3. 创建三类日志文件，可以复制技能自带模板，也可以手动创建：
   - `LEARNINGS.md`：记录纠正、知识缺口、最佳实践
   - `ERRORS.md`：记录命令失败、异常和工具报错
   - `FEATURE_REQUESTS.md`：记录用户提出但当前系统还没有的能力

4. 约定提升目标文件：
   - `AGENTS.md`：工作流、委托和交接规则
   - `TOOLS.md`：工具使用坑点和已验证修复
   - `SOUL.md`：行为偏好、表达风格和沟通规则

5. 如果希望在会话启动时得到提醒，可以启用可选 hook：

```bash
cp -r hooks/openclaw ~/.openclaw/hooks/self-improvement
openclaw hooks enable self-improvement
```

6. 用以下命令检查是否生效：

```bash
openclaw hooks list
openclaw status
```

## 归档材料
最小目录结构的价值在于把“原始学习记录”和“已提升规则”分层保存：

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

来源中的提升规则：
- 工作流改进 -> `AGENTS.md`
- 工具坑点 -> `TOOLS.md`
- 行为模式 -> `SOUL.md`
- 重复模式 -> 用 `scripts/extract-skill.sh` 提炼成可复用技能

## 相关链接
- [ClawHub：self-improving-agent](https://clawhub.ai/pskoett/self-improving-agent)
- [OpenClaw Skills 仓库：self-improving-agent](https://github.com/openclaw/skills/tree/main/skills/pskoett/self-improving-agent)
- [OpenClaw 集成参考](https://github.com/openclaw/skills/blob/main/skills/pskoett/self-improving-agent/references/openclaw-integration.md)
- [阿里云：OpenClaw 部署与 self-improving-agent 实战](https://developer.aliyun.com/article/1714943)
- [博客园：把 self-improving-agent 作为新手优先安装技能](https://www.cnblogs.com/shanren/p/19685473)

## 常见问题
### 什么情况下应该把内容留在 `.learnings/`？
当它只对当前项目有效、还没有验证完成，或者暂时不值得影响未来所有会话时，就先留在 `.learnings/`，不要急着提升。

### 这和语义记忆检索是一回事吗？
不是。这个案例解决的是“哪些经验应该被记录和提升”，语义检索解决的是“已经存下来的内容怎么更快找回”。

### 不启用 hook 能用吗？
可以。hook 只是让会话开始时自动提醒你记录和复盘，核心闭环依然可以靠手动记录和定期提升完成。

### 什么时候应该把经验提炼成新技能？
当同一类修复或流程模式在多个任务、仓库或协作者之间反复出现时，就值得从笔记升级为技能。此时，来源仓库里的 `extract-skill.sh` 比继续往 `.learnings/` 追加记录更适合长期复用。
