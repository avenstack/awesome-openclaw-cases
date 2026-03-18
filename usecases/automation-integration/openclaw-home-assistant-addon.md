---
title: "OpenClaw Home Assistant Add-on: Self-Hosted AI Gateway for Smart Home Automation"
slug: openclaw-home-assistant-addon
summary: "Deploy OpenClaw AI Gateway as Home Assistant Add-on with built-in browser automation, Assist Pipeline API, and SSH/Tailscale remote access for intelligent smart home control."
whatItDoes: "Installs OpenClaw as a Home Assistant Add-on to provide AI agent capabilities including browser automation, OpenAI-compatible API, and remote gateway access within the Home Assistant ecosystem."
category: automation-integration
difficulty: intermediate
tags:
  - home-assistant
  - smart-home
  - browser-automation
  - ai-gateway
  - containerized-add-on
targetUser:
  - Smart home automation enthusiasts
  - Home Assistant power users
  - DIY home AI system builders
skillsUsed:
  - name: openclaw-home-assistant
    href: https://github.com/techartdev/OpenClawHomeAssistant
  - name: home-assistant-integration
    href: https://developers.home-assistant.io/docs/apps/
updatedAt: "2026-03-18"
published: true
---

## What it does
- Deploys OpenClaw AI Gateway as a containerized Home Assistant Add-on through Supervisor
- Provides built-in browser automation with headless Chromium for web-based smart home interactions
- Exposes OpenAI-compatible Assist Pipeline API for voice assistant integrations
- Includes Web Terminal for direct container access and debugging
- Enables remote over SSH/Tailscale with secure port forwarding and network rules
- Grants controlled access to Home Assistant `/config` directory for AI agent file operations
- Supports MIT-licensed self-hosted deployment with full configuration control

