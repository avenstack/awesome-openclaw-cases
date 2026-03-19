---
title: OpenClaw Home Assistant 插件：智能家居 AI 网关自托管方案
slug: openclaw-home-assistant-addon
summary: 在 Home Assistant 中部署 OpenClaw AI 网关插件，提供内置浏览器自动化、Assist Pipeline API 和 SSH/Tailscale 远程访问，实现智能家居控制。
whatItDoes: 将 OpenClaw 作为 Home Assistant 插件安装，在 Home Assistant 生态系统中提供 AI 智能体能力，包括浏览器自动化、OpenAI 兼容 API 和远程网关访问。
category: automation-integration
difficulty: intermediate
tags:
  - home-assistant
  - 智能家居
  - 浏览器自动化
  - AI网关
  - 容器化插件
targetUser:
  - 智能家居自动化爱好者
  - Home Assistant 用户
skillsUsed:
  - name: openclaw-home-assistant
    href: https://github.com/techartdev/OpenClawHomeAssistant
  - name: home-assistant-integration
    href: https://developers.home-assistant.io/docs/apps/
updatedAt: "2026-03-18"
published: true
---

## 这个案例做什么
- 通过 Supervisor 将 OpenClaw AI 网关部署为容器化 Home Assistant 插件
- 提供内置浏览器自动化和无头 Chromium，用于基于 Web 的智能家居交互
- 暴露 OpenAI 兼容的 Assist Pipeline API，用于语音助手集成
- 包含 Web Terminal 用于直接容器访问和调试
- 通过 SSH/Tailscale 启用安全远程访问，支持端口转发和网络规则
- 授予对 Home Assistant `/config` 目录的受控访问，用于 AI 智能体文件操作
- 支持 MIT 许可的自托管部署，具有完整配置控制

