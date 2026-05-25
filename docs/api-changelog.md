# Claude API 릴리즈 노트

> 마지막 업데이트: 2026-05-25  
> 소스: https://platform.claude.com/docs/en/release-notes/overview

---

## 2026년 5월

### 2026-05-19
- **MCP Tunnels** Research Preview — 프라이빗 네트워크 MCP 서버 연결 가능
- **Managed Agents 자체 호스팅 샌드박스** — Anthropic 외부 인프라에서 툴 실행
- Managed Agents: 활성 세션 MCP 서버·툴 설정 업데이트 지원
- Managed Agents: 100K 토큰 초과 대형 출력 → 파일 자동 스필

### 2026-05-18
- **웹 검색 툴**: SEC 파일링 데이터 지원 강화

### 2026-05-13
- **캐시 진단** (public beta): `diagnostics.previous_message_id`로 캐시 미스 원인 분석  
  헤더: `cache-diagnosis-2026-04-07`

### 2026-05-12
- **Fast Mode** → Opus 4.7 지원  
  파라미터: `speed: "fast"`, `model: "claude-opus-4-7"`, 헤더: `fast-mode-2026-02-01`

### 2026-05-11
- **Claude Platform on AWS** 출시 — AWS 청구·IAM 인증으로 Claude API 전체 기능 사용

### 2026-05-06
- **Multiagent Sessions** + **Outcomes** public beta (`managed-agents-2026-04-01`)
- Managed Agents Vault `mcp_oauth` 백그라운드 자격증명 갱신
- Managed Agents Webhooks — 세션·볼트 라이프사이클 이벤트

### Claude Code CLI (2026-05-25 싱크 기준 최신 버전)

> 소스: https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md

| 버전 | 주요 변경 |
|------|---------|
| **v2.1.150** | 내부 인프라 개선 (사용자 가시 변경 없음) |
| **v2.1.149** | `/usage` 카테고리별 한도 세분화; `/diff` 키보드 스크롤; GFM 체크박스 렌더링; Enterprise `allowAllClaudeAiMcps`; PowerShell `cd` 함수 우회 버그 수정; 다수 버그 수정 |
| **v2.1.148** | Bash 툴 exit 127 회귀 버그 수정 (2.1.147 도입) |
| **v2.1.147** | `/simplify` → `/code-review` 개명 (정확성 레벨 지정, `--comment`로 GitHub PR 인라인 댓글); 백그라운드 세션 핀 고정(`Ctrl+T`); 자동 업데이터 재시도·오류 코드 개선 |
| **v2.1.145** | `claude agents --json` 추가; OTEL 스팬 `agent_id`/`parent_agent_id`; Stop/SubagentStop 훅에 `background_tasks`·`session_crons` 필드; `/plugin` 설치 전 상세 미리 보기 |
| **v2.1.144** | `/resume` 백그라운드 세션 지원; `/model` 현재 세션만 변경(`d`로 기본값); 스타트업 타임아웃 75s → 15s |
| **v2.1.143** | 플러그인 의존성 강제(비활성화 체인 확인); `worktree.bgIsolation: "none"` 설정; PowerShell 기본 `-ExecutionPolicy Bypass` |
| **v2.1.142** | Fast Mode 기본 모델 Opus 4.6 → Opus 4.7 변경; `claude agents` 신규 플래그(`--add-dir`, `--settings`, `--mcp-config`, `--plugin-dir` 등) |
| **v2.1.141** | 훅 JSON `terminalSequence` 필드(데스크탑 알림·타이틀·벨); `claude agents --cwd`; `/feedback` 이전 세션 포함; Rewind "여기까지 요약"; 스피너 10s 경과 시 황색 |
| **v2.1.140** | Agent tool `subagent_type` 대소문자·구분자 무관 매칭; 에이전트 색상 팔레트 업데이트 |
| **v2.1.139** | **에이전트 뷰 Research Preview** (`claude agents` — 모든 세션 단일 목록); `/goal` 명령(완료 조건 기반 자동 반복); `claude plugin details <name>` |

