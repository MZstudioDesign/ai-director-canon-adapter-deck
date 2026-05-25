---
title: 아마존 웨비나 발표 (인비저블웍스 / 캐논·어댑터·콘솔 시스템 공유)
date: 2026-05-06 23:00
duration: 30분 (QnA 별도, 발표 외부)
audience: 한국인 아마존 셀러 약 10명
speaker_position: 디자인 마케터 + AI 전문가 (인비저블웍스 운영자)
tone: 테스트 리포트 / 연구 과정 + 정보 공유 (확정 시스템 시연 X)
core_message: AI에게 배경지식(=캐논)을 깔아주면 결과가 잘 나온다. 그 정보 setup이 전문가의 일.
status: SKELETON (내용 슬롯 + 스타일 먼저, 콘텐츠 추후 흘려넣음)
---

# 발표 척추 — 7단 (총 30분)

## 슬롯 1. 인트로 + 페인 (3분)

**메시지**: "안녕하세요, 인비저블웍스 운영자입니다. 저는 AI로 카드뉴스·광고소재·웹사이트 만드는 일을 하면서 매번 똑같은 페인을 겪었어요 — **모델 변동성**, **결과가 막 나옴**, **재현 안 됨**."

**자산**:
- 발표자 한 줄 소개 (디자인 마케터 + AI 전문가)
- 페인 3개 (모델 변동성 / 결과 막 나옴 / 재현 X) — 텍스트 슬라이드 1장
- (선택) 어제 포스터 작업 9단계 = "이게 현재 프로의 실태" 한 컷

**슬롯 상태**: 텍스트만 — 즉시 작성 가능

---

## 슬롯 2. 시스템 한 장 (4분)

**메시지**: "그래서 저는 이걸 **캐논·어댑터·콘솔** 구조로 다시 짜는 중. 디렉터 = 나, AI = 스태프."

**자산**:
- 다이어그램 1장 — 3층 (캐논 = 본질·불변 / 어댑터 = 모델 호출 / 콘솔 = 디렉터 UI)
- DDD 매핑 (Domain / App+Infra / Presentation)
- 핵심 한 줄: "시대·모델 변해도 안 바뀌는 본질 = 캐논"

**자료 출처**:
- `0-공통-도메인/decisions/2026-05-04-architecture-directors-console.md` (Naming convention 섹션)
- `0-공통-도메인/q7-session-handoff.md` §2

**슬롯 상태**: 다이어그램 신규 제작 (web-ppt 스킬에서 SVG 또는 CSS)

---

## 슬롯 3. 캐논(배경지식) 깊이 — **메인 슬롯** (9분)

**메시지**: "AI에게 이런 거 다 inject하면 갑자기 잘함. 이게 진짜 일."

**자산** (각 30초 ~ 1분씩 빠르게 훑기):
1. **Nielsen UX Heuristics 10** (`canon/ux/02-laws-of-ux.md`)
2. **AIDA + Copy Laws** (`canon/copy/01-ogilvy-headline-rules.md`)
3. **Schwartz 5 Awareness Levels** (`canon/psychology/02-schwartz-awareness.md`)
4. **JTBD + Five Marketing Angles** (`canon/psychology/03-jtbd-four-forces.md`)
5. **Stories That Stick — 4 요소** (`canon/story/01-stories-that-stick.md`)
6. **Cialdini 6 Influence** (`canon/psychology/04-cialdini-influence.md`)
7. **Rams 10 / Grid Systems / Typography** (`canon/visual-design/`)
8. **Amazon Listing 딥어댑터** (`deep-adapters/marketing/17-amazon-listing-and-aplus.md`) — 7 필드 / Title 룰 / Bullet 5 룰 / A+ 7모듈 / A9 알고리즘
9. **Cross-border ecom Master** (`deep-adapters/marketing/18-cross-border-ecom-master.md`)
10. **그래프 시각화** (`graphify-out/graph.html`) — "이게 제 지식 구조 74노드 9커뮤니티"

**자료 출처**: 위 파일들 직접 발췌 (캡처 또는 텍스트)

**[트랙 A 추가 자료 슬롯]**: 트랙 A 진행되면서 새 캐논 파일 박힐 때마다 여기 추가
**[트랙 A 추가 자료 슬롯]**: ─
**[트랙 A 추가 자료 슬롯]**: ─

**슬롯 상태**: 자료 발췌 + 시각화 필요. 그래프 html은 그대로 임베드 가능

---

## 슬롯 4. 모델 매트릭스 (4분)

**메시지**: "이 시스템 안에서 모델은 swappable. 그동안 써본 결과 — "

**자산** (표 1장):

| 작업 | 픽한 모델 | 한 줄 |
|---|---|---|
| 시장조사·페인포인트 | Gemini 3.1 Pro CLI | 결과가 그냥 잘 나옴 |
| 회의·토론 (방향 잡기) | Claude Opus 4.7 | 일반적으로 Opus가 좋음 |
| 카피 (한국어, vertical 무관) | Opus + Codex 순차 | 사용자 픽 14/14 |
| 이미지 생성 (한국어 텍스트) | Codex `gpt-image-2` | duct tape인 GPT가 단연 1등 |
| 영구 탈락 | Sonnet (카피), Gemini (카피) | 결과로 충분 |

