# Claude API 릴리즈 노트

> 마지막 업데이트: 2026-08-24  
> 소스: https://platform.claude.com/docs/en/release-notes/overview

---

## 2026년 8월

### 2026-08-20
- **Python SDK v1.0 출시** — HTTP 레이어를 `httpx` → `httpx2`(유지 관리 중인 API 호환 포크)로 전환. 주요 제거 사항: 레거시 Text Completions API, Messages 메서드의 `temperature`/`top_p`/`top_k` 파라미터, 툴 러너 클라이언트 측 `compaction_control`. Python 3.10+ 필수. async 클라이언트 `.with_raw_response` 결과 파싱에 `await response.parse()` 필요. `AnthropicBedrock` AWS 리전 미설정 시 `us-east-1` 기본값 대신 오류 반환. v1 마이그레이션 가이드 참고.

### 2026-08-19
- **컴퓨터 사용 툴 정식 출시** (`computer_toolset_20260801`) — 베타 헤더 불필요. 배치 액션(한 턴에 여러 액션), 줌 기본 활성화, `configs`로 멤버별 설정 지원. 기존 `computer_20251124` 베타와 요청 형식 변경됨 → 마이그레이션 가이드 확인 필수. Fable 5·Mythos 5·Opus 5·Sonnet 5·Opus 4.8 지원.
- **브라우저 사용 툴 출시** (`browser_toolset_20260801`) — 앱이 호스팅하는 브라우저를 구동하는 클라이언트 툴셋. 접근성 트리·엘리먼트 참조·폼 입력·탭 관리·다운로드 리포팅·파일 업로드(옵트인) 지원. Fable 5·Mythos 5·Opus 5·Sonnet 5·Opus 4.8 지원.
- **Files API 정식 출시** — `files-api-2025-04-14` 베타 헤더 불필요. 업로드 시 `expires_in_seconds` 설정, 파일 객체에 `expires_at` 포함. 목록 조회 시 페이지네이션·`ids[]` 필터 지원. 기존 베타 헤더 요청도 계속 동작.
- **Agent Skills 및 Skills API 정식 출시** — `skills-2025-10-02` 베타 헤더 불필요. Messages API `container` 파라미터로 스킬 로드 가능.
- **Admin API 사용자 관리 정식 출시** — `ce-user-management-2026-07-13` 베타 헤더 불필요 (그룹·커스텀 역할 요청 포함).
- **Managed Agents 웹 검색·패치 도메인 제한** — `allowed_domains`·`blocked_domains`로 에이전트의 `web_search`·`web_fetch` 툴 접근 사이트 제한 가능.

### Claude Code CLI (2026-08-24 싱크 기준 최신 버전)

> 소스: https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md

