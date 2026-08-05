---
description: 현재 프로젝트를 AI SPACE에 배포 (배포 전 점검 포함)
argument-hint: [프로젝트명 또는 비워두기]
---

이 플러그인의 AGENTS.md를 기준으로 배포를 진행하라. 새 코드면 1부, 가져온 코드면 2부의 **배포 전 점검 체크리스트를 먼저** 수행한다:

1. 런타임 지원 확인(Node/Python/PHP/Static — Go·Java·Rust 미지원) + 루트 감지 파일 확인
2. 포트(Node 3000 / Python 8000, `0.0.0.0`) · DB 하드코딩 제거(`DB_USER` 등 자동 주입 변수로) · 영속 경로 `/app/user_data/` · Dockerfile류 제거
3. 기존 프로젝트 업데이트면 `get_project_status`로 `source`(internal/github) 먼저 확인 — SOURCE_MISMATCH 방지
4. 고친 것/그대로 둔 것 목록을 보여준 뒤 배포 (`wait=false` + `get_project_status` 폴링, 콘솔 스타일 체크리스트 갱신)
5. 완료 시 `site_verify`로 접속 검증 후 URL 보고 (`https://{호스팅ID}-{프로젝트명}.mycafe24.ai`)

같은 에러 2회 연속이면 멈추고 로그와 함께 보고한다. 대상: $ARGUMENTS
