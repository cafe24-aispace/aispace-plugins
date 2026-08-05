# Cafe24 AI SPACE — Antigravity CLI 플러그인

대화만으로 웹앱을 만들고 배포하세요. API 키 불필요 — 카페24 계정 로그인이 전부입니다.

## 설치

```bash
# 이 저장소를 받은 뒤
agy plugin install ./antigravity

# 또는 Gemini CLI에 aispace 확장을 쓰고 있었다면
agy plugin import gemini
```

설치 후 최초 1회 브라우저에서 카페24 계정 인증(OAuth)이 필요합니다 (`/mcp`에서 확인).

## 첫 마디는 이렇게

```
연결 확인하고 내 프로젝트 보여줘
커피숍 홈페이지 만들어서 배포해줘
왜 배포 실패했는지 로그 봐줘
```

배포가 끝나면 `https://{호스팅ID}-{프로젝트명}.mycafe24.ai`로 바로 접속됩니다 (SSL 자동).

> ⚠️ `mcp_config.json`의 원격 HTTP 서버 필드명(`httpUrl`)은 Gemini CLI 계열 규약 기준입니다. agy 버전에 따라 다르면 `/mcp` 문서를 확인하세요.

공식 문서: https://aispacedocs-docs.mycafe24.ai
