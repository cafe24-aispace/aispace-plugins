# Cafe24 AI SPACE MCP — Installation Guide for AI Agents (Cline)

This document lets an AI agent set up the Cafe24 AI SPACE MCP server end-to-end without human file editing.

## What this server does

Cafe24 AI SPACE (https://aispacedocs-docs.mycafe24.ai) is a Korean AI-native PaaS. Its remote MCP server lets you deploy and operate web apps (Node.js 20 / Python 3.11 / PHP 8.2 / Static) with built-in databases (MySQL·PostgreSQL·SQLite·Redis) through tool calls — no API keys, only a Cafe24 account OAuth login.

- Server URL: `https://aih-proxy.cafe24.com/mcp`
- Transport: Streamable HTTP
- Auth: OAuth 2.0 (browser login, one time)

## Installation (Cline)

This is a **remote** MCP server — nothing to install locally.

1. Open Cline → MCP Servers icon → **Remote Servers** tab.
2. Add:
   - Server Name: `cafe24-ai-space`
   - Server URL: `https://aih-proxy.cafe24.com/mcp`
3. Save. When the server first connects, a browser window opens for Cafe24 login (OAuth). Complete it once.
4. Verify: call `list_my_projects`. A successful (possibly empty) project list means setup is complete.

If manual JSON editing is preferred, add to `cline_mcp_settings.json`:

```json
{
  "mcpServers": {
    "cafe24-ai-space": {
      "url": "https://aih-proxy.cafe24.com/mcp",
      "type": "streamableHttp"
    }
  }
}
```

## Key tools (17 official)

`deploy_project` / `update_project` / `project_upload` (deploy), `get_project_status` / `get_project_logs` / `site_verify` (status·diagnosis), `list_my_projects` / `list_my_spaces`, `project_env` (env vars), `backup_project`, `external_repo` (GitHub), `project_acl` (IP/Geo access control), `import_database` and more.

## Rules the agent must follow when generating code for AI SPACE

1. Never create Dockerfile / docker-compose / Nginx / Apache config — the platform provides runtime images; these files cause build failure.
2. Database credentials are auto-injected env vars (`DB_HOST` `DB_PORT` `DB_NAME` `DB_USER` `DB_PASSWORD`, `REDIS_HOST` `REDIS_PORT`) — read them, never set them. The variable is `DB_USER`, not `DB_USERNAME`.
3. Persistent files must live under `/app/user_data/` — everything else resets on redeploy.
4. Node listens on port 3000, Python on 8000, host `0.0.0.0`.
5. On auth errors, re-authenticate the MCP connection — do not send the user to a login page.
6. If the same call fails twice with the same error, stop and report — no retry loops.

## Troubleshooting

- 401 / re-authorization → reconnect the MCP server (OAuth re-auth), not a code problem.
- Build failed → call `get_project_logs` first; check the rules above before retrying (free trial has a 5-builds/day limit).
- Deployed but not reachable → deployment success ≠ reachable; verify with `site_verify`.

Docs: https://aispacedocs-docs.mycafe24.ai (`/llms-ko.txt`, `/llms-full-ko.txt` for machine-readable docs)
