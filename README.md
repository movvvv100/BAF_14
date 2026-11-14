# ebuTuoY — 내가 보지 못하는 유튜브

내 유튜브 홈 화면 캡처를 올리면 알고리즘 편향을 분석하고, 정반대의 영상으로 채운 화면을 보여주는 데이터 시각화 과제용 데모입니다.

## GitHub Pages에 올리기

1. GitHub에서 새 저장소(Public)를 만든다.
2. `index.html`을 저장소에 올린다 (Add file → Upload files).
3. Settings → Pages → Branch를 `main` / `(root)`로 두고 Save.
4. 1~2분 뒤 `https://<아이디>.github.io/<저장소 이름>/` 으로 접속한다.

## 처음 접속했을 때

API 키는 `index.html`의 `KEYS`에 들어 있어 접속하면 바로 동작한다.


## 동작 순서

1. 캡처 → Gemini가 영상 제목·채널을 읽고 카테고리·키워드 분석 (Gemini 1회)
2. 자주 나온 채널 6개의 소개글·최근 영상 수집 (YouTube 검색 6회)
3. 채널 성향 분석 + 반대 검색어 만들기 (Gemini 1회)
4. 반대 영상 수집 (YouTube 검색 7~9회 + 인기 차트)

분석 1건에 YouTube 검색 약 15회(하루 한도 100회 → 하루 6건 안팎), Gemini 2회를 쓴다.
결과는 브라우저에 저장되어 새로고침해도 다시 호출하지 않는다.

## 구성 바꾸기

`index.html`의 `CONFIG`만 고치면 된다.

- `LAYOUT`: 한 화면 칸 구성과 순서 (same / cat / foreign / other / rookie)
- `SETS`: 상단 숫자 칩 개수
- `TOP_CHANNELS`: 깊이 볼 채널 수 (줄이면 검색 한도 절약)

## API 키 보호 (꼭 하기)

키가 공개 코드에 들어 있으므로 Google Cloud Console → API 및 서비스 → 사용자 인증 정보에서 각 키에
**웹사이트 제한**을 걸고 `https://<아이디>.github.io/*` 만 허용한다. 이렇게 하면 다른 사이트에서는 이 키를 쓸 수 없다.