| 버전 | 주요 변경 |
|------|---------|
| **v2.1.241** | 버그 수정 및 안정성 개선 |
| **v2.1.240** | 버그 수정 및 안정성 개선 |
| **v2.1.239** | 비용 추정에 1.1× 미국 전용 추론 프리미엄 반영; Bedrock·Vertex·Foundry 풀스크린 렌더러 최초 제안; `/claude-api upgrade` Python 0.x → 1.x 마이그레이션; 클라우드 세션 플러그인 `@synced` 표시·관리; Alpine/musl 네이티브 이미지 붙여넣기·클립보드·오디오 애드온 지원; 다수 보안·버그 수정 |
| **v2.1.238** | `keybindingFlavor` 설정(`"readline"` 모드); 마켓플레이스·카탈로그 `headersHelper` 지원; `self-hosted-runner --defer-shutdown-max-min`·`--proxy-authorization-command/file` 플래그; 다수 버그 수정 |
| **v2.1.237** | LLM 게이트웨이·커스텀 기반 URL 프롬프트 캐싱 수정; 내장 "Concise" 출력 스타일 추가 (`/config`에서 선택) |
| **v2.1.236** | `ANTHROPIC_DEFAULT_MODEL` 환경변수(새 세션 기본 모델 설정); `notify_when_idle` 교차 세션 SendMessage 옵션(macOS·Linux); macOS 샌드박스 와일드카드 거부 규칙 강화; 다수 버그 수정 |
| **v2.1.235** | 선택적 `spellcheck` 설정(aspell·hunspell·ispell로 입력 중 오타 밑줄 표시); 다수 버그 수정 |
| **v2.1.234** | `CLAUDE_CODE_PROJECT_DIR_NAME` 환경변수; `selection:clear` 키바인딩; GitLab MR 배지(풋터·상태줄); 사용 한도 초기화 시 세션 자동 재개; 보안: 원격 파일 읽기·세션 복원·워크플로우 스크립트의 Windows NT-namespace 경로 거부(NTLM 크레덴셜 유출 방어); 다수 버그 수정 |
| **v2.1.233** | GitLab MR URL `--worktree`·`claude agents` 지원; Linux Bash 툴 메모리 cgroup 지원 (`CLAUDE_CODE_TOOL_MEMORY_LIMIT`); `CLAUDE_CODE_WEBFETCH_CACHE_TTL_MS` 환경변수; `forward_user_identity` 게이트웨이 설정; Todo/task 추적 툴 Opus 4.8·Sonnet 5·Fable 5·Mythos 5+ 기본 제거 (`CLAUDE_CODE_ENABLE_TODO_TOOLS=1`로 복원); `claude plugin validate` `.claude/skills` 디렉토리 검사; 스크린 리더 `/effort` 선택기 개선; 다수 보안·버그 수정 |
| **v2.1.232** | **서브에이전트 포킹 기본 활성화** (`subagent_type: "fork"` 전체 대화·캐시 상속); `@` 세션 멘션으로 다른 세션에 직접 `SendMessage`; 세션 고유 이름 자동 부여; GitLab 플러그인 마켓플레이스 지원; GitLab 토큰 패밀리 시크릿 리덕션; `additionalMarketplaces`·`allowedMarketplaces` 설정 별칭; Fable 5 `/advisor` 재지원; PowerShell·Windows symlink 권한 우회 수정; 중첩 git 신뢰 범위 수정; 다수 보안·버그 수정 |
| **v2.1.231** | MCP OAuth Slack 등 사전 등록 클라이언트 리다이렉트 URI 불일치 수정 |
| **v2.1.229** | 플러그인 마켓플레이스 `command` 소스 지원; 게이트웨이 SSE keepalive 핑 (Vertex·Bedrock 타임아웃 방지); `ListAgents` 오프라인·클라우드 세션 레이블 표시; `claude remote-control --continue` 문서화; 스트리밍 응답 소실·중복 출력 수정; 좁은 터미널 RangeError 크래시 수정; `/install-github-app` 리뷰 미게시 수정; 다수 버그 수정 |
| **v2.1.228** | 세션 cleanup 메모리 폴더 내용 삭제 수정; self-hosted runner checkout 훅 실패 시 건너뜀; 클라우드 세션 자격증명 격리 수정; claude.ai 싱크 스킬 보안 강화 (로컬 명령 차단·설명 정제·섀도잉 방지); Vertex AI 만료 크리덴셜 즉시 실패; 세션 간 인박스 초기화 수정; 다수 보안·버그 수정 |
| **v2.1.227** | 만료 토큰 시작 시 Max 플랜 Fable 크레딧 오인 프롬프트 수정; `claude-code-action` Bash 명령 전면 실패 수정 (`allowed_non_write_users`); `/tui` 리와인드 세션 복원 수정; 슬래시 명령 메뉴 UI 개선 (선택 행 강조·이모지·악센트 보존) |
| **v2.1.226** | 버그 수정 및 안정성 개선 |
| **v2.1.225** | 게이트웨이 지출 한도(spend-limit) 지원 — 한도 도달 메시지에 한도명·초기화 시간·운영자 메시지 표시; `claude agents` 미신뢰 디렉토리 워크스페이스 신뢰 프롬프트; MCP OAuth macOS 키체인 타임아웃 후 401 오류 수정; Auto Mode 안전 필터 거부를 연속 차단 한도에서 제외; SendMessage로 다른 기기의 Remote Control 세션에 직접 대화 시작 가능; VS Code Focus view 수정(to-do·보류 질문 접힘 방지); 다수 버그 수정 |
| **v2.1.224** | **`claude self-hosted-runner`** — 직접 기계/컨테이너를 Claude Code 실행 환경으로 전환 (Team/Enterprise 플랜); `archive` 플러그인 소스 — HTTPS zip 설치·SHA-256 핀 지원; `ANTHROPIC_BEDROCK_REGION_PREFIX` 환경변수; `crossSessionInbound`·`dialogExpiry` 설정; 교차 세션 `SendMessage` GA (macOS·Linux); 샌드박스 크리덴셜 마스킹(`decode: "jwt"`, `awsPairs/sigv4`); 다수 보안·버그 수정 |
| **v2.1.223** | `strictKnownMarketplaces`·`blockedMarketplaces`에 소유자 와일드카드(`"owner/*"`) 지원; 제한 모델 서브에이전트 시 상위 모델 실행 경고; `/teleport` 힌트(클라우드→로컬 전환); Bash 권한 우회(제작 명령·탭/불가시 유니코드 숨김) 수정; 워크플로우 동적 `import()` 샌드박스 우회 수정; `bypassPermissions` 모드 조직 정책 우회 수정; 다수 버그 수정 |
| **v2.1.222** | 워크트리 격리 서브에이전트의 주 체크아웃 파괴적 git 명령 차단; PreToolUse 자동 허용 훅이 배경 에이전트 도구 제한 우회하던 수정; HTTPS 프록시 뒤 시작 연결 확인 중단 수정; Auto Mode 안전성: `SendMessage` 메시지 권한 분류기 평가 후 전달; 다수 버그 수정 |
| **v2.1.221** | [VSCode] **Focus 뷰** — 도구 활동을 턴별 확장 요약으로 숨김 (`Ctrl+Alt+F`); Linux·WSL 샌드박스 크리덴셜 `mode: "mask"` 지원; `claude plugin validate` 마켓플레이스 이름 호환성 경고; `claude-api` 스킬 `prompt-audit` 서브커맨드; Bash 권한 우회(zsh `[[ ]]` 정규식 조건) 수정; Vertex AI Claude 4.5+ 도구 검색 재활성화; 다수 버그 수정 |

