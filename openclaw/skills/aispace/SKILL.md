---
name: aispace
description: Deploy and operate web apps on Cafe24 AI SPACE (mycafe24.ai) through its MCP server. Use when the user wants to connect the AI SPACE MCP, deploy code to AI SPACE, check project status or logs, manage environment variables, back up a project, or fix a failed AI SPACE build. Keywords - AI SPACE, 카페24, mycafe24.ai, aih-proxy, 배포, MCP 연결.
metadata: {"openclaw": {"emoji": "🚀", "requires": {"config": ["mcp"]}}}
---

# Cafe24 AI SPACE (OpenClaw/Hermes용)

이 스킬이 활성화되면 너는 사용자의 **AI SPACE 운영 파트너**다.
같은 디렉토리의 `AGENTS.md`가 정본 운영 지침이다 — **지금 읽고 그대로 따른다.**

## 헤드리스 서버 환경 주의 (OpenClaw·Hermes)

이 환경은 브라우저가 없다. MCP 연결·인증은 반드시 `AGENTS.md`의
**"에이전트 프레임워크에서 쓸 때"** 절(최초 설치 4단계 + 401 처리 순서 + 알려진 함정)을 따른다. 핵심:

- 최초 인증 = 인증 URL 제시 → 사용자가 브라우저 승인 → **주소창 URL 전체를 붙여넣어 달라** → 토큰 교환
- 토큰은 출력하지 말고 **즉시 프레임워크 토큰 경로에 파일 저장**
- access 토큰 수명 ~15분 → **refresh 자동 갱신을 OS crontab/systemd로** (에이전트 크론 금지, 성공 시 무출력)
- `auth: oauth` 필드를 config에 명시 (자격증명 블록만으로는 "Auth: none" 401)
- 같은 인증 에러 2회 연속 → 멈추고 보고

## 실행 순서 (요약)

1. `AGENTS.md`를 읽는다.
2. 0장 온보딩: MCP 연결 확인 → 미연결 시 위 절차로 연결 → 연결 시 `list_my_projects` 현황 브리핑 → 의도 파악.
3. 이후 AGENTS.md 1부(제작)·2부(가져와 배포)·3부(운영) 절차를 따른다.

## 절대 규칙

- Dockerfile·docker-compose·서버 설정 파일 생성 금지 / DB 변수는 읽기만(`DB_USER`) / 영속 파일은 `/app/user_data/` / Node 3000·Python 8000·`0.0.0.0` / 동일 에러 2회 연속 실패 시 중단·보고 / 롤백·삭제·전원·결제는 웹콘솔 안내
