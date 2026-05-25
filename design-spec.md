---
title: 아마존 웨비나 발표 — 디자인 스펙
reference_image: 29829d381264607066c95afbd890317c.jpg (사용자 제공)
status: SPEC v1 (web-ppt 스킬 input용)
---

# 디자인 결정 (사용자 명시 + ref 이미지 분석)

## 1. 컬러 팔레트

### 베이스
- **Page background (외곽)**: `#D4C5C8` 따뜻한 라일락/dusty rose
- **Slide card surface**: `#FAF7F5` 따뜻한 크림 화이트
- **Card border**: `#EDE5E2` 거의 안 보이는 보더
- **Card shadow**: `rgba(60, 40, 50, 0.08)` 부드러운 plum-tinted shadow

### 텍스트
- **Heading (H1·H2)**: `#3D2A2D` 진한 다크 플럼
- **Body**: `#5A4548` 미디엄 plum-gray
- **Caption / 보조**: `#9A8A8C` 페일 plum-gray

### 핑크 그라디언트 (메인 액센트 — 사용자 명시)
원형 그라디언트 — 이미지처럼 큰 phantom circle 두 개 겹친 효과:

```css
background: radial-gradient(
  ellipse at 30% 40%,
  #F4B6B0 0%,      /* 코랄 핑크 */
  #F8DCC8 40%,     /* 살구 / peach */
  #E8E4C8 70%,     /* 페일 그린·옐로우 */
  transparent 100%
);
```

또는 두 원 겹침:
- 원 1: `radial-gradient(circle at 35% 45%, #F4B6B0 0%, #F8C8C0 30%, transparent 60%)`
- 원 2: `radial-gradient(circle at 60% 55%, #F8DCC8 0%, #E8E4C8 40%, transparent 70%)`

### 차트·데이터
- **Bar / 인포그래픽 fill**: 위 그라디언트 동일 (핑크 → 살구)
- **Bar 음영**: `linear-gradient(180deg, #F4B6B0 0%, #F8C8C0 100%)`
- **Cap (둥근 캡)**: 라운드 끝 (border-radius: 999px on top)

---

## 2. 타이포그래피 — Paperlogy 단독 (사용자 명시)

Paperlogy 한글 폰트 weight scale로 위계:

| Role | Font | Weight | Size | Line-height | 용도 |
|---|---|---|---|---|---|
| **Display** | Paperlogy | 900 (Black) | 60-72px | 1.1 | 슬라이드 메인 제목 |
| **H1** | Paperlogy | 800 (ExtraBold) | 44-52px | 1.15 | 섹션 타이틀 |
| **H2** | Paperlogy | 700 (Bold) | 28-32px | 1.2 | 카드 제목 |
| **H3** | Paperlogy | 600 (SemiBold) | 20-22px | 1.3 | 서브 제목 |
| **Body** | Paperlogy | 400 (Regular) | 16-18px | 1.6 | 본문 |
| **Caption** | Paperlogy | 300 (Light) | 13-14px | 1.5 | 라벨·보조 |

**한글 자간 (letter-spacing)**: -0.02em (Paperlogy는 살짝 좁히면 더 정돈됨)

**폰트 로드**:
- Paperlogy 공식 GitHub release CSS 또는 jsDelivr CDN
- fallback: `Pretendard, -apple-system, sans-serif`
- 9 weights 모두 로드 (display 900부터 thin 100까지)

---

## 3. WebGL 배경 (사용자 명시)

이미지의 정적 그라디언트 원을 살아있는 mesh gradient로:

**스펙**:
- WebGL fragment shader 또는 lightweight library (e.g., `mesh-gradient`, `granim`, custom Three.js)
- 핑크·코랄·살구·페일그린 4 컬러 mesh
- 슬로우 motion (15-20초 cycle, ease-in-out, 거의 안 보일 정도로 느리게)
- bloom / soft blur 효과 (50-80px blur radius)
- opacity 0.35 ~ 0.5 (콘텐츠 가려지면 안 됨)
- 슬라이드 카드 뒤 layer (z-index: 0, 카드는 z-index: 10+)
- prefers-reduced-motion → 정적 그라디언트 fallback

**성능 룰**:
- 60fps 유지 (저사양 모니터 고려)
- requestAnimationFrame 기반
- 페이지 비활성 시 pause (Page Visibility API)

---

## 4. 컴포넌트 토큰

### Card (슬라이드 본문 카드)
- `background`: `#FAF7F5`
- `border-radius`: `28px`
- `box-shadow`: `0 8px 32px rgba(60, 40, 50, 0.08), 0 2px 8px rgba(60, 40, 50, 0.04)`
- `padding`: `48px 56px`
- `border`: `1px solid #EDE5E2`

### Slide container
- 16:9 비율
- max-width: 1200px (centered)
- 내부 카드 형태로 콘텐츠 wrapping

### Image / 사진
- `border-radius`: `20px`
- 부드러운 shadow

### Diagram / 인포그래픽
- 원형 / Venn-style 선호 (ref 이미지의 겹친 원 패턴)
- 핑크 그라디언트 fill, 60% opacity
- 라벨은 진한 플럼 (#3D2A2D)

### Bar chart
- 막대 라운드 캡 (radius 999px)
- 핑크 그라디언트 (코랄 → 살구)
- baseline은 페일 (#EDE5E2)
- 숫자 큰 weight로 강조

---

## 5. 레이아웃 룰

- **viewport lock**: 슬라이드 1장 = 100vh / 100vw 또는 16:9 컨테이너
- **여백**: 상하 64-80px / 좌우 80-120px (카드 안)
- **그리드**: 12 column (gap 24px) — 멀티 카드 배열 시
- **콘텐츠 max-width**: 980px (가독성)
- **인터랙션**: 키보드 화살표 / 클릭 / 스페이스로 슬라이드 이동

---

## 6. 슬라이드 transition

- 페이지 전환 = fade + 살짝 위로 (translateY -12px) cubic-bezier
- 듀레이션: 400ms
- WebGL 배경은 transition 동안 계속 흐름 (continuity)

---

## 7. 콘텐츠 element 강조

- **숫자 강조**: Paperlogy 900, 핑크 그라디언트 (background-clip: text)
- **인용 / verbatim**: 좌측 핑크 4px border + 살짝 들여쓴 italic
- **코드 / file path**: 모노스페이스 fallback (`JetBrains Mono`, `Consolas`) — Paperlogy 모노 없음
- **체크리스트**: 핑크 둥근 체크 아이콘

---

## 8. 인터랙션 / 모션

- 슬라이드 진입 시 콘텐츠 stagger (텍스트 → 이미지 → 다이어그램 순으로 50ms 간격)
- 그래프·다이어그램 = 진입 시 한 번 그려지는 애니메이션 (svg path animate)
- WebGL 배경 = 항상 흐름

---

## 9. 자료 임베드 룰

- **그래프 (graph.html)**: iframe 임베드 또는 스크린샷 (slot 3)
- **carousel 4장 (성형외과)**: 가로 4 grid 또는 hover 확대 (slot 5)
- **Before/After 비교** (slot 6, 추후): 좌우 split

---

## 10. 출력

- 단일 self-contained HTML (`presentation.html`)
- 외부 의존: Paperlogy CDN + WebGL library CDN만
- 이미지·자료는 `assets/` 또는 `source/` 상대 경로
- 인쇄 / PDF export 호환 (그라디언트는 정적 fallback)
