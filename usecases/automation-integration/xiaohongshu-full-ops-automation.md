---
title: OpenClaw Xiaohongshu Full Ops Automation with XiaohongshuSkills
slug: xiaohongshu-full-ops-automation
summary: Run a full Xiaohongshu operations workflow in OpenClaw, including automated publishing, comment handling, topic search, and performance data extraction.
whatItDoes: Uses XiaohongshuSkills to automate core Xiaohongshu creator operations from post publishing and comment interactions to content search and data export.
category: automation-integration
difficulty: intermediate
tags:
  - xiaohongshu-automation
  - content-operations
  - auto-publishing
  - creator-workflow
targetUser:
  - Xiaohongshu operators
  - Creator teams
  - Growth marketers
skillsUsed:
  - name: XiaohongshuSkills
    href: https://github.com/white0dew/XiaohongshuSkills
updatedAt: '2026-03-12'
published: true
---

## What it does
- Automates Xiaohongshu post publishing with title, content, image upload, and tag handling.
- Supports multi-account operation with isolated login state and account switching.
- Provides operational capabilities beyond publishing, including note search, detail retrieval, comment actions, and metrics export.

## Skills You Need
- [XiaohongshuSkills](https://github.com/white0dew/XiaohongshuSkills)

## Pain Point
Xiaohongshu daily operations combine repetitive execution tasks and high-frequency account interactions. Manual publishing, comments, and data checks consume significant time and reduce iteration speed.

## Core value of this case
- Turns fragmented creator operations into one repeatable automation pipeline.
- Reduces manual effort in publishing and post-publication maintenance.
- Improves content iteration by linking execution and data feedback in the same workflow.

## Typical scenarios
- Solo creators running daily post schedules.
- Small teams operating multiple Xiaohongshu accounts.
- Campaign periods requiring fast publish-and-review cycles.

## How to setup
1. Install `XiaohongshuSkills` and required dependencies (Python, Chrome, Playwright-related runtime as documented).
2. Complete first-time login with the provided CDP login command and verify account state.
3. Configure publishing inputs (title/content/images/tags) and choose preview or auto-publish mode.
4. Use operational commands for search, comments, and content data export to close the loop after publishing.

## Related Links
- [XiaohongshuSkills (GitHub)](https://github.com/white0dew/XiaohongshuSkills)
- [Awesome OpenClaw Usecases ZH (community usecase reference)](https://github.com/AlexAnys/awesome-openclaw-usecases-zh)
- [Post-to-xhs (upstream inspiration)](https://github.com/Angiin/Post-to-xhs)

## FAQ
### Why is this case selected as a higher-confidence Xiaohongshu automation case?
It has strong community adoption signals (high stars/forks), recent maintenance activity, and cross-reference visibility in community usecase collections.

### Is this only for publishing posts?
No. It also covers operational tasks such as search, comment workflows, and data extraction.

### Can teams use this for multiple accounts?
Yes. The documented workflow includes account isolation and switching mechanisms for multi-account operations.