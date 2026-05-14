# SUWONMATE 프론트엔드 디자인 리프레시 — Phase 문서

## Phase 1: 디자인 시스템 마이그레이션 (완료)

### 목표
`suwon_smart_timetable_hackathon_polished.html`의 디자인을 현재 프론트엔드에 적용.
기존 기능(백엔드 API 연동, JS 로직)은 그대로 유지하면서 CSS만 오버레이.

### 변경 내역

#### 1. 폰트 추가
- **Bricolage Grotesque** 구글폰트 링크 추가
- body 폰트 스택: `'Bricolage Grotesque', 'Noto Sans KR', system-ui, ...`

#### 2. `<style id="suwonmate-ui-refresh">` 블록 삽입 (~460줄)
| 항목 | 기존 (Apple-style) | 변경 (SUWONMATE) |
|------|-------------------|------------------|
| 메인 컬러 | `#0066cc` (Apple Blue) | `#0052ff` (Vivid Blue) + `#FDE047` (Yellow) |
| 배경 | 순백 `#ffffff` | radial-gradient 노랑/파랑 오버레이 |
| border-radius | `18px` | `32px` |
| 그림자 | `none` | `0 8px 24px rgba(0,62,204,.08)` 등 |
| CTA 버튼 | Apple Blue 배경 | 노란색 배경 + 아래쪽 box-shadow |
| 로고 마크 | near-black 배경 | 노란색 배경 + offset shadow |
| 카드 | 흰 배경, 얇은 border | 반투명 배경, 두꺼운 border, 그림자 |
| 다크모드 | 순검정 `#000000` 기반 | 네이비 `#071326` 기반 |
| 타일 컬러 | `#1d1d1f` (near-black) | `#001a33` ~ `#003ecc` (deep navy) |

#### 3. `<style id="suwonmate-motion-ui">` 블록 삽입 (~398줄)
| 효과 | 설명 |
|------|------|
| `suwonPageFade` | 라우트 전환 시 fade-in + slide-up |
| `suwonHighlightDraw` | `.accent` 텍스트 뒤 형광펜 드로우 애니메이션 |
| `suwonBadgeFloat` | 배지/태그 둥둥 부유 |
| `suwonButtonShine` | CTA 버튼 hover 시 빛 반짝임 |
| `suwonPop` | 옵션 선택 시 통통 튀는 피드백 |
| `suwonNavDrop` | 네비게이션 바 등장 애니메이션 |
| `suwonHeroIn` | 히어로 섹션 요소 순차 등장 |
| 카드 hover | translateY(-5px) + 그림자 강화 |
| `prefers-reduced-motion` | 접근성 — 모션 비활성화 대응 |

### 의도적으로 제외한 것
- **해커톤 전용 HTML 섹션**: story section, workflow section, scoring demo, comparison table (`.hm-*` 클래스)
- **JS 변경**: 하드코딩 학과 데이터(`UNI_DATA`), API 제거, `Object.freeze()` 등
- **로그인 폼 변경**: 학번 필드 추가, 학과 optgroup 하드코딩
- **서버 설정 패널 제거**: 기존 백엔드 연동 유지

### 적용 방식
기존 CSS는 건드리지 않고 새 `<style>` 블록을 뒤에 추가하여 cascade로 덮어쓰기.
`!important`를 활용해 기존 인라인 스타일도 오버라이드.

---

## Phase 2: 해커톤 프레젠테이션 섹션 추가 (완료)

### 목표
해커톤 심사용 서비스 소개 섹션과 결과 페이지 추천 점수 UI를 추가.
다크모드 대응 + 모바일 반응형 포함.

### 변경 내역

#### 1. 홈페이지 (route-index) — 3개 섹션 추가
Hero 섹션과 Feature Cards 섹션 사이에 삽입:

| 섹션 | 클래스 | 내용 |
|------|--------|------|
| Story Section | `.hm-section` | 기존 방식의 문제 vs suwonmate 해결 방식 비교 카드 |
| Workflow Section | `.hm-workflow` | 4단계 사용자 플로우 (입력 → 조건 → 비교 → 저장) |
| Scoring Demo | `.hm-demo-band` | 추천 적합도 점수 92점 + 4개 미터 바 데모 |

#### 2. 결과 페이지 (route-result) — 추천 UI 추가
목표학점 선택 바(`.ctb`) 아래, 시간표 그리드(`.main-layout`) 위에 삽입:

| 컴포넌트 | 클래스 | 내용 |
|----------|--------|------|
| 점수 패널 | `.hm-result-summary > .hm-score-panel` | 적합도 92점 + 4개 미터 바 (네이비 배경) |
| 추천 이유 | `.hm-result-summary > .hm-reason-card` | 4가지 추천 근거 카드 (2x2 그리드) |
| 비교 테이블 | `.hm-compare-polish > .hm-compare-table` | 추천안 A/B/C 정량 비교 (추천도, 공강, 학점, 이동거리) |

#### 3. CSS 추가 (~270줄)
`suwonmate-ui-refresh` 스타일 블록 끝에 추가:

- **`.hm-*` 컴포넌트 스타일**: 카드, 그리드, 미터 바, 칩, 배지 등
- **다크모드**: `.hm-section`, `.hm-workflow`, `.hm-demo-band`, 결과 페이지 패널 모두 대응
- **반응형 (900px, 620px)**: 그리드 1열 폴백, 패딩 축소, 폰트 크기 조정

### 작업 결과
- 34,096줄 → 34,477줄 (+381줄: HTML ~110줄 + CSS ~270줄)
- 12개 라우트 구조 변경 없음
- JS/API 연동 변경 없음
