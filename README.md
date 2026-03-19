# Awesome OpenClaw Cases

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](https://choosealicense.com/licenses/mit/)
[![Cases](https://img.shields.io/badge/cases-26-green.svg)](#cases)
[![Languages](https://img.shields.io/badge/languages-EN%2FCN-lightgrey.svg)](#languages)

**[中文版](README.zh.md) | English**

A curated collection of real-world OpenClaw use cases with detailed implementation guides in English and Chinese.

> **Browse online at [clawindex.app](https://clawindex.app)** - The interactive platform for exploring, filtering, and discovering OpenClaw cases.

## 🎯 What This Is

This repository contains structured, well-documented case studies that demonstrate real-world applications of OpenClaw. Each case includes:

- **Clear problem definition** - What pain points does it solve?
- **Core value proposition** - What makes this approach valuable?
- **Implementation details** - Skills needed, setup steps, and code examples
- **Typical scenarios** - When and how to apply this pattern
- **FAQ** - Common questions and answers
- **Available in English and Chinese** - Cases provided in both languages

These cases are extracted from community showcases, official documentation, blog posts, and real-world implementations, then structured for maximum reusability.

## 📚 Browse Cases by Category

### 🔧 Automation & Integration
- [Family Digital Scrapbook](usecases/automation-integration/family-digital-scrapbook.md) - Automatic photo journaling with calendar context
- [OpenClaw Three-Tier Memory System](usecases/automation-integration/openclaw-three-tier-memory-system.md) - Cross-session context management
- [WeChat Auto-Publishing Pipeline](usecases/automation-integration/wechat-auto-publishing-pipeline.md) - One-click content pipeline from topic to draft
- [Xiaohongshu Full Ops Automation](usecases/automation-integration/xiaohongshu-full-ops-automation.md) - End-to-end Xiaohongshu operations
- [TweetClaw Twitter Automation](usecases/automation-integration/tweetclaw-twitter-automation.md) - Full X/Twitter automation from chat
- [OpenClaw n8n Stack](usecases/automation-integration/openclaw-n8n-stack.md) - Self-hosted AI agents with workflow automation (400+ service integrations)
- [Multi-Agent Orchestration Specialists](usecases/automation-integration/multi-agent-orchestration-specialists.md) - 14+ specialist AI agents with parallel execution (15s human time)
- [OpenClaw Home Assistant Add-on](usecases/automation-integration/openclaw-home-assistant-addon.md) - AI gateway for smart home automation with browser automation
- [OpenClaw Prediction Market Trading](usecases/automation-integration/openclaw-prediction-market-trading.md) - Automated Polymarket trading with 115K weekly returns

### 📊 Data Analytics
- [Semantic Memory Search](usecases/data-analytics/semantic-memory-search.md) - Knowledge recall with semantic retrieval
- [Network Latency Benchmark](usecases/data-analytics/network-latency-benchmark.md) - Multi-node coordination latency analysis

### 🛠 Engineering
- [OpenClaw Opik Observability](usecases/engineering/openclaw-opik-observability.md) - Observability practices with Opik
- [Swift Logger Package (TDD)](usecases/engineering/swift-logger-package-tdd.md) - Test-driven development for Swift libraries

### ⚙ Operations
- [Event Guest Confirmation Supercall](usecases/operations/event-guest-confirmation-supercall.md) - Automated guest confirmation workflow
- [GitHub Stale Issue Cleanup](usecases/operations/github-stale-issue-cleanup.md) - Periodic issue management and cleanup
- [Log Anomaly Detection](usecases/operations/log-anomaly-detection.md) - Rolling baseline comparison for anomaly alerts

### 🚀 Product Growth
- [Market Research Product Factory](usecases/product-growth/market-research-product-factory.md) - Research to productization pipeline
- [Automated Social Media Posting](usecases/product-growth/automated-social-media-posting.md) - Content drafting, review, and scheduling
- [Price Comparison Shopping Assistant](usecases/product-growth/price-comparison-shopping-assistant.md) - Cross-platform cost comparison
- [Customer Signal Scanner](usecases/product-growth/customer-signal-scanner.md) - Community feedback signal detection
- [Pre-Build Idea Validator](usecases/product-growth/pre-build-idea-validator.md) - Multi-source validation before development
- [Content Factory](usecases/product-growth/content-factory.md) - Multi-agent content production orchestration
- [Multi-Channel Presence Sync](usecases/product-growth/multi-channel-presence-sync.md) - Cross-platform content distribution
- [OpenClaw Commercial Usecase Radar](usecases/product-growth/openclaw-commercial-usecase-radar.md) - Multi-source opportunity ranking
- [OpenClaw Product Manager Copilot](usecases/product-growth/openclaw-product-manager-copilot.md) - Self-hosted AI assistant for sprint reviews, documentation, and competitive intelligence

### 💬 Support & Success
- [Email Auto-Classifier](usecases/support-success/email-auto-classifier.md) - Email triage with urgency-based routing

## 🚀 Quick Start

### 1. Explore Cases
Browse the categories above or visit [clawindex.app](https://clawindex.app) for:
- Interactive filtering by category, difficulty, and tags
- Full-text search across all cases
- Visual case cards with quick summaries

### 2. Adapt to Your Needs
Each case is designed to be:
- **Reusable** - Clear structure and patterns you can copy
- **Adaptable** - Modify for your specific requirements
- **Complete** - Includes setup steps, skills needed, and FAQ

### 3. Contribute Your Own
Have a use case that others would benefit from? We'd love your contribution!

**Easy submission**: You only need to submit in **one language** (English OR Chinese). We'll handle machine translation to generate the other language version!

See [Contributing](#contributing) for guidelines.

## 🤝 Contributing

We welcome contributions from the OpenClaw community! Our goal is to build a comprehensive collection of real-world use cases.

### What to Contribute

- **New cases** - Share your unique OpenClaw workflows (submit in one language, we'll handle translation)
- **Case improvements** - Enhance existing cases with more details or better structure
- **Translations** - Add translations or improve existing ones
- **Bug fixes** - Fix typos, broken links, or factual errors

### Case Writing Guidelines

All cases should follow our structured format. **Frontmatter is optional** - it will be auto-generated when synced to [clawindex.app](https://clawindex.app).

1. **Frontmatter** (optional):
   ```yaml
   ---
   title: "SEO-friendly Title: Object + Action + Value"
   slug: kebab-case-slug
   summary: One-sentence summary (20-35 words)
   whatItDoes: Action + object + outcome (one sentence)
   category: engineering | documentation | operations | security-compliance | data-analytics | product-growth | support-success | automation-integration
   difficulty: beginner | intermediate | advanced
   tags: [3-5 tags, kebab-case]
   targetUser: [1-3 user types]
   skillsUsed:
     - name: Skill Name
       href: /skills/skill-slug-or-https-url
   updatedAt: "YYYY-MM-DD"
   published: true
   ---
   ```

2. **Body Structure** (required):
   - What it does / Skills You Need / Pain Point / Core value of this case / Typical scenarios / Related Links / FAQ
   - Optional: How to setup (only if source has reliable setup flow)

3. **Language Support**:
   - Create `slug.md` (English) OR `slug.zh.md` (Chinese) - you only need to submit in one language
   - We'll handle machine translation to generate the other language version automatically

4. **Quality Standards**:
   - Only include facts supported by sources
   - Don't fabricate features or data
   - Skills must be real, traceable entities

### Submission Process

1. Fork this repository
2. Create a branch: `git checkout -b feature/your-case-slug`
3. Add your case files to the appropriate `usecases/` category directory
4. Commit and push your changes
5. Open a pull request with:
   - Clear title describing the case
   - Link to original source (if applicable)
   - Explanation of why this case is valuable

## 📖 Documentation

For detailed guidelines on writing cases:

- Ensure clear structure: problem statement, value proposition, implementation details, and FAQ
- Submit in one language (English OR Chinese); we'll handle translation
- Only include factual information supported by reliable sources

## 🔗 Links

- [clawindex.app](https://clawindex.app) - Interactive case browser
- [OpenClaw Documentation](https://docs.openclaw.ai) - Official OpenClaw documentation
- [ClawHub](https://clawhub.ai/skills) - OpenClaw skills marketplace
- [OpenClaw GitHub](https://github.com/openclaw/openclaw) - OpenClaw source code

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 📚 Data Sources

Cases in this collection are compiled from:
- **Community showcases** - Real-world OpenClaw workflows shared by users
- **Official documentation** - OpenClaw docs and guides
- **Blog posts & tutorials** - Articles and implementation guides
- **Public repositories** - GitHub projects using OpenClaw

All cases are based on actual use cases and implementations.
