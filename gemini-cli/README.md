# Cafe24 AI SPACE — Gemini CLI 확장

대화만으로 웹앱을 만들고 배포하세요. API 키 불필요 — 카페24 계정 로그인이 전부입니다.

## 2분 시작

```bash
gemini extensions install https://github.com/cafe24-aispace/aispace-gemini
```

설치하면 AI SPACE MCP 서버가 자동 등록됩니다. 첫 도구 호출 때 브라우저가 열리면 카페24 계정으로 로그인 1회만 하면 됩니다.

## 첫 마디는 이렇게

```
/connect                              ← 연결 확인 → 내 프로젝트 브리핑
커피숍 홈페이지 만들어서 배포해줘        ← 그냥 자연어로
/deploy my-shop                       ← 배포 전 점검 포함 배포
/logs my-shop                         ← 빌드 실패 진단
```

배포가 끝나면 `https://{호스팅ID}-{프로젝트명}.mycafe24.ai`로 바로 접속됩니다 (SSL 자동).

## 이 확장이 해주는 것

- MCP 서버 자동 등록 (`https://aih-proxy.cafe24.com/mcp`)
- AI SPACE 운영 지침(GEMINI.md) 자동 로드 — 배포 실패를 부르는 실수(Dockerfile 생성, DB 변수 하드코딩, 잘못된 포트)를 Gemini가 알아서 피합니다
- 배포 → 접속 검증 → 로그 진단까지 대화로

## 막히면

- 인증 에러 → 로그인 페이지가 아니라 **MCP 재인증**이 정답입니다
- 무료 체험은 빌드 일 5회 제한 — 실패 시 무한 재시도 대신 `/logs`로 원인부터

공식 문서: https://aispacedocs-docs.mycafe24.ai