---

## 2026년 7월

### 2026-07-15
- **미드-대화 시스템 메시지 Claude Fable 5·Mythos 5·Opus 4.8 지원** — Claude API, Amazon Bedrock, Google Cloud에서 베타 헤더 없이 사용 가능. 기존 가용성 안내 오류 정정.

### 2026-07-14
- **Claude Enterprise 사용자 관리 Admin API (베타)** — 전체 Claude Enterprise 조직 대상 베타 공개. 멤버 목록 조회·이메일 검색·역할 변경·멤버 제거·초대 발송·취소, 그룹·멤버십 관리, 커스텀 역할 조회 지원. 그룹·커스텀 역할 요청: 헤더 `anthropic-beta: ce-user-management-2026-07-13` 필요. `read:org_audit` 스코프 Admin API 키로 GET 엔드포인트 전체 접근 가능.

### 2026-07-10
- **Access Transparency 문서 확장** — `cmek_preserve` 이벤트에 필터 예시·이벤트 페이로드·보존 사유 코드 2개(`policy_violation_investigation`, `csae_report`) 추가. 보존 이벤트는 사람 검토자·자동 안전 파이프라인 어느 쪽에서 시작하든 기록됨을 명시.

### 2026-07-08
- **API 키 만료일 설정 지원** — Console에서 API 키·Admin API 키 생성 시 만료 기간 지정 가능(사전 설정·커스텀·무기한). 7일 이상 키는 만료 전 이메일 알림. Admin API `expires_at` 필드로 조회. 기존 키 영향 없음.