## 所需技能
- [openclaw-home-assistant](https://github.com/techartdev/OpenClawHomeAssistant) - 用于部署 OpenClaw AI 网关的 Home Assistant 插件，包含浏览器自动化和远程访问
- [home-assistant-integration](https://developers.home-assistant.io/docs/apps/) - Home Assistant Apps（插件）开发、容器化和 Supervisor 配置

## 痛点
将 AI 智能体与 Home Assistant 集成通常面临以下挑战：

- **部署复杂性**：在 Home Assistant 旁边运行外部 AI 网关需要手动网络配置、端口管理和服务协调
- **浏览器自动化障碍**：基于 Web 的智能家居交互（登录门户、受控仪表板）需要单独的 Selenium/Puppeteer 设置和复杂依赖
- **访问控制风险**：在没有适当沙箱的情况下授予 AI 智能体对 Home Assistant API 和配置的访问会产生安全风险
- **远程访问限制**：在家庭网络之外暴露 AI 功能需要仔细的安全配置（VPN、SSH 隧道）
- **工具碎片化**：语音助手、浏览器自动化和终端访问各自需要单独的集成

该插件通过为 Home Assistant 的 Supervisor 架构专门设计的预配置、容器化 OpenClaw 部署来解决这些挑战。

## 这个案例的核心价值
OpenClaw Home Assistant 插件在 Home Assistant 生态系统中提供集成的 AI 智能体能力：

- **容器化 simplicity**：通过 Home Assistant Supervisor 一键插件部署安装——无需手动 Docker 网络或依赖管理
- **内置浏览器自动化**：开箱即用的无头 Chromium，用于基于 Web 的智能家居交互（登录门户、能源仪表板、ISP 配置页面）
- **OpenAI 兼容 API**：Assist Pipeline 暴露标准 OpenAI API 格式，与现有语音助手和聊天界面无缝集成
- **安全远程访问**：通过 SSH/Tailscale 远程访问，具有可配置的端口转发规则——从家庭网络外部安全访问 AI 网关
- **受控文件系统访问**：对 `/config` 目录的精细权限——AI 智能体在明确授权时可以读取/修改配置
- **Web Terminal convenience**：基于浏览器的终端，无需 SSH 客户端即可直接容器调试
- **MIT 许可的可扩展性**：完整源代码可用于定制和社区贡献

## 典型应用场景
- **Web 门户自动化**：AI 智能体登录能源提供商门户，抓取使用数据，通过浏览器自动化更新 Home Assistant 传感器
- **语音助手增强**：通过 OpenAI 兼容的 Assist Pipeline API 将 OpenClaw 连接到现有语音助手（Alice、Siri），实现自然语言智能家居控制
- **远程故障排除**：通过 SSH/Tailscale 访问 Web Terminal，从家庭网络外部调试 AI 智能体行为
- **配置管理**：AI 智能体读取和修改 Home Assistant YAML 配置（`/config`），用于动态自动化调整
- **多服务编排**：单个插件通过统一的浏览器自动化管理跨多个智能家居服务（公用事业、安全、媒体）的 AI 交互
- **强制门户处理**：自动化与 ISP 强制门户、酒店 Wi-Fi 登录或认证网络服务的交互

## 如何设置

### 前置条件
- 带有 Supervisor 的 Home Assistant（Home Assistant OS 或 supervised 安装）
- 对 Home Assistant 的 SSH 访问（用于远程配置）
- 可选：安装 Tailscale 用于 tailnet 远程访问
- 用于 API 集成的 Home Assistant 长期访问令牌

### 安装步骤

**1. 将自定义仓库添加到 Home Assistant：**

导航到 Settings → Add-ons → Add-on Store → Menu（三个点）→ Add-on Repository，并输入：

```
https://github.com/techartdev/OpenClawHomeAssistant
```

**2. 安装 OpenClaw 插件：**

在 Add-on Store 中，在 Community 部分找到 "OpenClaw" 并点击 Install。

**3. 配置插件：**

在 Add-on Configuration 标签中：

```yaml
# 基本配置
options:
  # OpenClaw 网关配置
  gateway:
    port: 3456
    remote:
      enabled: true
      ssh:
        enabled: true
      tailnet:
        enabled: false  # 如果使用 Tailscale 则设置为 true

  # 浏览器自动化
  browser:
    enabled: true
    chromium:
      headless: true

  # Assist Pipeline（OpenAI 兼容 API）
  assist:
    enabled: true
    port: 8080

  # 文件系统访问
  mounts:
    - type: config
      access: rw  # 对 /config 的读写访问

  # Web Terminal
  terminal:
    enabled: true
```

**4. 启动插件：**

在 Add-on Info 标签中点击 "Start"。检查 Logs 标签以获取成功的启动消息。

**5. 访问 OpenClaw 网关：**

- 本地访问：`http://home-assistant.local:3456`
- 通过 Web Terminal：在 Add-on Info 标签中点击 "Open Web UI"

### 远程访问设置

**选项 A：SSH 远程访问**

```yaml
# 在插件配置中
remote:
  ssh:
    enabled: true
    port: 2222  # 自定义 SSH 端口
```

从外部机器连接：
```bash
ssh -p 2222 user@home-assistant.local
```

**选项 B：Tailscale Tailnet**

1. 在 Home Assistant 主机上安装 Tailscale
2. 在插件配置中启用：
```yaml
remote:
  tailnet:
    enabled: true
```
3. 从 tailnet 上的任何设备通过 Tailscale IP 访问

### Home Assistant API 集成

生成长期访问令牌：
- Home Assistant UI → Profile → Long-Lived Access Tokens → Create Token

在 AI 智能体配置中使用：
```yaml
home_assistant:
  url: http://supervisor/core
  token: YOUR_LONG_LIVED_TOKEN
```

### 浏览器自动化示例

AI 智能体控制浏览器的 Python 示例：
```python
from selenium import webdriver
from selenium.webdriver.chrome.options import Options

# 连接到插件的 Chromium
chrome_options = Options()
chrome_options.add_argument("--headless")
driver = webdriver.Chrome(
    options=chrome_options,
    service_args=["--port=9222"]  # 连接到插件的浏览器
)

# 导航到能源门户
driver.get("https://energy-provider.com/login")
# AI 智能体执行自动化...
```

### 安全注意事项

**网络隔离：**
- 插件默认在隔离容器中运行
- 仅通过 Supervisor 网络设置暴露必要的端口（网关、SSH）

**访问控制：**
- 使用 SSH 密钥身份验证而不是密码
- 将 `/config` 访问限制为 `ro`（只读），除非需要写访问
- 将 Home Assistant API 令牌范围限制为最低要求

**更新：**
- 当仓库发布新版本时，插件自动更新
- 监控插件日志以获取破坏性更改

### 故障排查

**插件无法启动：**
- 检查 Supervisor 日志：Settings → System → Logs → Supervisor
- 验证端口冲突（3456、8080、2222）与其他插件
- 确保 Home Assistant 中有足够的磁盘空间

**浏览器自动化失败：**
- 验证在插件配置中启用了 Chromium
- 检查 `/config/openclaw/browser.log` 以获取浏览器错误
- 确保足够的内存（浏览器建议 512MB+ RAM）

**远程访问不可达：**
- 验证在插件配置中启用了 SSH/Tailscale
- 检查 Home Assistant 防火墙规则
- 首先在本地测试 SSH：`ssh -p 2222 root@home-assistant.local`

**对 /config 的权限被拒绝：**
- 在插件配置中添加 `mounts: - type: config, access: rw`
- 配置更改后重启插件

## 归档材料

### 插件组件列表

**核心组件：**
- **AI Gateway**：OpenClaw 网关服务器（端口 3456）
- **Browser Automation**：无头 Chromium 和 Selenium WebDriver
- **Assist Pipeline**：OpenAI 兼容 API 端点（端口 8080）
- **Web Terminal**：基于浏览器的终端（ttyd）
- **SSH Server**：用于远程访问的 Dropbear（端口 2222）

**容器架构：**
- 基于 Home Assistant Supervisor 基础镜像
- 与 Home Assistant 核心隔离，但共享 `/config` 挂载
- 通过 Supervisor 的内部网络进行网络访问

### repository.yaml 结构

```yaml
name: "OpenClaw Home Assistant"
url: "https://github.com/techartdev/OpenClawHomeAssistant"
maintainer: "techartdev"
```

这个最小的 repository.yaml 使 Home Assistant 能够从 GitHub 仓库发现和获取插件版本。

### 许可证

MIT License - 完整源代码可用于修改和重新分发。

### 远程访问安全模型

**默认行为：**
- 仅环回绑定（仅 localhost）
- SSH 需要在配置中明确启用
- 端口转发默认禁用

**安全建议：**
- 使用 Tailscale 进行远程访问，而不是将 SSH 暴露到互联网
- 将 SSH 限制为基于密钥的身份验证
- 将 `/config` 访问限制为只读，除非需要修改
- 监控插件日志以获取未经授权的访问尝试

## 相关链接
- [OpenClaw Home Assistant Add-on](https://github.com/techartdev/OpenClawHomeAssistant) — 容器化插件源代码和发布版本
- [Home Assistant Apps 文档](https://developers.home-assistant.io/docs/apps/) — 官方插件开发和部署指南
- [OpenClaw 远程访问文档](https://docs.openclaw.ai/gateway/remote) — SSH 和 tailnet 配置参考
- [社区讨论线程](https://community.home-assistant.io/t/openclaw-clawdbot-on-home-assistant/981467) — 用户经验和故障排除
- [中文实战指南](https://eastondev.com/blog/zh/posts/ai/20260227-openclaw-smart-home-guide/) — 中文部署和智能家居集成教程

## 常见问题

### 这个插件与在 Docker 中单独运行 OpenClaw 有什么区别？

该插件直接与 Home Assistant Supervisor 集成，提供简化的网络、通过插件商店的自动更新以及对 Home Assistant `/config` 目录的预配置访问。单独运行 OpenClaw 需要手动 Docker 网络、端口配置和单独的更新管理。该插件还包括 Web Terminal UI 和 Supervisor 特定的优化。

### AI 智能体可以访问我的所有 Home Assistant 配置吗？

只有在明确配置的情况下。默认情况下，插件无法访问 `/config`。您必须在插件配置中添加挂载：`mounts: - type: config, access: ro` 用于只读或 `access: rw` 用于读写。从只读访问开始，仅在您的自动化需要修改配置时才启用写访问。

### 浏览器自动化是否占用大量资源？

是的，运行无头 Chromium 需要额外的内存（通常 200-400MB）。如果您的 Home Assistant 主机内存有限（例如总共 2GB），请考虑在插件配置中禁用浏览器自动化，或仅在计划任务期间使用浏览器自动化。您还可以在单独的机器上运行浏览器密集型任务，并通过 SSH 远程访问。

### SSH 远程访问功能有多安全？

SSH 访问在隔离容器内使用 Dropbear SSH 服务器。安全最佳实践：(1) 使用基于密钥的身份验证而不是密码，(2) 通过 Supervisor 网络设置将 SSH 限制为仅本地网络，(3) 考虑使用 Tailscale 进行远程访问，而不是将 SSH 暴露到互联网，(4) 监控 `/config/openclaw/ssh.log` 以获取访问尝试。插件的 SSH 不提供对 Home Assistant 核心的 shell 访问——仅对 OpenClaw 容器提供。

### 我可以将其与 Home Assistant 原生语音以外的语音助手一起使用吗？

可以。Assist Pipeline 暴露 OpenAI 兼容的 API 端点（默认端口 8080）。这意味着您可以与任何支持 OpenAI API 格式的语音助手集成，例如 Alice、通过 HomeKit 的自定义 Siri 快捷方式或第三方语音平台。API 遵循标准 OpenAI 聊天完成格式。

### 这个插件适用于 Home Assistant Container（手动安装）吗？

不适用。该插件需要 Home Assistant Supervisor，它包含在 Home Assistant OS 和 supervised 安装中。Home Assistant Container（手动 Docker Compose 方法）没有插件管理所需的 Supervisor API。对于 Container 安装，按照官方 OpenClaw 文档将 OpenClaw 作为单独的 Docker 容器运行。

### 如果插件崩溃或无响应会发生什么？

Home Assistant Supervisor 监控插件健康状态，如果插件崩溃将自动重启。通过 Supervisor → Add-ons → OpenClaw → Logs 检查插件日志。对于持续问题，您可以 (1) 在 Supervisor 中增加插件资源限制，(2) 禁用浏览器自动化等资源密集型功能，或 (3) 检查 GitHub issues 以获取已知问题。

### 我可以运行此插件的多个实例吗？

技术上可以，但不推荐。每个插件实例需要单独的端口配置（网关、SSH、浏览器端口）以避免冲突。对于大多数用例，具有多个智能体/通道的单个 OpenClaw 实例提供更好的资源利用率。如果您需要隔离，请考虑在单独的 Docker 容器中运行 OpenClaw，而不是多个插件。

### 如何更新插件？

当插件商店中有新版本可用时，Home Assistant Supervisor 会自动通知您。在 Add-on Info 标签中点击 "Update"。插件从 GitHub 仓库的发布版本中提取新版本。更新前始终备份您的 `/config` 目录，以防出现破坏性更改。
