# aispace-plugins — 멀티 프로바이더 플러그인/스킬 모노레포

각 AI 클라이언트에서 **AI SPACE MCP 연결을 쉽게 하고 기본 기능을 바로 쓰게** 만드는 프로바이더별 패키지.
`aispace-kit.zip`(챗 클라이언트용)의 AGENTS.md를 **정본 코어**로 삼고, 프로바이더별 네이티브 포장만 얇게 씌운다.

> 원칙 (플레이북 설계안 5장): **코어 90% / 어댑터 10%** — 콘텐츠는 core/ 하나, 채널별로 달라지는 건 매니페스트와 연결 설정뿐.

## 구조

```
core/                 ← 정본. 여기만 수정한다
├── AGENTS.md         # 운영 지침 전문 (aispace-kit 정본과 동기화)
└── SKILL.md          # AgentSkills 표준 스킬 (크로스 에이전트)

claude-code/          ← Claude Code 플러그인 (공식 마켓플레이스)
├── .claude-plugin/plugin.json · marketplace.json
├── .mcp.json         # MCP 자동 등록
├── commands/         # /aispace:connect·deploy·status·logs·ops
├── skills/aispace/SKILL.md
└── AGENTS.md

gemini-cli/           ← Gemini CLI 확장 (Extensions Gallery — 무심사)
├── gemini-extension.json  # MCP 자동 등록 + GEMINI.md 컨텍스트
├── GEMINI.md
└── commands/*.toml   # /connect·deploy·logs

openclaw/             ← OpenClaw 스킬 (ClawHub — 무심사)
└── skills/aispace/SKILL.md (+AGENTS.md)   # 헤드리스 인증 절차 포함

cursor/               ← Cursor 플러그인 (마켓 심사형)
├── .cursor-plugin/plugin.json  ⚠️ 스키마 검증 필요
├── mcp.json · rules/aispace.md · AGENTS.md

grok-build/           ← Grok Build 플러그인 (마켓 PR형)
├── .grok-plugin/plugin.json  ⚠️ 스키마 검증 필요
├── .mcp.json · skills/aispace/SKILL.md · AGENTS.md

kimi-code/            ← Kimi Code (자체 카탈로그 우회)
├── marketplace.json  # KIMI_CODE_PLUGIN_MARKETPLACE_URL용 자체 카탈로그
└── plugin/AGENTS.md

antigravity/          ← Antigravity CLI 네이티브 플러그인 (agy plugin install)
├── plugin.json · mcp_config.json · AGENTS.md · skills/

cline/                ← Cline MCP Marketplace 제출물
└── llms-install.md   # Cline이 스스로 설치하는 문서 (제출 필수물)

chat-kit/             ← 챗 클라이언트(ChatGPT·Claude 웹) 폴백 = 기존 aispace-kit.zip (원본 참조 보관)
```

## 채널별 배포 방법 (서드파티_마켓플레이스_조사_2026-08-04.md 근거)

