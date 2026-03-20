# 작업 히스토리

---

## 요청 1 — 웹사이트 초기 제작

### 사용자 요청
`resource` 폴더에 있는 이미지 파일 3개 (`Desktop - 2.png`, `btn_start.png`, `star_title.png`)를 이용해서 `concept1.png`와 같은 웹사이트 화면을 만들어달라.
`btn_start.png`를 눌렀을 때 `Desktop - 2.png` 화면으로 이동하게 만들어달라.

### 사고 과정
1. 작업 디렉터리(`/Users/kaylee/Desktop/studio team/krackers/소멸성/website/`) 내 파일 구조 확인
2. `resource/` 폴더에 `Desktop - 1.png`, `Desktop - 2.png`, `btn_start.png`, `star_title.png`, `concept1.png` 존재 확인
3. `concept1.png` 이미지를 분석하여 레이아웃 파악:
   - 배경: 별이 빛나는 궁전 마당 (`Desktop - 1.png`)
   - 중앙: 타이틀 이미지 (`star_title.png`) — 사라진 별에 별들이 모여든다
   - 하단 중앙: START 버튼 (`btn_start.png`)
   - 두 번째 화면: 더 어두운 동일 배경 (`Desktop - 2.png`)
4. 두 씬을 `position: fixed`로 겹쳐 놓고 `opacity` transition으로 fade 전환 구현
5. 타이틀에 float 애니메이션, 버튼에 pulse + hover glow 효과 적용
6. `index.html` 단일 파일로 작성

### 결과물
- `index.html` 생성
- Scene 1: `Desktop - 1.png` 배경 + `star_title.png` + `btn_start.png`
- Scene 2: `Desktop - 2.png` 배경 (빈 화면)
- 버튼 클릭 시 1.2초 fade 전환

---

## 요청 2 — Scene 2 메뉴 화면 구현

### 사용자 요청
Scene 2를 다음 스펙으로 발전시켜달라.

- 캔버스: `width: 1440px`, `height: 1024px`
- 타이포 색상: `#fff`
- 클릭 가능한 박스 3개 (ACADEMY / CHARACTER / WEBTOON):
  - `width: 380px`, `height: 280px`
  - 박스 간격: `32px`
  - 박스 색상: `#000 50%` (rgba)
  - 텍스트: `HeirofLightOTFBold.otf`, `28px`, `700`, center
- Back to the title 버튼:
  - 아이콘: `Vector1.svg`
  - 폰트: Sandoll HeirofLight, 28px, 700, white
  - 클릭 시 Scene 1으로 복귀

### 사고 과정
1. `resource/` 폴더 재확인 → `HeirofLightOTFBold.otf`, `Vector 1.svg` 파일 존재 확인
2. 1440×1024 고정 캔버스를 뷰포트에 맞게 `scale()` 변환하는 방식 채택 (반응형 대응)
3. `@font-face`로 `HeirofLightOTFBold.otf` 등록
4. `.back-btn`: `position: absolute; top: 56px; left: 72px` — `button` 태그 기본 스타일 reset 필요 → `background: none; border: none; padding: 0` 추가 (별도 Edit으로 수정)
5. `.menu-row`: flexbox, gap 32px, 3개 `.menu-box` 배치
6. JS에서 `scaleInner()` 함수로 `window.innerWidth/1440`과 `window.innerHeight/1024` 중 작은 값으로 scale, resize 이벤트에도 연결
7. `btnBack` 클릭 시 scene 전환 로직 추가

### 결과물
- Scene 2에 `scene2-layout` / `scene2-inner` 구조 추가
- Back to the title 버튼 (좌상단)
- ACADEMY / CHARACTER / WEBTOON 메뉴 박스 3개
- 뷰포트 크기에 따른 자동 scale 처리
- hover 시 박스 어두워짐 + 위로 4px 이동 효과

---

## 요청 3 — Scene 1 이미지 사이즈 조정

### 사용자 요청
- `star_title.png`: `width: 608px`, `height: 608px`, `aspect-ratio: 1/1`
- `btn_start.png`: `width: 203px`, `height: 73px`
- 둘 사이 간격: `12px`
- 그 외 요소 유지

