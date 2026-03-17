# Contributing to Awesome OpenClaw Cases

Thank you for your interest in contributing to Awesome OpenClaw Cases! This document provides guidelines and instructions for contributing.

## 🎯 Our Mission

We're building a comprehensive collection of real-world OpenClaw use cases to help users:

- **Discover** practical applications of OpenClaw
- **Learn** from community implementations
- **Adapt** proven patterns to their own needs
- **Contribute** back to the ecosystem

## 🤝 Ways to Contribute

### 1. Add New Cases

Have an OpenClaw use case that others would benefit from? Submit it as a new case!

**Important**: You only need to submit in **one language** (English OR Chinese). We'll handle machine translation to generate the other language version!

**Steps:**
1. Review existing cases in the same category to understand style
2. Write your case following [Case Writing Guidelines](#case-writing-guidelines)
3. Open a Pull Request with your case file
4. After your PR is approved, the case will be automatically synced to [clawindex.app](https://clawindex.app)

**Note on Frontmatter**: Frontmatter is **not required** in your submission. When your case is synced to [clawindex.app](https://clawindex.app), the platform will automatically generate standardized frontmatter for both languages.

### 2. Improve Existing Cases

Found a case that could be better? Help improve it!

**Types of improvements:**
- Add more implementation details
- Clarify ambiguous sections
- Add missing FAQ entries
- Fix typos or grammar issues
- Update outdated information
- Add better examples or code snippets

**Steps:**
1. Fork this repository
2. Find the case file you want to improve
3. Make your changes
4. Open a Pull Request with clear description of improvements

### 3. Add Translations

**You can translate in two ways:**

#### Option A: Translate Existing Cases
1. Choose a case that only exists in one language
2. Create `slug.<lang>.md` (e.g., `slug.zh.md` for Chinese)
3. Translate all content following the same structure
4. Open a Pull Request

#### Option B: Machine Translation Assistance
If you submit a case in one language only, we'll use machine translation to generate the other language version. This helps us:
- Accept contributions from users who may not be fluent in both languages
- Quickly expand case coverage
- Maintain semantic alignment through review

**Note**: Human translations are always preferred over machine translations, but we welcome machine-translated drafts that the community can review and improve.

### 4. Report Issues

Found a bug or have a suggestion?

- Open an issue with:
  - Clear title describing the problem
  - Steps to reproduce (for bugs)
  - Expected vs actual behavior
  - Screenshots if applicable

## 📝 Case Writing Guidelines

### Structure Requirements

Your case should include the following sections (frontmatter is optional):

1. **Title** (at the top, H1): Clear, descriptive title
2. **Body** (required sections for English cases):
   - What it does
   - Skills You Need
   - Pain Point
   - Core value of this case
   - Typical scenarios
   - How to setup (optional, only if source has reliable setup flow)
   - Related Links
   - FAQ

3. **Body** (required sections for Chinese cases):
   - 这个案例做什么
   - 所需技能
   - 痛点
   - 这个案例的核心价值
   - 典型应用场景
   - 如何设置（可选）
   - 相关链接
   - 常见问题

### Frontmatter (Optional)

You **don't need to include frontmatter** when submitting. However, if you want to include it, here's the structure:

```yaml
---
title: "SEO-friendly Title: Object + Action + Value"
slug: unique-kebab-case-slug
summary: One-sentence summary (20-35 words EN, 45-90 chars ZH)
whatItDoes: Action + object + outcome (one sentence)
category: engineering | documentation | operations | security-compliance | data-analytics | product-growth | support-success | automation-integration
difficulty: beginner | intermediate | advanced
tags: [3-5 tags, kebab-case]
targetUser: [1-3 user types]
skillsUsed:
  - name: Skill Name
    href: /skills/slug-or-https-url
updatedAt: "YYYY-MM-DD"
published: true
---
```

**Note**: When your PR is approved, [clawindex.app](https://clawindex.app) will automatically generate standardized frontmatter for both language versions.

### Content Guidelines

#### DO ✅

- Use real sources: official docs, blog posts, GitHub repos, release notes
- Only include facts supported by sources
- Be specific: what problem, what solution, what value
- Use clear, concise language
- Add Related Links with at least 1 real, accessible URL
- Include FAQ with direct question-answer format

#### DON'T ❌

- Don't fabricate features, data, or user testimonials
- Don't use vague marketing language like "improves efficiency" without specifics
- Don't copy-paste large sections from source (summarize and structure)
- Don't include "How to setup" if source lacks reliable setup flow
- Don't add skills that don't exist or can't be traced

### Skills Used Rules

If you reference skills, they must be:
- Real, traceable entities from ClawHub or GitHub
- Referenced with valid URLs
- Directly involved in the case's core workflow

### Category Selection

Choose one primary category based on the case's **main value**:

| Category | Focus | Examples |
|-----------|----------|-----------|
| `engineering` | Software development, build, test, CI/CD | Code quality, automation, testing |
| `documentation` | Docs generation, maintenance, tooling | API docs, auto-docs, knowledge management |
| `operations` | Ops, monitoring, alerting, troubleshooting | Monitoring, logs, incidents |
| `security-compliance` | Security scans, compliance, permissions | Vulnerability scans, audits, access control |
| `data-analytics` | Data collection, processing, analysis | Data pipelines, metrics, reports |
| `product-growth` | User growth, optimization, A/B testing | User analytics, growth strategies |
| `support-success` | Customer service, problem solving | Auto-support, tickets, FAQ |
| `automation-integration` | Third-party integration, workflows | Service integration, automation, webhooks |

### Tag Guidelines

- **3-5 tags** per case
- **kebab-case** format (lowercase, hyphens)
- Use industry-standard terminology (e.g., `api-integration` not `api-connect`)
- Include at least 1 scenario tag + 1 result tag

For Chinese cases, translate common terms but keep:
- Brand names: OpenClaw, GitHub, Docker
- Tech stack: React, FastAPI, LangGraph
- Industry terms: API, CI/CD

### De-duplication

Before creating a new case:
1. Search existing cases by slug and topic
2. If topic overlaps significantly, **improve existing case** instead of creating duplicate
3. Use `slug` as a unique identifier

## 🌐 Sync to clawindex.app

After your Pull Request is reviewed and approved:

1. **Automatic Frontmatter Generation**: The platform will automatically generate standardized frontmatter for both English and Chinese versions
2. **Website Sync**: Your case will appear on [clawindex.app](https://clawindex.app) with full indexing
3. **Search Integration**: Users can find your case through search and filters on the platform
4. **Cross-Language Support**: If you submitted in one language only, we'll use machine translation to generate the other version

**Timeline**: After PR approval, cases are typically synced within 24-48 hours.

## 📤 Pull Request Process

1. **Fork** this repository
2. **Create branch**: `git checkout -b feature/your-case-slug`
3. **Add file**:
   - English OR Chinese: `usecases/category/slug.md` or `usecases/category/slug.zh.md`
   - You only need to submit **one language**!
4. **Commit** with clear message:
   - `Add: [category] case name` (for new cases)
   - `Add translation: [category] case name` (for translations)
   - `Fix: [category] correct issue description` (for fixes)
5. **Push** to your fork
6. **Open PR** with:
   - Clear title: `[EN/ZH] Add/fix/improve: case name`
   - Description:
     - What this PR does
     - Link to original source (if applicable)
     - Note which language this is (EN, ZH, or both)
     - Any additional context

**After Approval**: Your case will automatically sync to [clawindex.app](https://clawindex.app) within 24-48 hours.

## 🎨 Code Style

- Use **YAML** for frontmatter (optional)
- Use **Markdown** for body
- Follow existing formatting in other cases
- Keep lines under 100 characters where possible
- Use sentence case for headings (e.g., "Pain Point" not "pain point")

## 📖 Documentation Links

- Ensure clear structure: problem statement, value proposition, implementation details, and FAQ
- You only need to submit in one language (English OR Chinese); we'll handle translation
- Only include factual information supported by reliable sources

## 🤝 Community Guidelines

### Code of Conduct

- Be respectful and inclusive
- Provide constructive feedback
- Assume good intentions
- Focus on what's best for the community

### Getting Help

- Check existing cases before asking
- Search issues for similar questions
- Join [OpenClaw Discord](https://discord.com/invite/clawd) for real-time help

## 📊 Impact

Your contributions help the OpenClaw ecosystem by:

- **Growing case library** - More examples for users to learn from
- **Improving quality** - Better documentation through peer review
- **Expanding reach** - More languages, more domains covered
- **Driving adoption** - Proven patterns help new users get started faster
- **Enabling discovery** - Cases on [clawindex.app](https://clawindex.app) help users find solutions faster

Thank you for contributing! 🚀