**발견 일화 (선택, 셀러 임팩트용)**:
- Sonnet 한국어 카피 무너짐 — 4모델 40카피 비교에서 사용자 픽 14개 모두 Opus
- Codex 이미지 1장 = Plus 한도 3-5x 소진 (실무 비용 감각)
- Codex CLI 인자 ~32KB 한계 — 윈도 환경 디테일

**자료 출처**:
- `0-공통-도메인/contracts/03-model-lineup.md` (모델 ID·검증 일자)
- `0-공통-도메인/q7-session-handoff.md` §5 (어댑터 매핑)

**슬롯 상태**: 표 1장 즉시 작성 가능

---

## 슬롯 5. 사례: 성형외과 carousel (6분)

**메시지**: "실제로 위 캐논 + 매트릭스로 만든 1세트 — 비용 차별화 angle, PESONA 매핑."

**자산**:
- 4장 carousel 결과물 PNG (1장 Problem · 2장 Empathy · 3장 Offer · 4장 Action)
- 각 장 = 어떤 캐논 inject + 어느 모델 호출 매핑 (오버레이 또는 다음 슬라이드)
- 라운드 1-6 흐름 한 페이지 요약 (브리프 → 조사 → 회의 → 카피 → 이미지)

**자료 출처**:
- `3-마케팅-콘솔/docs/q7-round6/images/page-1-codex-v2.png` ~ `page-4-single-v2.png`
- `0-공통-도메인/decisions/2026-05-06-carousel-workflow.md` (8단계 워크플로)

**슬롯 상태**: 이미지 4장 복사 + 매핑 오버레이 신규 제작

---

## 슬롯 6. 아마존 적용 (가설) (3분)

**메시지**: "같은 원리로 amazon listing 뽑으면? 캐논 (`17-amazon-listing-and-aplus.md`) + 동일 매트릭스 → 결과."

**자산**:
- amazon-listing 7 필드 다이어그램 (Title / Main Image / Bullet 5 / Description / Backend KW / A+ / Brand Story)
- inject할 캐논 매핑 (AIDA → Bullet 1·2 / Schwartz → Title fold / Ogilvy → Title 헤드 / Stories → A+ Header)
- **[트랙 B 결과 슬롯]**: 콘솔 `/amazon-listing` 페이지 실제 결과 — 트랙 B 진행되면 스샷 흘려넣음
- **[트랙 B 결과 슬롯]**: Before (캐논 없음) / After (캐논 inject) 비교
- **[트랙 B 결과 슬롯]**: 실제 셀러 1 vertical 시연 결과

**자료 출처**:
- `0-공통-도메인/deep-adapters/marketing/17-amazon-listing-and-aplus.md` (전체)
- `0-공통-도메인/decisions/2026-05-06-console-mvp.md` §4 페이지 (`/amazon-listing` MVP-2)

**슬롯 상태**: 다이어그램 + 매핑 = 즉시 / 트랙 B 결과 = placeholder (추후 흘려넣음)

---

## 슬롯 7. 현재 한계·다음 (1분)

**메시지**: "솔직히 — 콘솔 빌드 진행 중, 아직 안 풀린 거 있음."

**자산**:
- 진행 상태 한 페이지 (트랙 A: 캐논 정련 중 / 트랙 B: 콘솔 v0 빌드 중)
- 미해결 질문 3개 (parking-lot Q1·Q3·Q8 정도)
- 마무리 한 줄 — "이게 제 실험 노트입니다."

**자료 출처**:
- `0-공통-도메인/open-questions/parking-lot.md`
- `0-공통-도메인/q7-session-handoff.md` §8 다음 액션

**슬롯 상태**: 텍스트만 — 즉시 작성 가능

---

# 자료 흘려넣기 룰 (이번 발표 후에도 살아있는 outline)

발표 끝난 후 트랙 A·B 진행되면서 이 outline에 추가:

| 슬롯 | 추후 받을 자료 |
|---|---|
| 3 캐논 깊이 | 새 캐논 파일 박힐 때마다 |
| 6 아마존 적용 | 콘솔 `/amazon-listing` 페이지 빌드 결과·스샷 |
| 6 아마존 적용 | Before/After 실제 비교 결과 |
| 5 사례 | 다른 vertical (병원·치과·필라테스·학원·카페) carousel 추가 |

추가 시 web-ppt 결과물 (`presentation.html`) 의 placeholder 슬롯에 직접 삽입 또는 스킬 재호출.

---

# 발표 폴더 구조

```
D:\잠깐만머물께\260506 아마존 웨비나\
├── 29829d381264607066c95afbd890317c.jpg   (디자인 컬러감 ref — 사용자 제공)
├── outline.md                              (이 파일)
├── design-spec.md                          (스타일 결정 — Paperlogy / 그라디언트 핑크 / WebGL)
├── source/                                 (추가 자료 받는 폴더 — 사용자 추후)
└── presentation.html                       (web-ppt 스킬 산출, 다음 단계)
```
