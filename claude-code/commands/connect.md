---
description: AI SPACE MCP 연결 확인·인증 온보딩
---

이 플러그인의 AGENTS.md(플러그인 루트)를 읽고 0장 온보딩을 실행하라:

1. AI SPACE MCP 도구(`list_my_projects` 등)가 사용 가능한지 확인한다.
2. 미연결이면 이 환경(Claude Code) 기준으로 연결을 안내한다 — 이 플러그인은 `.mcp.json`으로 서버(`https://aih-proxy.cafe24.com/mcp`)를 이미 제안하므로, 대부분 `/mcp` → cafe24-ai-space → Authenticate(브라우저 OAuth 1회)만 남는다.
3. 인증 에러가 나면 로그인 페이지가 아니라 **MCP 재인증**으로 안내한다.
4. 연결되면 `list_my_projects`로 현황을 브리핑하고 의도를 묻는다 (새로 만들기 / 만든 것 배포 / 운영·관리).
