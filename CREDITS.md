# 크레딧 & 출처

한국 갈론드 벨 (비영리 팬 도구)은 다음 오픈소스 프로젝트들 위에 만들어졌습니다.

- **GarlandTools** by ufx — 원본 갈론드 벨 엔진 (MIT)
  https://github.com/ufx/GarlandTools
- **GarlandBell** by arlequins — 파생 버전
  https://github.com/arlequins/garlandbell
- **한국 서버판 갈론드 벨** by Ariette — 한국어화 (MIT)
  https://github.com/Ariette/garlandbell
- **FFXIV Fish Tracker App** by icykoneko — 낚시 데이터 참고
  https://github.com/icykoneko/ff14-fish-tracker-app

게임 데이터·아이콘 © SQUARE ENIX. FFXIV Materials Usage License(비영리)에 따라 사용.

## 이 포크에서 변경한 것 (2026-06)

- **디자인 리뉴얼** — 모던 다크/라이트 테마(`theme.css`), 다크/라이트 토글. 원본
  `style.css`·엔진 로직은 보존하고 비주얼만 오버레이.
- **황금(7.x) 데이터 추가** — 글로벌 GarlandTools 최신 데이터에서 던트레일 채집
  노드 30종을 가져와 한섭 데이터(2.x~6.x)에 병합. `7.0` 버전 버튼 및 엔진의
  patch-7 필터 로직 추가.

## 번역 현황 — 전부 공식 명칭 확정 ✅

황금(7.x) 신규 명칭을 **KR 클라이언트 데이터마이닝**에서 글로벌 아이템 ID로
정확 매칭해 전부 공식 명칭으로 확정했습니다 (아이콘 공유 문제 없음):

- **아이템 40종** — [`Ra-Workspace/ffxiv-datamining-ko`](https://github.com/Ra-Workspace/ffxiv-datamining-ko)
  `Item.csv`에서 아이템ID→공식명 직접 매칭. 스크립트: [`_build/resolve_by_id.py`](_build/resolve_by_id.py).
  (예: Brightwind Ore→양풍암, Electrocoal→흑뢰암, Rarefied X→소장용 X)
- **지역 6종 + 채집지 16종** — XIVAPI v2(EN→placeID) + KR `PlaceName.csv`(placeID→공식명)
  교차. 스크립트: [`_build/resolve_places.py`](_build/resolve_places.py).
  (예: Urqopacha→오르코 파차, Living Memory→리빙 메모리)
- 크리스탈/클러스터 8종 — 기존 KR 데이터 ID 복구.

> 참고: ff14.co.kr 아이콘 매칭(`crawl_kr_names.py`)도 시도했으나, FFXIV가 채집
> 아이템에 아이콘을 공유해 19종이 구분 불가 → 데이터마이닝 CSV의 ID 직매칭으로 해결.

`ko-overrides.json` 수정 → `python _build/build-nodes.py`로 갱신. (`_build/backup/` 백업)

## 황금(7.x) 지도 지원

엔진 `gt.location.index`에 던트레일 지역 9엔트리(6지역 + Yok Tural/Xak Tural/
Unlost World 3개 상위지역)를 글로벌 엔진에서 추출해 주입하고, 지도 이미지는
garlandtools(`files/maps/{지역}/{맵}.png`)에서 받아 1024px JPG로 변환해 추가.
즐겨찾기 시 던트레일 노드 지도가 마커와 함께 정상 렌더됨을 확인.
스크립트: [`_build/extract_dt2.py`](_build/extract_dt2.py), [`_build/fetch_dt_maps.py`](_build/fetch_dt_maps.py).
