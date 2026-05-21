# Claude 모델 레퍼런스

> 마지막 업데이트: 2026-05-21  
> 소스: https://platform.claude.com/docs/en/about-claude/models/overview

---

## 현재 최신 모델

| 모델 | API ID | 컨텍스트 | 최대 출력 | 입력 | 출력 |
|------|--------|---------|---------|------|------|
| **Claude Opus 4.7** | `claude-opus-4-7` | 1M | 128k | $5/MTok | $25/MTok |
| **Claude Sonnet 4.6** | `claude-sonnet-4-6` | 1M | 64k | $3/MTok | $15/MTok |
| **Claude Haiku 4.5** | `claude-haiku-4-5-20251001` | 200k | 64k | $1/MTok | $5/MTok |

### 특징 비교

| 기능 | Opus 4.7 | Sonnet 4.6 | Haiku 4.5 |
|------|---------|----------|---------|
| Extended Thinking | ❌ | ✅ | ✅ |
| Adaptive Thinking | ✅ | ✅ | ❌ |
| 지식 컷오프 (신뢰) | 2026-01 | 2025-08 | 2025-02 |
| 학습 데이터 컷오프 | 2026-01 | 2026-01 | 2025-07 |

### 플랫폼별 ID

| 플랫폼 | Opus 4.7 | Sonnet 4.6 | Haiku 4.5 |
|--------|---------|----------|---------|
| Claude API | `claude-opus-4-7` | `claude-sonnet-4-6` | `claude-haiku-4-5-20251001` |
| AWS Bedrock | `anthropic.claude-opus-4-7` | `anthropic.claude-sonnet-4-6` | `anthropic.claude-haiku-4-5-20251001-v1:0` |
| Vertex AI | `claude-opus-4-7` | `claude-sonnet-4-6` | `claude-haiku-4-5@20251001` |

---

## 레거시 모델 (사용 가능)

| 모델 | API ID | 상태 |
|------|--------|------|
| Claude Opus 4.6 | `claude-opus-4-6` | 활성 |
| Claude Sonnet 4.5 | `claude-sonnet-4-5-20250929` | 활성 |
| Claude Opus 4.5 | `claude-opus-4-5-20251101` | 활성 |
| Claude Opus 4.1 | `claude-opus-4-1-20250805` | 활성 |
| **Claude Sonnet 4** | `claude-sonnet-4-20250514` | ⚠️ 2026-06-15 은퇴 예정 |
| **Claude Opus 4** | `claude-opus-4-20250514` | ⚠️ 2026-06-15 은퇴 예정 |

---

## 특수 모델

- **Claude Mythos Preview**: Project Glasswing 방어 사이버보안 연구용, 초대 전용
- **Claude Design** (Anthropic Labs): 시각 디자인·프로토타입·슬라이드 생성

---

## Fast Mode

- Opus 4.6, Opus 4.7 지원
- 최대 2.5배 빠른 출력 토큰 생성 (프리미엄 가격)
- 파라미터: `speed: "fast"` + 헤더 `fast-mode-2026-02-01`
- 대기자 명단: https://claude.com/fast-mode
