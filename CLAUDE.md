# Claude Code — 전문가 레퍼런스 워크스페이스

> 마지막 업데이트: 2026-08-31

이 디렉토리는 Claude Code의 기능 연구, 하네스 감사, 설정 실험을 위한 레퍼런스 공간입니다.

## 목적

- Claude Code 2026 최신 기능 정리 및 학습
- 하네스(Hooks, MCP, Agents, Skills) 설정 감사 및 개선안 도출
- 브레인스토밍 기반 설정 최적화

---

## Claude Code 2026 — 핵심 기능 맵

### 모델 선택 전략

| 모델 | ID | 용도 |
|------|----|------|
| Opus 4.7 | `claude-opus-4-7` | 복잡한 설계·심층 추론 |
| Sonnet 4.6 | `claude-sonnet-4-6` | 기본 개발 작업 (기본값) |
| Haiku 4.5 | `claude-haiku-4-5-20251001` | 경량 에이전트·빈번한 호출 (3배 비용 절감) |

Fast Mode: `/fast` 토글 — Opus 기반 빠른 출력 (다운그레이드 아님).

### Hooks 시스템

```
SessionStart   → 초기화 (환경변수, 상태 복구)
PreToolUse     → 도구 실행 전 (검증, 차단, 파라미터 수정)
PostToolUse    → 도구 실행 후 (자동 포맷, 린트, 품질 체크)
Stop           → 세션 종료 시 (빌드 검증, 비용 집계, 알림)
```

### 에이전트 시스템

- **서브에이전트**: 별도 컨텍스트 윈도우에서 독립 실행
- **병렬 실행**: 독립 작업은 동시 실행 (Agent tool, 단일 메시지)
- **워크트리 격리**: `isolation: "worktree"` 옵션으로 git worktree 분리
- **GAN 하네스**: Planner → Generator → Evaluator 반복 루프

### MCP 통합

| 서버 | 용도 | 상태 |
|------|------|------|
| figma | 설계↔코드 양방향 | 자격증명 필요 |
| github | PR·이슈·코드 검색 | **토큰 미설정 시 dead** |
| playwright | E2E 테스트·브라우저 자동화 | 활성 |
| memory | 세션 간 지식 공유 | 활성 |
| context7 | 라이브러리 최신 문서 | 활성 |
| sequential-thinking | 구조적 추론 | 활성 |

### Skills / Slash Commands

- 온디맨드 로드: 필요할 때만 컨텍스트에 포함
- 위치: `~/.claude/skills/` (마크다운 파일)
- ECC 플러그인: 150+ 스킬 (`/plugin` 으로 설치)

### 메모리 시스템

| 유형 | 경로 | 로드 방식 |
|------|------|---------|
| CLAUDE.md | 프로젝트 루트 | 전체 항상 로드 |
| MEMORY.md | `~/.claude/projects/.../memory/` | 처음 200줄만 자동 로드 |
| Rules | `~/.claude/rules/` | 전체 항상 로드 |

---

## 하네스 감사 결과 (2026-05-21)

### 점수판

| 영역 | 점수 | 비고 |
|------|------|------|
| Hooks 커버리지 | 8/10 | Dart Stop hook 누락 |
| Bash 권한 | 4/10 | npm install만 허용 |
| MCP 서버 | 5/10 | 27개 중 13개 자격증명 미설정 |
| 에이전트 | 9/10 | 44개 완비 |
| Rules | 7/10 | flutter/ 디렉토리 없음 |
| Skills | 9/10 | 150개 |
| CLAUDE.md 정합성 | 6/10 | BLoC vs Riverpod 충돌 |

### 발견된 문제

#### 🔴 Critical

**1. BLoC vs Riverpod 충돌**
- `~/.claude/CLAUDE.md` → BLoC/Provider 명시
- `~/.claude/rules/dart/state-management.md` → Riverpod 전용
- Rules 우선순위가 높아 CLAUDE.md 지침이 조용히 무시됨
- **해결**: CLAUDE.md에 "BLoC/Provider 또는 Riverpod (프로젝트별 결정)" 으로 수정

**2. GitHub MCP 자격증명 미설정**
- `development-workflow.md` 필수 단계: `gh search repos/code`
- MCP 경로 완전 dead (CLI `gh` 바이너리는 별개로 작동)
- **해결**: 토큰 설정 또는 엔트리 제거

#### 🟡 High

**3. Bash 권한 과도하게 제한**
- 현재 허용: `npm install:*`, `oh-my-opencode install:*` 두 가지만
- flutter, dart, pnpm, git, tsc 모두 매번 승인 요청 발생
- **해결안**:
  ```json
  "Bash(flutter *)", "Bash(dart *)", "Bash(pnpm *)",
  "Bash(git *)", "Bash(npx *)", "Bash(tsc --noEmit*)"
  ```

**4. Dart 포맷 Hook 누락**
- `stop:format-typecheck`는 JS/TS 파일만 처리
- `.dart` 파일 편집 후 `dart format` 자동 실행 없음
- **해결**: PostToolUse에 dart format 훅 추가

**5. Next.js 전용 Rules 미정의**
- App Router, RSC, Server Actions 컨벤션 없음
- `rules/typescript/nextjs.md` 파일 신규 작성 필요

#### 🟢 Low

**6. Stop 빌드 검증 Hook 없음**
- `rules/web/hooks.md`에 `pnpm build` Stop hook 권장 명시
- 실제 `hooks.json`에 미구현

---

## 즉시 실행 체크리스트

- [ ] GitHub MCP 토큰 설정 (`~/.claude/mcp-configs/mcp-servers.json`)
- [ ] Bash 권한 확장 (`~/.claude/settings.local.json`)
- [ ] BLoC/Riverpod 충돌 해소 (`~/.claude/CLAUDE.md` 한 줄 수정)
- [ ] Dart PostToolUse 포맷 훅 추가 (`~/.claude/hooks/hooks.json`)
- [ ] Next.js rules 파일 작성 (`~/.claude/rules/typescript/nextjs.md`)
- [ ] Stop 빌드 검증 훅 추가 (`pnpm build`)

---

## 브레인스토밍 메모

### 이 워크스페이스에서 실험할 것들

1. **최적 Hooks 조합 탐색** — Dart 포맷 + Next.js 빌드 검증
2. **MCP 서버 우선순위** — 13개 미설정 서버 정리 기준 수립
3. **모델 라우팅 전략** — 작업 복잡도별 자동 모델 선택
4. **GAN 하네스 실습** — Planner/Generator/Evaluator 실제 테스트
5. **컨텍스트 비용 최적화** — Haiku 위임 가능한 작업 목록화

### 참고 경로

| 항목 | 경로 |
|------|------|
| 전역 설정 | `~/.claude/settings.json` |
| 로컬 권한 | `~/.claude/settings.local.json` |
| Hooks | `~/.claude/hooks/hooks.json` |
| MCP 서버 | `~/.claude/mcp-configs/mcp-servers.json` |
| Rules | `~/.claude/rules/` |
| 에이전트 | `~/.claude/agents/` |
| 프로젝트 메모리 | `~/.claude/projects/-Users-dana-workspaces-claude/memory/` |