| 채널 | 배포 절차 | 상태 |
|---|---|---|
| **Claude Code** | 이 repo를 GitHub 공개(`cafe24-aispace/aispace-plugins`) → 사용자: `/plugin marketplace add cafe24-aispace/aispace-plugins` → `/plugin install aispace`. 기존 `aispace-claude-plugin`과의 통합/대체 결정 필요 | 즉시 가능 |
| **Gemini CLI** | gemini-cli/를 **별도 공개 repo로 분리**(갤러리 요건: gemini-extension.json이 repo 루트) → repo topic에 `gemini-cli-extension` 추가 → 크롤러가 매일 수집, 검증 통과 시 **자동 등재(신청 절차 없음)**. 사용자: `gemini extensions install <repo URL>`. 설치 경로 4종: Git repo / GitHub Releases 아카이브(플랫폼별 바이너리 가능) / 로컬 경로(zip 배포 우회로) / link(개발용). 프라이빗 repo 미지원 — 원격 소스는 공개 GitHub뿐 | 무신청·무심사 |
| **ClawHub** | `clawhub skill publish ./openclaw/skills/aispace` | 무심사 |
| **skills.sh** | repo 루트에 skills/ 구조로 core/SKILL.md 배치 → `npx skills add cafe24-aispace/aispace-plugins` | 무심사 |
| **Cline** | github.com/cline/mcp-marketplace에 이슈 제출: repo URL + 로고 400×400 PNG + cline/llms-install.md. 사전에 "Cline에게 llms-install.md만 주고 셀프 설치" 테스트 | 이슈 제출 |
| **Grok Build** | xai-org/plugin-marketplace에 PR: marketplace.json 엔트리 + 커밋 SHA 고정 + CI 통과 | PR 제출 |
| **Cursor** | cursor.com/marketplace/publish 제출 (법인 심사) — 사전에 `review-plugin-submission` 검증 | 심사형 |
| **Kimi Code** | ① 가이드에 URL 설치 안내(`/plugins install <repo URL>`) ② kimi-code/marketplace.json을 docs 사이트에 호스팅해 `KIMI_CODE_PLUGIN_MARKETPLACE_URL` 안내 ③ Moonshot 접촉해 카탈로그 진입 | 우회로 즉시 |
| **Copilot** | GitHub Marketplace — Verified Publisher 인증 선행 (사내 협의) | 중기 |

## 유지보수 규칙

1. **정본은 core/AGENTS.md 하나** — 수정 시 각 패키지의 AGENTS.md/GEMINI.md로 복사(빌드 스크립트화 예정). 채널별 사본을 직접 고치지 말 것.
2. aispace-kit.zip(챗 클라이언트 배포본)과 core/AGENTS.md는 **같은 정본을 공유** — 어느 쪽을 고치든 동기화.
3. 버전은 semver — 전 채널 동일 버전으로 릴리스.

## 기존 라이브 플러그인과의 관계 (2026-08-04 확인)

`cafe24-aispace/aispace-claude-plugin`은 **이미 라이브** (21커밋, 스킬 5종: deploy/status/env/backup/github-connect + rules/, 마켓명 `cafe24-aispace-plugins`, 플러그인명 `cafe24-aispace`).
- 이 모노레포의 claude-code/는 라이브 네이밍에 **정합 완료** (plugin `cafe24-aispace` v1.1.0, marketplace `cafe24-aispace-plugins`).
- **병합 방향**: 기존 스킬 5종은 유지하고, 이 패키지의 AGENTS.md(운영 지침 전문)·connect/logs 커맨드(온보딩·실패 진단)를 **추가**하는 v1.1 업데이트로 배포 — 기존 사용자 `/plugin update`로 무중단 수신.

## 출시 전 체크리스트

- [ ] GitHub org/repo 확정 (`cafe24-aispace/aispace-plugins` — 기존 aispace-claude-plugin과 관계 정리)
- [ ] Gemini용 별도 repo 분리 (`aispace-gemini` — 갤러리 크롤러가 repo 루트의 gemini-extension.json만 인식) + topic `gemini-cli-extension` 태그
- [ ] Cursor plugin.json 스키마 검증 (`create-plugin` 스캐폴더 대조)
- [ ] Grok plugin.json 스키마 검증 (marketplace 내 Vercel 플러그인 구조 대조)
- [ ] Kimi plugin 구조 검증 (플러그인 포맷 문서 대조)
- [ ] 로고 제작 (Cline 400×400 PNG, 각 마켓 아이콘)
- [ ] Cline 셀프 설치 테스트 (llms-install.md만으로)
- [ ] 각 채널 실기기 완주 QA (클라이언트×패키지 매트릭스 — 1차: Claude Code·Gemini CLI·OpenClaw)
- [ ] 경유 측정: 문서·가이드 내 가입 링크에 채널별 식별 파라미터 부여 (KPI: 채널 경유 가입→배포→유료)
- [ ] 대외비 점검: 패키지에 내부 IP·DB 정보 미포함 확인 (완료 — 공개 엔드포인트만 사용)
