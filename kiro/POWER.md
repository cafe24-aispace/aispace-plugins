---
name: "cafe24-aispace"
displayName: "Cafe24 AI SPACE"
description: "Deploy and operate web apps on Cafe24 AI SPACE by conversation - MCP onboarding, guarded deploys, log diagnosis, and operations. Cafe24 account OAuth; no API keys."
keywords: ["aispace", "cafe24", "deploy", "mcp", "hosting", "mycafe24"]
author: "Cafe24 AI SPACE"
---

# Cafe24 AI SPACE

## Onboarding

When this power is first activated:

1. Verify the MCP server `cafe24-aispace` is available (tools like `list_my_projects`, `deploy_project`). The bundled `mcp.json` registers it via the `mcp-remote` bridge to `https://aih-proxy.cafe24.com/mcp`.
2. On first tool call a browser opens for one-time Cafe24 OAuth sign-in — wait for the user to complete it. On auth errors, re-authenticate the MCP connection; never send the user to a login page.
3. Once connected, call `list_my_projects`, brief the user on their projects, and ask what they want to do: build something new / deploy existing code / operate a running app.
4. Then follow `steering/aispace-operations.md` for all AI SPACE work.

## Hard rules (violations cause failed deploys)

- Never create Dockerfile, docker-compose, or Nginx/Apache config files.
- Database credentials are auto-injected env vars (`DB_HOST` `DB_PORT` `DB_NAME` `DB_USER` `DB_PASSWORD`, `REDIS_*`) — read them, never set them. The variable is `DB_USER`, not `DB_USERNAME`.
- Persistent files go under `/app/user_data/` only.
- Node listens on port 3000, Python on 8000, host `0.0.0.0`.
- If the same call fails twice with the same error, stop and report — no retry loops.
- Rollback / delete / power / billing are not available over MCP — direct the user to the AI SPACE web console.

# Steering File Mappings

- All AI SPACE deploy/operate work → aispace-operations.md
