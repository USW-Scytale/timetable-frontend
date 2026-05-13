# 수원대 스마트 시간표 — 프론트엔드

수원대학교 학생을 위한 시간표 자동 생성·졸업요건 분석·학사 관리 통합 SPA.  
**단일 HTML 파일**로 동작하며, 별도 빌드/번들러 없이 브라우저에서 바로 실행됩니다.

---

## 배포

GitHub Pages: **https://usw-scytale.github.io/timetable-frontend/**

백엔드 서버 주소는 앱 로그인 화면 하단 **"서버 설정"** 버튼에서 변경할 수 있습니다.

---

## 주요 기능

| 영역 | 내용 |
|---|---|
| 인증 | 회원가입 / 로그인 (JWT) |
| 시간표 추천 | 공강일·시작 교시·관심사 기반 플랜 A·B·C 자동 생성 |
| 졸업요건 분석 | 미이수 영역 계산, 필수과목 체크리스트 |
| 수강 추천 | 졸업요건 기반 추천 과목 목록 |
| 빈 강의실 조회 | 건물·교시·요일별 빈 강의실 |
| 캠퍼스 경로 | 건물 간 도보 최단 경로 (Dijkstra) |
| 시간표 저장 | 저장·관리·PNG 내보내기 |

---

## 백엔드 연동

백엔드 레포: [USW-Scytale/timetable-backend](https://github.com/USW-Scytale/timetable-backend)

앱 실행 시 `BASE_URL` (기본 `http://localhost:8000/v1`) 로 API를 호출합니다.  
배포 환경에서는 로그인 화면 → **서버 설정**에서 ngrok / 운영 서버 URL로 변경하세요.

---

## 파일 구조

```
timetable-frontend/
├── index.html    ← 메인 앱 (CSS + JS + HTML 단일 파일 SPA)
└── README.md
```

---

## 기술 스택

- Vanilla HTML / CSS / JavaScript (빌드 도구 없음)
- 단일 파일 SPA (hash routing)
- html2canvas — 시간표 PNG 내보내기
- Tesseract.js v5.1 — 성적표 OCR
- FastAPI 백엔드 (별도 레포)
