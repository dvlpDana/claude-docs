# Claude 모델 레퍼런스

> 마지막 업데이트: 2026-06-15  
> 소스: https://platform.claude.com/docs/en/about-claude/models/overview

---

## 현재 최신 모델

| 모델 | API ID | 컨텍스트 | 최대 출력 | 입력 | 출력 |
|------|--------|---------|---------|------|------|
| **Claude Fable 5** | `claude-fable-5` | 1M | 128k | 확인 필요 | 확인 필요 |
| **Claude Opus 4.8** | `claude-opus-4-8` | 1M | 128k | 확인 필요 | 확인 필요 |
| **Claude Opus 4.7** | `claude-opus-4-7` | 1M | 128k | $5/MTok | $25/MTok |
| **Claude Sonnet 4.6** | `claude-sonnet-4-6` | 1M | 64k | $3/MTok | $15/MTok |
| **Claude Haiku 4.5** | `claude-haiku-4-5-20251001` | 200k | 64k | $1/MTok | $5/MTok |

> **Claude Fable 5**: Mythos-class 모델, 역대 일반 공개 최고 성능. 1M 컨텍스트 기본 내장. (2026-06-15 기준 신규 추가)  
> **Claude Opus 4.8**: Opus 계열 최신 버전. Bedrock·Vertex·Foundry Auto Mode 지원. (2026-06-15 기준 신규 추가)

### 특징 비교

| 기능 | Fable 5 | Opus 4.8 | Opus 4.7 | Sonnet 4.6 | Haiku 4.5 |
|------|---------|---------|---------|----------|---------|
| Extended Thinking | 확인 필요 | 확인 필요 | ❌ | ✅ | ✅ |
| Adaptive Thinking | ✅ | ✅ | ✅ | ✅ | ❌ |
| Auto Mode | ✅ | ✅ | ✅ | - | - |
| 지식 컷오프 (신뢰) | 확인 필요 | 확인 필요 | 2026-01 | 2025-08 | 2025-02 |

### 플랫폼별 ID

| 플랫폼 | Fable 5 | Opus 4.7 | Sonnet 4.6 | Haiku 4.5 |
|--------|---------|---------|----------|---------|
| Claude API | `claude-fable-5` | `claude-opus-4-7` | `claude-sonnet-4-6` | `claude-haiku-4-5-20251001` |
| AWS Bedrock | 확인 필요 | `anthropic.claude-opus-4-7` | `anthropic.claude-sonnet-4-6` | `anthropic.claude-haiku-4-5-20251001-v1:0` |
| Vertex AI | 확인 필요 | `claude-opus-4-7` | `claude-sonnet-4-6` | `claude-haiku-4-5@20251001` |

---

## 레거시 모델 (사용 가능)

| 모델 | API ID | 상태 |
|------|--------|------|
| Claude Opus 4.6 | `claude-opus-4-6` | 활성 |
| Claude Sonnet 4.5 | `claude-sonnet-4-5-20250929` | 활성 |
| Claude Opus 4.5 | `claude-opus-4-5-20251101` | 활성 |
| Claude Opus 4.1 | `claude-opus-4-1-20250805` | 활성 |
| **Claude Sonnet 4** | `claude-sonnet-4-20250514` | ❌ 은퇴 (2026-06-15) |
| **Claude Opus 4** | `claude-opus-4-20250514` | ❌ 은퇴 (2026-06-15) |

---

## 특수 모델

- **Claude Mythos Preview**: Project Glasswing 방어 사이버보안 연구용, 초대 전용
- **Claude Design** (Anthropic Labs): 시각 디자인·프로토타입·슬라이드 생성

---

## Fast Mode

- Opus 4.6, Opus 4.7, Opus 4.8 지원
- 최대 2.5배 빠른 출력 토큰 생성 (프리미엄 가격)
- 파라미터: `speed: "fast"` + 헤더 `fast-mode-2026-02-01`
- 대기자 명단: https://claude.com/fast-mode