## Skills You Need
- [openclaw-home-assistant](https://github.com/techartdev/OpenClawHomeAssistant) - Home Assistant Add-on for deploying OpenClaw AI Gateway with browser automation and remote access
- [home-assistant-integration](https://developers.home-assistant.io/docs/apps/) - Home Assistant Apps (add-ons) development, containerization, and Supervisor configuration

## Pain Point
Integrating AI agents with Home Assistant typically faces several challenges:

- **Deployment complexity**: Running external AI gateways alongside Home Assistant requires manual networking, port management, and service coordination
- **Browser automation barriers**: Web-based smart home interactions (login portals, captive dashboards) require separate Selenium/Puppeteer setups with complex dependencies
- **Access control risks**: Granting AI agents access to Home Assistant APIs and configurations without proper sandboxing creates security concerns
- **Remote access limitations**: Exposing AI capabilities outside the home network demands careful security configuration (VPNs, SSH tunnels)
- **Fragmented tooling**: Voice assistants, browser automation, and terminal access each require separate integrations

This Add-on addresses these challenges by providing a pre-configured, containerized OpenClaw deployment designed specifically for Home Assistant's Supervisor architecture.

## Core value of this case
OpenClaw Home Assistant Add-on provides integrated AI agent capabilities within the Home Assistant ecosystem:

- **Containerized simplicity**: Install through Home Assistant Supervisor with one-click add-on deployment—no manual Docker networking or dependency management
- **Built-in browser automation**: Headless Chromium included out-of-the-box for web-based smart home interactions (login portals, energy dashboards, ISP configuration pages)
- **OpenAI-compatible API**: Assist Pipeline exposes standard OpenAI API format for seamless integration with existing voice assistants and chat interfaces
- **Secure remote access**: Remote over SSH/Tailscale with configurable port forwarding rules—access AI gateway from outside your home network safely
- **Controlled filesystem access**: Granular permissions for `/config` directory access—AI agents can read/modify configurations when explicitly authorized
- **Web Terminal convenience**: Browser-based terminal for direct container debugging without SSH clients
- **MIT-licensed extensibility**: Full source code available for customization and community contributions

## Typical scenarios
- **Web portal automation**: AI agent logs into energy provider portals, scrapes usage data, and updates Home Assistant sensors via browser automation
- **Voice assistant enhancement**: Connect OpenClaw to existing voice assistants (Alice, Siri) via OpenAI-compatible Assist Pipeline API for natural language smart home control
- **Remote troubleshooting**: Access Web Terminal through SSH/Tailscale to debug AI agent behavior from outside the home network
- **Configuration management**: AI agents read and modify Home Assistant YAML configurations in `/config` for dynamic automation adjustments
- **Multi-service orchestration**: Single add-on manages AI interactions across multiple smart home services (utilities, security, media) through unified browser automation
- **Captive portal handling**: Automate interactions with ISP captive portals, hotel Wi-Fi logins, or authenticated network services

## How to setup

### Prerequisites
- Home Assistant with Supervisor (Home Assistant OS or supervised installation)
- SSH access to Home Assistant (for remote configuration)
- Optional: Tailscale installation for tailnet remote access
- Home Assistant long-lived access token for API integration

### Installation Steps

**1. Add custom repository to Home Assistant:**

Navigate to Settings → Add-ons → Add-on Store → Menu (three dots) → Add-on Repository, and enter:

```
https://github.com/techartdev/OpenClawHomeAssistant
```

**2. Install OpenClaw Add-on:**

In the Add-on Store, find "OpenClaw" in the Community section and click Install.

**3. Configure the Add-on:**

In the Add-on Configuration tab:

```yaml
# Basic configuration
options:
  # OpenClaw Gateway configuration
  gateway:
    port: 3456
    remote:
      enabled: true
      ssh:
        enabled: true
      tailnet:
        enabled: false  # Set to true if using Tailscale

  # Browser automation
  browser:
    enabled: true
    chromium:
      headless: true

  # Assist Pipeline (OpenAI-compatible API)
  assist:
    enabled: true
    port: 8080

  # Filesystem access
  mounts:
    - type: config
      access: rw  # Read/write access to /config

  # Web Terminal
  terminal:
    enabled: true
```

**4. Start the Add-on:**

Click "Start" in the Add-on Info tab. Check the Logs tab for successful startup messages.

**5. Access OpenClaw Gateway:**

- Local access: `http://home-assistant.local:3456`
- Via Web Terminal: Click "Open Web UI" in the Add-on Info tab

### Remote Access Setup

**Option A: SSH Remote Access**

```yaml
# In Add-on configuration
remote:
  ssh:
    enabled: true
    port: 2222  # Custom SSH port
```

Connect from external machine:
```bash
ssh -p 2222 user@home-assistant.local
```

**Option B: Tailscale Tailnet**

1. Install Tailscale on Home Assistant host
2. Enable in Add-on configuration:
```yaml
remote:
  tailnet:
    enabled: true
```
3. Access via Tailscale IP from any device on your tailnet

### Home Assistant API Integration

Generate long-lived access token:
- Home Assistant UI → Profile → Long-Lived Access Tokens → Create Token

Use in AI agent configurations:
```yaml
home_assistant:
  url: http://supervisor/core
  token: YOUR_LONG_LIVED_TOKEN
```

### Browser Automation Example

Python example for AI agent controlling browser:
```python
from selenium import webdriver
from selenium.webdriver.chrome.options import Options

# Connect to Add-on's Chromium
chrome_options = Options()
chrome_options.add_argument("--headless")
driver = webdriver.Chrome(
    options=chrome_options,
    service_args=["--port=9222"]  # Connect to add-on's browser
)

# Navigate to energy portal
driver.get("https://energy-provider.com/login")
# AI agent performs automation...
```

### Security Considerations

**Network isolation:**
- Add-on runs in isolated container by default
- Only expose necessary ports (gateway, SSH) via Supervisor network settings

**Access control:**
- Use SSH key authentication instead of passwords
- Restrict `/config` access to `ro` (read-only) unless write access required
- Limit Home Assistant API token scopes to minimum required

**Updates:**
- Add-on auto-updates when repository releases new versions
- Monitor add-on logs for breaking changes

### Troubleshooting

**Add-on won't start:**
- Check Supervisor logs: Settings → System → Logs → Supervisor
- Verify port conflicts (3456, 8080, 2222) with other add-ons
- Ensure sufficient disk space in Home Assistant

**Browser automation failures:**
- Verify Chromium is enabled in add-on configuration
- Check `/config/openclaw/browser.log` for browser errors
- Ensure sufficient memory (recommend 512MB+ RAM for browser)

**Remote access unreachable:**
- Verify SSH/Tailscale enabled in add-on configuration
- Check Home Assistant firewall rules
- Test SSH locally first: `ssh -p 2222 root@home-assistant.local`

**Permission denied on /config:**
- Add `mounts: - type: config, access: rw` to add-on configuration
- Restart add-on after configuration changes

## Archived Materials

### Add-on Component List

**Core Components:**
- **AI Gateway**: OpenClaw gateway server (port 3456)
- **Browser Automation**: Headless Chromium with Selenium WebDriver
- **Assist Pipeline**: OpenAI-compatible API endpoint (port 8080)
- **Web Terminal**: Browser-based terminal (ttyd)
- **SSH Server**: Dropbear for remote access (port 2222)

**Container Architecture:**
- Based on Home Assistant Supervisor base image
- Isolated from Home Assistant core but shares `/config` mount
- Network access via Supervisor's internal network

### repository.yaml Structure

```yaml
name: "OpenClaw Home Assistant"
url: "https://github.com/techartdev/OpenClawHomeAssistant"
maintainer: "techartdev"
```

This minimal repository.yaml enables Home Assistant to discover and fetch add-on versions from the GitHub repository.

### License

MIT License - Full source code available for modification and redistribution.

### Remote Access Security Model

**Default behavior:**
- Loopback-only binding (localhost only)
- SSH requires explicit enable in configuration
- Port forwarding disabled by default

**Security recommendations:**
- Use Tailscale for remote access instead of exposing SSH to internet
- Restrict SSH to key-based authentication
- Limit `/config` access to read-only unless modifications required
- Monitor add-on logs for unauthorized access attempts

## Related Links
- [OpenClaw Home Assistant Add-on](https://github.com/techartdev/OpenClawHomeAssistant) — Containerized add-on source code and releases
- [Home Assistant Apps Documentation](https://developers.home-assistant.io/docs/apps/) — Official add-on development and deployment guide
- [OpenClaw Remote Access Documentation](https://docs.openclaw.ai/gateway/remote) — SSH and tailnet configuration reference
- [Community Discussion Thread](https://community.home-assistant.io/t/openclaw-clawdbot-on-home-assistant/981467) — User experiences and troubleshooting
- [中文实战指南](https://eastondev.com/blog/zh/posts/ai/20260227-openclaw-smart-home-guide/) — Chinese deployment and smart home integration tutorial

## FAQ

### What's the difference between this add-on and running OpenClaw in Docker separately?

This add-on integrates directly with Home Assistant Supervisor, providing simplified networking, automatic updates through the add-on store, and pre-configured access to Home Assistant's `/config` directory. Running OpenClaw separately requires manual Docker networking, port configuration, and separate update management. The add-on also includes Web Terminal UI and Supervisor-specific optimizations.

### Can the AI agent access all my Home Assistant configurations?

Only if explicitly configured. By default, the add-on has no access to `/config`. You must add a mount in the add-on configuration: `mounts: - type: config, access: ro` for read-only or `access: rw` for read-write. Start with read-only access and only enable write access if your automation requires modifying configurations.

### Is browser automation resource-intensive?

Yes, running headless Chromium requires additional memory (typically 200-400MB). If your Home Assistant host has limited RAM (e.g., 2GB total), consider disabling browser automation in the add-on configuration or using browser automation only during scheduled tasks. You can also run browser-intensive tasks on a separate machine and access via SSH remote.

### How secure is the SSH remote access feature?

SSH access uses Dropbear SSH server within the isolated container. Security best practices: (1) Use key-based authentication instead of passwords, (2) Restrict SSH to local network only via Supervisor network settings, (3) Consider using Tailscale for remote access instead of exposing SSH to internet, (4) Monitor `/config/openclaw/ssh.log` for access attempts. The add-on's SSH does not provide shell access to Home Assistant core—only to the OpenClaw container.

### Can I use this with voice assistants other than Home Assistant's native voice?

Yes. The Assist Pipeline exposes an OpenAI-compatible API endpoint (port 8080 by default). This means you can integrate with any voice assistant that supports OpenAI API format, such as Alice, custom Siri shortcuts via HomeKit, or third-party voice platforms. The API follows standard OpenAI chat completion format.

### Does this add-on work on Home Assistant Container (manual installation)?

No. This add-on requires Home Assistant Supervisor, which is included in Home Assistant OS and supervised installations. Home Assistant Container (the manual Docker Compose method) does not have the Supervisor API needed for add-on management. For Container installations, run OpenClaw as a separate Docker container following the official OpenClaw documentation.

### What happens if the add-on crashes or becomes unresponsive?

Home Assistant Supervisor monitors add-on health and will automatically restart the add-on if it crashes. Check the add-on logs via Supervisor → Add-ons → OpenClaw → Logs. For persistent issues, you can (1) Increase add-on resource limits in Supervisor, (2) Disable resource-intensive features like browser automation, or (3) Check GitHub issues for known problems.

### Can I run multiple instances of this add-on?

Technically yes, but it's not recommended. Each add-on instance would require separate port configurations (gateway, SSH, browser ports) to avoid conflicts. For most use cases, a single OpenClaw instance with multiple agents/channels provides better resource utilization. If you need isolation, consider running OpenClaw in separate Docker containers instead of multiple add-ons.

### How do I update the add-on?

Home Assistant Supervisor will automatically notify you when a new version is available in the add-on store. Click "Update" in the Add-on Info tab. The add-on pulls new versions from the GitHub repository's releases. Always backup your `/config` directory before updating in case of breaking changes.
