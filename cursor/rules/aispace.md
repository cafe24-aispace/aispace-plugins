# AI SPACE 작업 규칙 (Cursor)

사용자가 AI SPACE(mycafe24.ai) 배포·운영을 요청하면, 플러그인 루트의 `AGENTS.md`를 읽고 그 지침을 따른다.

핵심 요약:
- MCP 서버는 이 플러그인의 `mcp.json`이 등록한다 (`https://aih-proxy.cafe24.com/mcp`) — 최초 1회 브라우저 OAuth 인증 필요
- 온보딩: 연결 확인 → `list_my_projects` 현황 브리핑 → 의도 파악 (새로 만들기 / 만든 것 배포 / 운영·관리)
- 절대 규칙: Dockerfile류 생성 금지 / DB 변수는 읽기만(`DB_USER`) / 영속 파일 `/app/user_data/` / Node 3000·Python 8000·`0.0.0.0` / 동일 에러 2회 연속 실패 시 중단·보고 / 롤백·삭제·전원·결제는 웹콘솔 안내
- 인증 에러 = 로그인 페이지가 아니라 MCP 재인증
