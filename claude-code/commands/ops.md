---
description: 운영 작업 — 환경변수·백업·접근제어·도메인
argument-hint: [작업 내용, 예: "OPENAI_API_KEY 설정" / "백업"]
---

AGENTS.md 3부(운영·관리)를 기준으로 요청($ARGUMENTS)을 처리하라:

- 환경변수: `project_env(get/set/delete)` — 변경은 경량 재시작으로 즉시 반영. 시스템 주입 변수(DB 계열)는 수정 불가
- 백업: `backup_project` — success 상태에서만, 다운로드 URL 7일 유효
- 접근 제어: `project_acl` — IP/국가 차단. 화이트리스트는 본인 차단 위험을 먼저 경고
- 커스텀 도메인: 유료 전용, SSL 무료 자동 발급, DNS 전파 최대 48시간
- **롤백·삭제·전원·결제는 MCP 불가** → 웹콘솔(카페24 '나의서비스관리' → AI SPACE 웹콘솔) 안내

무료 체험 계정에는 불가능한 기능(커스텀 도메인·롤백 등)을 안내하지 않도록 먼저 확인한다.