### 사고 과정
1. 기존 `.title-img`의 `width: min(62vw, 820px)` → 고정값 `608px / 608px`으로 교체, `aspect-ratio: 1/1` 추가
2. 기존 `.btn-start`의 `margin-top: 5vh`, `width: min(18vw, 240px)` → 고정값 `203px / 73px`으로 교체
3. `.title-content`의 `gap: 0` → `gap: 12px`으로 변경, 기존 `margin-top` 제거하여 gap으로 통일

### 결과물
- `star_title.png` 608×608px 고정, aspect-ratio 1/1 적용
- `btn_start.png` 203×73px 고정
- 두 요소 사이 간격 12px

---

## 요청 4 — 히스토리 및 요청 문서 저장

### 사용자 요청
지금까지의 모든 요청과 사고 과정을 `history.md`로 저장하고, 요청 텍스트만 모아 `request.md`로 저장해달라. 오래된 순으로 정렬.

### 사고 과정
1. 대화 전체를 순서대로 정리
2. `history.md`: 요청 + 사고 과정 + 결과물을 요청별로 섹션화
3. `request.md`: 사용자 요청 텍스트만 발췌하여 별도 파일로 작성
4. 두 파일 모두 오래된 순(요청 1 → 4) 정렬

### 결과물
- `history.md` 생성
- `request.md` 생성

---

## 요청 5 — Scene 3 웹툰 뷰어 구현

### 사용자 요청
Scene 2에서 'WEBTOON' 박스를 클릭하면 Scene 3로 넘어가게 만들어달라.
Scene 3는 `web-webtoon.png`를 참고해서 만들어달라.
`p1`, `p2`, `p3`, `p4`를 빈틈없이 이어붙여서 스크롤해서 볼 수 있게 만들어달라.
Back btn은 스크롤해서 아래로 내려도 계속 같은 자리에 유지되도록 fixed하게 만들어달라.
항상 최상단으로 올라갈 수 있는 'back to the top' 아이콘을 우측 하단에 작게 만들어달라.

### 사고 과정
1. `resource/` 폴더 확인 → `p1.png`, `p2.png`, `p3.png`, `p4.png`, `web-webtoon.png` 존재 확인
2. `web-webtoon.png` 레퍼런스 분석: 검정 배경 위에 웹툰 패널이 세로로 나열된 구조
3. Scene 3 스크롤 처리 방식 결정:
   - 기존 씬들은 `position: fixed; overflow: hidden` — Scene 3는 `overflow-y: auto`로 오버라이드
   - `body`의 `overflow: hidden`은 유지하면서 씬 컨테이너 자체에서 스크롤
4. 이미지 연결 방법: `display: block; width: 100%` → 이미지 간 기본 gap(inline gap) 제거
5. Back button: `position: fixed` + `z-index: 100` → 스크롤과 무관하게 뷰포트에 고정
6. Back to top 버튼:
   - `position: fixed; bottom: 40px; right: 40px`
   - 기본 `opacity: 0; pointer-events: none` → 300px 이상 스크롤 시 `.visible` 클래스로 표시
   - SVG chevron-up 아이콘 사용, 반원 테두리 스타일
7. JS `showScene()` 헬퍼 함수 추가 — 씬 전환 로직 통일
8. WEBTOON 박스에 `id="menu-webtoon"` 추가, 클릭 이벤트로 Scene 3 표시
9. Scene 3 진입 시 `scrollTop = 0` 리셋
10. `vertical-align: bottom` 경고(block 요소에 무효) → 제거

### 결과물
- Scene 3 (`#scene-webtoon`) 추가: 검정 배경 + 최대 860px 폭 웹툰 스트립
- p1~p4 `display: block; width: 100%` 로 gap 없이 이어붙임
- 고정 Back 버튼 (`.back-btn-webtoon`) — 스크롤 중에도 좌상단 고정
- Back to top 버튼 — 우측 하단 고정, 300px 스크롤 후 등장
- WEBTOON 메뉴박스 클릭 → Scene 3 전환
- Scene 3 Back 버튼 클릭 → Scene 1 복귀
