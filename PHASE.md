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

## Phase 2: 추가 고려 사항 (미착수)

### 선택적 작업
- [ ] 해커톤 전용 섹션(서비스 소개, 추천 점수 UI) HTML 추가 여부 결정
- [ ] 결과 페이지에 추천 이유/비교 테이블 UI 추가
- [ ] 다크모드에서 해당 신규 디자인 요소 추가 검증
- [ ] 모바일 반응형 세부 조정 (600px 이하)
- [ ] 성능 점검: 추가된 CSS 애니메이션이 저사양 기기에서 부드러운지 확인
