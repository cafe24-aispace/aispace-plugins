# Cafe24 AI SPACE — Plugins & Skills

Official plugins and agent skills for **[Cafe24 AI SPACE](https://aispace.cafe24.com)** — deploy and operate web apps through conversation with your AI. No API keys; sign in with your Cafe24 account (OAuth) once.

대화만으로 웹앱을 만들고 배포하세요. API 키 불필요 — 카페24 계정 로그인이 전부입니다.

- **MCP server**: `https://aih-proxy.cafe24.com/mcp` (Streamable HTTP, OAuth 2.0)
- **Docs**: https://aispacedocs-docs.mycafe24.ai
- **Format**: conforms to the [Agent Plugins](https://agent-plugins.org) open standard v1.0.0 (root `plugin.json` + `mcp.json` + `skills/`), with client-specific manifests kept for backward compatibility.
- After deploy, your app is live at `https://{id}-{project}.mycafe24.ai` with automatic SSL.

## Install

### Plugin — one command, full bundle (recommended)

Installs the skill **and registers the MCP server** into your detected agent tools (Codex CLI, GitHub Copilot CLI, Cursor, Grok Build, Kimi Code, ...), with auto-updates:

```bash
npx plugins add cafe24-aispace/aispace-plugins
```

> Claude Code users: use the official marketplace below instead (same plugin name — avoid double-install).

### Skill only (lightweight alternative, 20+ agents)

```bash
npx skills add cafe24-aispace/aispace-plugins
```

### Claude Code (plugin)

```
/plugin marketplace add cafe24-aispace/aispace-claude-plugin
/plugin install cafe24-aispace
```

### Gemini CLI

```bash
gemini extensions install https://github.com/cafe24-aispace/aispace-gemini
```

### Antigravity CLI

```bash
# from this repo
agy plugin install ./antigravity
# or convert an existing Gemini CLI install
agy plugin import gemini
```

### Hermes

One command — no tap required:

```bash
hermes skills install cafe24-aispace/aispace-plugins/skills/aispace
```

(Optional: `hermes skills tap add cafe24-aispace/aispace-plugins` to make it browsable via `hermes skills browse`.)

### OpenClaw / other headless agents

Copy `openclaw/skills/aispace/` into your agent's skills directory — the skill includes the headless OAuth procedure (paste-back URL + token refresh).

### Cline (remote MCP)

MCP Servers → Remote Servers → add `cafe24-ai-space` with the MCP URL above. Details: [`cline/llms-install.md`](cline/llms-install.md).

## What you get

- **Guided onboarding**: on first use the agent checks the MCP connection, walks you through one-time OAuth, briefs your projects, and asks what you want to build.
- **Deploy with guardrails**: pre-deploy checks that prevent the common build failures (Dockerfile, DB env vars, ports, persistent paths).
- **Operations by conversation**: status, logs diagnosis, env vars, backups, access control.

## Repository layout

```
core/          canonical operating guide (OPERATIONS.md — kept as AGENTS.md/GEMINI.md etc. in per-channel copies) + AgentSkills-standard SKILL.md
skills/        skills.sh discovery layout (mirror of core)
claude-code/   Claude Code plugin package
gemini-cli/    Gemini CLI extension source (published at cafe24-aispace/aispace-gemini)
antigravity/   Antigravity CLI native plugin
openclaw/      OpenClaw / Hermes skill (headless auth procedure included)
cursor/        Cursor plugin package
grok-build/    Grok Build plugin package
kimi-code/     Kimi Code package + self-hosted catalog
cline/         Cline install guide (llms-install.md)
chat-kit/      chat-client kit (ChatGPT / Claude web — attach & go)
```

All adapters share one canonical core (`core/OPERATIONS.md`); per-channel folders only add packaging.

## License

[MIT](LICENSE)