---

## 2026년 4월

### 2026-04-30
- Sonnet 4.5·Sonnet 4 1M 컨텍스트 베타 종료 (`context-1m-2025-08-07`)

### 2026-04-24
- **Rate Limits API** — 요율 한도 프로그래밍 조회

### 2026-04-23
- **Managed Agents Memory** public beta

### 2026-04-20
- Claude Haiku 3 (`claude-3-haiku-20240307`) 은퇴

### 2026-04-16
- **Claude Opus 4.7** 출시 ($5/$25, Opus 4.6과 동일 가격)  
  ⚠️ 브레이킹 체인지 → [마이그레이션 가이드](https://platform.claude.com/docs/en/about-claude/models/migration-guide) 필수 확인
- Amazon Bedrock 전체 고객 개방 (27개 리전)

### 2026-04-14
- Sonnet 4·Opus 4 지원 종료 예고 → **2026-06-15 은퇴**

### 2026-04-09
- **Advisor Tool** public beta — 실행 모델 + 어드바이저 모델 조합  
  헤더: `advisor-tool-2026-03-01`

### 2026-04-08
- **Claude Managed Agents** public beta 출시  
  헤더: `managed-agents-2026-04-01`
- **`ant` CLI** 출시 — Claude API 커맨드라인 클라이언트

### 2026-04-07
- Claude Mythos Preview (Project Glasswing) — 방어 사이버보안 초대 전용

---

## 2026년 3월

### 2026-03-30
- Message Batches API `max_tokens` 300k로 확대 (헤더: `output-300k-2026-03-24`)

### 2026-03-18
- Models API에 `max_input_tokens`, `max_tokens`, `capabilities` 필드 추가

### 2026-03-16
- Extended Thinking `display: "omitted"` — 생각 블록 생략으로 스트리밍 속도 향상

### 2026-03-13
- **1M 컨텍스트** Opus 4.6·Sonnet 4.6 GA (베타 헤더 불필요)
- 이미지/PDF 요청당 제한: 100 → 600으로 확대

---

## 2026년 2월

### 2026-02-19
- **자동 캐싱 (Automatic Caching)** — `cache_control` 단일 필드로 자동 캐시 이동
- Claude Sonnet 3.7·Haiku 3.5 은퇴

### 2026-02-17
- **Claude Sonnet 4.6** 출시
- 코드 실행 툴: 웹 검색·웹 패치 함께 사용 시 **무료**
- 웹 검색·프로그래밍 툴 호출·코드 실행·웹 패치·툴 서치·메모리 툴 **GA**

### 2026-02-07
- **Fast Mode** Research Preview (Opus 4.6) — 최대 2.5배 빠른 출력

### 2026-02-05
- **Claude Opus 4.6** 출시 — Adaptive Thinking, Compaction API, Data Residency Controls

---

## 2026년 1월

| 날짜 | 변경사항 |
|------|---------|
| 2026-01-29 | Structured Outputs GA — `output_config.format` |
| 2026-01-12 | `console.anthropic.com` → `platform.claude.com` 리다이렉트 |
| 2026-01-05 | Claude Opus 3 은퇴 |

---

## 2025년 주요 마일스톤

| 날짜 | 이벤트 |
|------|--------|
| 2025-11-24 | Claude Opus 4.5, Effort 파라미터, 프로그래밍 툴 호출 beta |
| 2025-10-16 | Agent Skills beta (PPT/Excel/Word/PDF 관리형 스킬) |
| 2025-10-15 | Claude Haiku 4.5 출시 |
| 2025-09-29 | Claude Sonnet 4.5, Memory Tool, Context Editing beta |
| 2025-09-16 | Claude 브랜드 통합 (Anthropic Docs → Claude Docs) |
| 2025-05-22 | Claude Opus 4·Sonnet 4, Files API, Code Execution, MCP Connector beta |
