# 포르투갈 · 스페인 여행 — 휴대폰용 (로그인 없음)

정적 페이지입니다. 계정·서버·앱 설치 없이 `index.html`만 열면 됩니다.  
데이터는 `trip_board.json`(보드 사실만)이며, HTML에도 동일 데이터가 임베드되어 **파일로 직접 열어도** 동작합니다.

## 빠른 열기 (아이폰)

1. Mac/PC에서 `mobile` 폴더 또는 `trip-mobile.zip`을 AirDrop / iCloud Drive / 메시지 / 메일로 보냅니다.
2. 아이폰에서 압축을 풀고 **파일** 앱에서 `index.html`을 탭합니다.
3. 공유 → **Safari에서 열기** (또는 파일 앱 미리보기에서 Safari로 열기).
4. Safari에서 공유 → **홈 화면에 추가** 하면 앱처럼 쓸 수 있습니다.

> `file://`로 열면 서비스 워커는 등록되지 않지만, 임베드된 JSON으로 오프라인 조회는 됩니다.

## 로컬 서버 (권장 · 오프라인 캐시)

같은 Wi‑Fi의 노트북/데스크톱에서:

```bash
cd /path/to/mobile
python3 -m http.server 8080
```

폰 브라우저에서 `http://<노트북-IP>:8080` 접속.  
HTTP로 열면 `sw.js`가 `index.html` + `trip_board.json`을 캐시합니다.

간단 대안:

```bash
npx --yes serve -l 8080
```

## 탭 · 해시 라우트

| 탭 | 해시 | 내용 |
|----|------|------|
| 오늘 | `#/today` | 유럽 현지 날짜가 여행 기간이면 그날, 아니면 가장 가까운 날 |
| 일정 | `#/days` · `#/day/YYYY-MM-DD` | 전체 일 → 상세 |
| 숙소 | `#/stays` | 확인코드·일정·금액 |
| 예약 | `#/bookings` | 항공·열차·렌터카 |
| 비용 | `#/spend` | 선결제·Hertz € · 현장 지출(`spend.live`) |
| 공백 | `#/gaps` | 마드리드 숙소, NOH 귀국권, 코르도바 등 |

## 데이터

- 근거: `/workspace/por-trip/trip_board.json` (및 보드 MD와 동일 사실)
- **예약 없는 항목은 만들지 않음.** 공백은 공백 탭·해당 일에 표시.


## Travel Desk 연동

Travel Desk가 `trip_board.json`에 `days[].day_plan`(동선)과 `spend.live`(현장 지출)를 쓰면 모바일 앱의 **오늘/일정**·**비용** 탭에 반영됩니다. 보드를 갱신한 뒤 `mobile/trip_board.json`과 `index.html`의 `#board-embed`를 다시 맞추고(또는 HTTP로 `trip_board.json`을 다시 받아) 새로고침하면 됩니다. `file://`로 열 때는 임베드 JSON이 소스이므로 재임베드가 필요합니다.

## 파일

- `index.html` — SPA (CSS/JS 포함)
- `trip_board.json` — 보드 데이터
- `sw.js` — 선택적 캐시 (http(s)만)
- `README.md` — 이 문서

상위 폴더의 `trip-mobile.zip`은 이 `mobile/` 전체를 압축한 핸드오프용입니다.

## Live
https://sunnysideplease.github.io/por-trip-mobile/
