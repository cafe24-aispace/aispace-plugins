# Cafe24 AI SPACE — Claude Code 플러그인

대화만으로 웹앱을 만들고 배포하세요. API 키 불필요 — 카페24 계정 로그인이 전부입니다.

## 3분 시작

```
/plugin marketplace add cafe24-aispace/aispace-claude-plugin
/plugin install cafe24-aispace
```

Claude Code를 재시작(`exit` → `claude`)한 뒤, **최초 1회 인증**:

```
/mcp  →  cafe24-aispace 선택  →  Authenticate (브라우저에서 카페24 로그인)
```

## 첫 마디는 이렇게

설치가 끝났다면 아무거나 하나 던져보세요:

```
연결 잘 됐는지 확인하고 내 프로젝트 보여줘        ← /cafe24-aispace:connect
커피숍 홈페이지 만들어서 배포해줘                  ← 그냥 자연어로
왜 배포 실패했는지 로그 봐줘                       ← /cafe24-aispace:logs
```

배포가 끝나면 `https://{호스팅ID}-{프로젝트명}.mycafe24.ai`로 바로 접속됩니다 (SSL 자동).

## 명령어

| 명령 | 하는 일 |
|---|---|
| `/cafe24-aispace:connect` | 연결 확인·인증 온보딩 → 현황 브리핑 |
| `/cafe24-aispace:deploy` | 배포 전 점검 → 배포 → 접속 검증 |
| `/cafe24-aispace:status` | 프로젝트·공간 현황 |
| `/cafe24-aispace:logs` | 빌드 실패·에러 로그 진단 |
| `/cafe24-aispace:ops` | 환경변수·백업·접근제어·도메인 |

명령어를 몰라도 됩니다 — "배포해줘", "로그 봐줘"처럼 말하면 알아서 동작합니다.

## 막히면

- 인증 에러 → `/login`이 아니라 `/mcp` → cafe24-aispace → **Authenticate**
- 설치 후 도구가 안 보임 → Claude Code 재시작
- Claude.ai 웹 커넥터와 **동시 사용 금지** (계정 고정 사고 — [상세](https://aispacedocs-docs.mycafe24.ai))

공식 문서: https://aispacedocs-docs.mycafe24.ai