### 2026-07-02
- **`agent-memory-2026-07-22` 베타 헤더 추가** — 메모리 조회(`GET /v1/memory_stores/{id}/memories`) 동작 변경: 안정적 서버 정렬 순서, `depth` 0·1·미제공만 허용, `path_prefix` 경로 세그먼트 완전 일치. 기존 커서 재사용 불가(첫 페이지부터 재시작 필요). 2026-07-22부터 `managed-agents-2026-04-01` 헤더도 동일 동작 적용; 양 헤더 동시 사용 시 400 오류. SDK 일괄 업데이트(Python 0.116.0, TS 0.110.0, Go 1.56.0, Java 2.48.0, Ruby 1.55.0, PHP 0.36.0, C# 12.35.0, CLI 1.16.0).

### 2026-07-01
- **Claude Fable 5·Claude Mythos 5 접근 복구** — 서비스 중단 이후 재배포 완료. [Anthropic 성명](https://www.anthropic.com/news/redeploying-fable-5-mythos-5) 참고

### Claude Code CLI (2026-07-27 싱크 기준 최신 버전)

> 소스: https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md

| 버전 | 주요 변경 |
|------|---------|
| **v2.1.220** | 버그 수정 및 안정성 개선 |
| **v2.1.219** | **Claude Opus 5** (`claude-opus-5`) 출시 — 새 기본 Opus 모델, 1M 컨텍스트, Fast Mode $10/$50/MTok; `sandbox.network.strictAllowlist` 설정; `DirectoryAdded` 훅; 중첩 서브에이전트 depth 3 기본 허용; Opus 4.7 Fast Mode 제거; `workflowSizeGuideline` 설정 키; 다수 버그 수정 |
| **v2.1.218** | `/code-review` 배경 서브에이전트 실행 전환; `/deep-research` 수동 호출 전환; Auto Mode 위험 명령(rm/`&` 등) 자동 분류; 에이전트 이름 `:` 포함 금지; `skills context: fork` 기본 배경 실행; 다수 안정성 수정 |
| **v2.1.217** | 이모지 단축 코드 자동완성(`:heart:` → ❤️); 동시 서브에이전트 캡 20개 기본(`CLAUDE_CODE_MAX_CONCURRENT_SUBAGENTS`); 서브에이전트 중첩 기본 비활성화; 트랜스크립트 쓰기 실패 경고; 다수 버그 수정 |
| **v2.1.216** | `sandbox.filesystem.disabled` 설정; 긴 세션 메시지 정규화 성능 회귀 수정; worktree 격리 서브에이전트 git 리다이렉션 차단; `/context` 컨텍스트 초과 경고; 다수 버그 수정 |
| **v2.1.215** | `/verify`·`/code-review` 스킬 더 이상 자동 실행 안 함 — `/verify` 또는 `/code-review` 직접 호출 필요 |
| **v2.1.214** | 권한 체크 다수 보안 강화(`dir/**` 자동 승인 오류·PowerShell 5.1 우회·10,000자 초과 명령·zsh 변수 구문); **EndConversation 툴** 추가(남용 사용자 세션 종료 가능); 장시간 툴 호출 주기적 진행 하트비트; 메모리 파일 프론트매터에 ISO `modified` 타임스탬프; OTel 이벤트 `message.uuid`·`client_request_id`·`tool_source` 속성; Docker 데몬 리다이렉트 플래그 권한 프롬프트 추가; 다수 버그·메모리 수정 |
| **v2.1.212** | **`/fork`** 대화를 새 배경 세션으로 복사(기존 인-세션 서브에이전트 → **`/subtask`**); `claude auto-mode reset`; WebSearch 세션당 최대 200회 캡(`CLAUDE_CODE_MAX_WEB_SEARCHES_PER_SESSION`); 서브에이전트 최대 200개 캡(`CLAUDE_CODE_MAX_SUBAGENTS_PER_SESSION`); MCP 툴 2분 초과 시 배경 자동 이동; `/resume` 과거 세션 목록 피커; 다수 버그 수정 |
| **v2.1.211** | `--forward-subagent-text` 플래그·환경변수(서브에이전트 텍스트·싱킹 stream-json 포함); 권한 미리보기 양방향 오버라이드·영너비 문자 무력화; PreToolUse hook `ask`가 Auto Mode를 재정의하도록 수정; 플러그인 MCP 아이들 복귀 후 재연결 수정; 서브에이전트 모델 오버라이드 유지 수정; 다수 버그 수정 |
| **v2.1.210** | 접힌 툴 요약 라인에 실시간 경과시간 카운터; `Write(path)`·`NotebookEdit(path)`·`Glob(path)` 권한 규칙 시작 경고 추가; worktree 격리 서브에이전트 주 repo git-mutating 명령 차단 수정; `ultracode` 비사람 입력(웹훅 페이로드 등) 발동 수정; 성능 개선(파일 편집 읽기 캐시 16 MB 한도·세션 트랜스크립트 크기 최대 79배 절감·MCP 도구 라운드 최대 7배 가속) |
| **v2.1.209** | `claude agents` 배경 세션에서 `/model` 등 다이얼로그 차단 수정 (2.1.208 과도한 가드 회귀 수정) |
| **v2.1.208** | **스크린 리더 모드** 추가(`--ax-screen-reader` / `CLAUDE_AX_SCREEN_READER=1` / `"axScreenReader": true`); `vimInsertModeRemaps` 설정(삽입 모드 두 키 시퀀스 매핑); `CLAUDE_CODE_PROCESS_WRAPPER`(기업 래퍼 실행 파일 지원); 멀티셀렉트·입력 행 마우스 클릭 지원; 다수 버그 수정 |
| **v2.1.207** | Auto Mode Bedrock·Vertex·Foundry GA(`disableAutoMode` 설정으로 비활성화); 긴 목록·표 스트리밍 중 터미널 프리즈·키 지연 수정; 비대화형 실행 시 원격 관리 설정 미동의 자동 기록 수정; 플러그인 훅 `${user_config.*}` 쉘 인젝션 차단(exec 형식 사용 권고); 플러그인 옵션 프로젝트 `.claude/settings.json` 읽기 금지(사용자·관리·`--settings` 설정만 허용); `/usage-credits` 잘못된 금액 입력 거부·$1,000 초과 시 타이핑 확인 등 다수 수정 |
| **v2.1.206** | `/cd` 디렉토리 경로 제안; `/doctor` 불필요 CLAUDE.md 콘텐츠 정리 제안; `/commit-push-pr` 설정된 push 원격지 자동 허용; Gateway `/login` 공개 게이트웨이 지원; `EnterWorktree` 프로젝트 외부 워크트리 진입 시 확인 프롬프트; 배경 에이전트 버전 업데이트 세션 어태치 전 사전 처리; 다수 버그 수정 |
| **v2.1.205** | Auto Mode 세션 트랜스크립트 파일 변조 차단 규칙 추가; `--json-schema` 유효하지 않은 스키마 미구조화 출력 방지; max-turns 한도 도달 시 미전송 메시지 유실 수정; Windows 워크트리 삭제 시 NTFS 정션 외부 파일 삭제 방지; 서브에이전트 `SendMessage` 재개 후 실패/완료 상태 유지 수정 등 다수 |
| **v2.1.204** | SessionStart 훅 실행 중 비대화형 세션 훅 이벤트 스트리밍 미전송 수정 (원격 워커 유휴 회수 방지) |
| **v2.1.203** | 로그인 만료 전 경고 추가; 수동 권한 모드 시 푸터 회색 ⏸ 배지 표시; MCP `roots/list` 추가 작업 디렉토리 포함; macOS 저메모리 오탐으로 인한 배경 에이전트 세션 전환 15-20초 지연 수정; 배경 에이전트 데몬 토큰 만료 시 자동 복구; 컨텍스트 사용량 지표 매 턴 전체 분석 CPU·메모리 회귀 수정 등 다수 |
| **v2.1.202** | `/config` 동적 워크플로우 크기 설정(small/medium/large 에이전트 수 지침); 워크플로우 에이전트 OTel `workflow.run_id`·`workflow.name` 속성 추가; Remote Control 명령 전송 실패 수정; 캡션 없는 이미지·파일 RC 앱 전송 시 유실 수정; 다수 버그 수정 |
| **v2.1.201** | Claude Sonnet 5 세션 미드-대화 시스템 역할 하네스 리마인더 제거 |
| **v2.1.200** | `AskUserQuestion` 대화 자동 진행 기본 비활성화(→ `/config`에서 옵트인); 기본 권한 모드 `"default"` → `"manual"` 전환(CLI·VS Code·JetBrains 전체); 백그라운드 에이전트 데몬 핸드오버·스레드 복수 버그 수정; 스크린 리더 출력 개선 |
| **v2.1.199** | `/skill-a /skill-b` 중첩 슬래시 스킬 최대 5개 동시 로드; TLS 검사 프록시·SSL 오류 즉시 실패(리트라이 낭비 방지); 부분 응답 미드스트림 오버로드 보존; 백그라운드 에이전트 Linux 데몬 50초 자살 버그 수정 등 다수 |
| **v2.1.198** | 서브에이전트 백그라운드 기본 실행(GA); **Claude in Chrome** 일반 공개; 백그라운드 에이전트 알림 훅 (`agent_needs_input`/`agent_completed`); `/dataviz` 내장 스킬 추가; Gateway에 Claude Platform on AWS 업스트림 추가; 탐색(Explore) 에이전트 모델 Haiku → Opus 상속 |
| **v2.1.197** | **Claude Sonnet 5** Claude Code 기본 모델로 설정; 1M 컨텍스트 네이티브 지원; 프로모션 가격 $2/$10/MTok (2026-08-31까지) |
| **v2.1.196** | 조직 기본 모델 지원(관리자가 Console에서 설정); 세션 시작 시 읽기 쉬운 기본 이름 생성; 채팅 파일 첨부 클릭 공개(Finder/Explorer); `claude mcp list/get` 비승인 워크스페이스 서버 노출 보안 수정 |

---

## 2026년 6월

### 2026-06-30
- **Claude Sonnet 5** (`claude-sonnet-5`) 출시 — 소개 가격 $2/$10/MTok (2026-08-31까지, 이후 $3/$15). 1M 컨텍스트, 128k 최대 출력. Adaptive Thinking 기본 활성화. 수동 Extended Thinking 제거(→ 400 오류). `temperature`/`top_p`/`top_k` 비기본값 설정 시 400 오류. 신규 토크나이저(동일 텍스트 대비 약 30% 더 많은 토큰 생성). Priority Tier 미지원.

### Claude Code CLI (2026-06-29 싱크 기준 최신 버전)

> 소스: https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md

| 버전 | 주요 변경 |
|------|---------|
| **v2.1.195** | `CLAUDE_CODE_DISABLE_MOUSE_CLICKS` 설정(전체화면 마우스 클릭·드래그 비활성화); 하이픈 포함 훅 매처 정확한 매칭 수정(기존 서브스트링 매칭 → 정확한 일치, 와일드카드는 `mcp__brave-search__.*` 사용); voice 딕테이션 공백 없는 언어(일본어·중국어·태국어) 자동 제출 수정; 플러그인 설치 동의 경로 강화; 백그라운드 에이전트 소켓·재시작·영구 stop 다수 수정 |
| **v2.1.193** | `autoMode.classifyAllShell` 설정(모든 Bash/PowerShell 자동분류); Auto Mode 거부 사유 트랜스크립트·토스트·`/permissions` 기록; `claude_code.assistant_response` OpenTelemetry 로그 이벤트(`OTEL_LOG_ASSISTANT_RESPONSES=0`으로 비활성화); bash 모드(`!`) 파일경로 라이브 자동완성; MCP 인증 필요 서버 시작 알림; 백그라운드 쉘 아이들 메모리 압박 자동 해제 |
| **v2.1.191** | `/rewind` 명령으로 `/clear` 이전 대화 복원; 스트리밍 중 스크롤 위치 점프 수정; 백그라운드 에이전트 stop 후 재생성 버그 영구 수정; MCP OAuth 재시도·에러메시지·헤더 헬퍼 재인증 개선; CPU 사용량 ~37% 절감(텍스트 업데이트 100ms 코얼레싱) |
| **v2.1.190** | 버그 수정 및 안정성 개선 |
| **v2.1.187** | `sandbox.credentials` 설정(자격증명 파일·비밀 환경변수 샌드박스 차단); 조직 모델 제한을 피커·`--model`·`/model`·`ANTHROPIC_MODEL`에 반영; `--json-schema`·Workflow `agent({schema})` 구조화 출력 무한 재호출 수정; 원격 MCP 5분 무응답 시 오류 반환(`CLAUDE_CODE_MCP_TOOL_IDLE_TIMEOUT`으로 조정 가능) |
| **v2.1.186** | `claude mcp login/logout <name>` CLI 인증(SSH `--no-browser` 지원); `/workflows` 상태 필터(`f` 키); `/plugin` 설치 탭 Skills 섹션 추가; `teammateMode: "iterm2"` 설정; `!` bash 출력 자동 응답 기본 활성화(`respondToBashCommands: false`로 비활성화 가능); 마켓플레이스 `renames` 맵 자동 적용 |

### 2026-06-26
- **API Rate Limits 대폭 인상** — Claude Sonnet·Haiku 요율 한도를 Claude Opus 수준으로 통일. 사용 티어 Start·Build·Scale 3단계로 통합. 기존 대비 하향 없음, 별도 조치 불필요. Console `/settings/limits`에서 확인 가능

### 2026-06-25
- **Fast Mode: Opus 4.7 지원 종료 예고** — 2026-07-24 완전 제거 예정. 이후 `claude-opus-4-7` + `speed: "fast"` 요청 시 오류 반환. **Opus 4.8 Fast Mode로 마이그레이션 필요**

### 2026-06-18
- **SDK 업데이트** (Python·TypeScript·Go·Java·Ruby·PHP·C#): `code_execution_20260120` 코드 실행 툴 타입 지원 추가 — REPL 상태 지속 + 프로그래밍 툴 호출 최소 버전. 베타 헤더 불필요. Fable 5·Mythos 5·Opus 4.5+·Sonnet 4.5+ 지원

### Claude Code CLI (2026-06-22 싱크 기준 최신 버전)

> 소스: https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md

| 버전 | 주요 변경 |
|------|---------|
| **v2.1.185** | 스트림 스톨 힌트 문구 개선 ("Waiting for API response · will retry in …"), 트리거 타임아웃 10s → 20s |
| **v2.1.183** | Auto Mode 안전성 강화(파괴적 git 명령 자동 차단·amend 제한·terraform/pulumi/cdk destroy 차단); 사용 중단 모델 경고 추가; `attribution.sessionUrl` 설정; `/config --help`; 다수 버그 수정 |
| **v2.1.181** | `/config key=value` 프롬프트 내 설정 직접 변경; `sandbox.allowAppleEvents` 설정(macOS); `CLAUDE_CLIENT_PRESENCE_FILE` 모바일 알림 억제; Bun 1.4 업그레이드; 프롬프트 캐싱 Foundry 수정; 다수 버그 수정 |
| **v2.1.179** | 미드스트림 연결 끊김 시 부분 응답 보존; WSL2 마우스 휠 수정(2.1.172 회귀); 서브에이전트 트랜스크립트 표시 수정; 다수 버그 수정 |
| **v2.1.178** | 에이전트 팀 단순화(`TeamCreate`/`TeamDelete` 제거 → 암묵적 팀); `Tool(param:value)` 권한 규칙 구문; 중첩 `.claude/skills` 네임스페이스(`<dir>:<name>`); Auto Mode 서브에이전트 사전 분류; `/bug` 설명 필수화; 다수 버그 수정 |

### 2026-06-15
- **Claude Sonnet 4 (`claude-sonnet-4-20250514`) 공식 은퇴** — 2026-04-14 예고 기준 예정대로 지원 종료
- **Claude Opus 4 (`claude-opus-4-20250514`) 공식 은퇴** — 동일 일정으로 지원 종료

### Claude Code CLI (2026-06-15 싱크 기준 최신 버전)

> 소스: https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md

| 버전 | 주요 변경 |
|------|---------|
| **v2.1.176** | 세션 제목 대화 언어 자동 생성; `footerLinksRegexes` 설정; Bedrock 자격증명 캐싱 개선; hook `if` 경로 패턴 수정; Remote Control 다수 버그 수정 |
| **v2.1.175** | `enforceAvailableModels` 관리형 설정 — `availableModels` 허용 목록이 Default 모델도 제한 |
| **v2.1.174** | `wheelScrollAccelerationEnabled` 설정; `/model` 피커 Fable 5·Opus 별도 행 표시; VSCode Usage 대화상자 세분화; Bedrock GovCloud 리전 수정 |
| **v2.1.173** | Fable 5 모델 ID의 `[1m]` 접미사 자동 제거 (기본 1M 컨텍스트이므로 불필요) |
| **v2.1.172** | 서브에이전트 5단계 재귀 지원; Bedrock `~/.aws` 설정 리전 자동 읽기; 플러그인 검색 바; WebFetch 도메인 와일드카드 규칙 수정 |
| **v2.1.170** | **Claude Fable 5 출시** — Mythos-class, 역대 일반 공개 최고 성능; `https://www.anthropic.com/news/claude-fable-5-mythos-5` |
| **v2.1.169** | `--safe-mode` 플래그 (모든 커스터마이제이션 비활성화); `/cd` 명령 (캐시 유지 디렉토리 이동); `disableBundledSkills` 설정; 자체 호스팅 `post-session` 훅 |
| **v2.1.168** | 버그 수정 및 안정성 개선 |
| **v2.1.167** | 버그 수정 및 안정성 개선 |
| **v2.1.166** | `fallbackModel` 설정(최대 3개 순차 폴백); 부정 규칙 글로브 패턴 지원(`"*"` → 모든 툴 차단); 교차 세션 메시지 권한 보안 강화; `MAX_THINKING_TOKENS=0` 지원 |
| **v2.1.165** | 버그 수정 및 안정성 개선 |
| **v2.1.163** | `requiredMinimumVersion`/`requiredMaximumVersion` 관리형 설정; `/plugin list` 명령; Stop/SubagentStop 훅 `additionalContext` 반환 지원 |
| **v2.1.162** | `claude agents --json` `waitingFor` 필드; Remote Control 풋터 고정 알약 표시; Windsurf → Devin Desktop 리브랜드 반영 |
| **v2.1.161** | `OTEL_RESOURCE_ATTRIBUTES` 값을 메트릭 레이블로 포함; 병렬 툴 호출 실패 시 독립 결과 반환 |
| **v2.1.160** | 쉘 스타트업 파일 쓰기 전 확인 프롬프트; 동적 워크플로우 키워드 `workflow` → `ultracode` 변경 |
| **v2.1.159** | 내부 인프라 개선 (사용자 가시 변경 없음) |
| **v2.1.158** | Bedrock·Vertex·Foundry Auto Mode — Opus 4.7·Opus 4.8 대상 (`CLAUDE_CODE_ENABLE_AUTO_MODE=1`) |
| **v2.1.157** | `.claude/skills` 플러그인 자동 로드 (마켓플레이스 불필요); `claude plugin init <name>` 스캐폴딩; `EnterWorktree` 세션 간 전환 지원 |

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
