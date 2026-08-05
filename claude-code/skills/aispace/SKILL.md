---
name: aispace
description: Deploy and operate web apps on Cafe24 AI SPACE (mycafe24.ai) through its MCP server. Use when the user wants to connect the AI SPACE MCP, deploy code to AI SPACE, check project status or logs, manage environment variables, back up a project, or fix a failed AI SPACE build. Keywords - AI SPACE, 카페24, mycafe24.ai, aih-proxy, 배포, MCP 연결.
---

# Cafe24 AI SPACE

이 스킬이 활성화되면 너는 사용자의 **AI SPACE 운영 파트너**다.
같은 디렉토리의 `AGENTS.md`가 정본 운영 지침이다 — **지금 읽고 그대로 따른다.**

## 실행 순서 (요약)

1. `AGENTS.md`를 읽는다 (이 스킬 디렉토리에 동봉).
2. AGENTS.md 0장의 온보딩을 즉시 실행한다:
   - AI SPACE MCP 도구(`list_my_projects` 등) 사용 가능 여부 확인
   - 미연결 → **현재 환경 기준으로** 연결 안내 (서버: `https://aih-proxy.cafe24.com/mcp`, Streamable HTTP + OAuth)
   - 연결됨 → `list_my_projects`로 현황 브리핑 → 의도 파악 (새로 만들기 / 만든 것 배포 / 운영·관리)
3. 이후 작업은 AGENTS.md의 1부(제작)·2부(가져와 배포)·3부(운영) 절차를 따른다.

## 절대 규칙 (AGENTS.md 전문과 동일 — 위반 = 배포 실패)

- Dockerfile·docker-compose·Nginx/Apache 설정 파일 생성 금지
- DB 접속정보는 자동 주입 환경변수를 읽기만 (`DB_USER` — `DB_USERNAME` 아님)
- 영속 파일은 `/app/user_data/` 하위에만
- Node 3000 / Python 8000, `0.0.0.0` 리슨
- 같은 호출이 같은 에러로 2회 연속 실패하면 멈추고 보고 (무한 재시도 금지)
- 롤백·삭제·전원·결제는 MCP 불가 → 웹콘솔 안내
- 인증 에러 = 로그인 페이지가 아니라 **MCP 재인증**이 정답
