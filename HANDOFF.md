# 핸드오프 메모 (AI 코딩 도구용)

이 폴더를 열고 이어서 작업할 때 필요한 맥락입니다.

## 프로젝트
인하대 INGAME 팀의 Yuga Labs 연계 프로젝트. NFT(BAYC, MAYC, Koda) 보유자가 Otherside 게임으로 얼마나 전환되는지 보여주는 **운영자용 분석 화면의 시안**입니다. 이 화면 구현(임의 데이터 기반 웹 화면)이 사용자(성철) 담당입니다.

## 현재 상태
- GitHub 저장소 https://github.com/seongchul33/otherside-dashboard 를 만들었고(공개), main에 `index.html` 한 개가 올라가 있습니다.
- GitHub Pages가 main, /(root)로 켜져 있고 https://seongchul33.github.io/otherside-dashboard/ 에서 열립니다.
- 이 폴더의 `index.html`이 저장소의 것보다 최신입니다. (Utility 사용자 HRR 이름 변경 반영)
- Claude 채팅에서는 브라우저 파일 업로드가 막혀 있어서, 수정본을 올릴 때마다 사용자가 직접 올렸습니다. Claude Code나 Cursor에서는 git push로 직접 올릴 수 있습니다.
- 원본 Claude 대시보드(참고용): https://claude.ai/artifact/CkcoVP9UGeLQ8xtkadstpL

## 사용자가 정한 규칙 (바꾸지 말 것)
- 값이 임의 데이터이면 이름 뒤에 `(sample)`을 붙인다. 붙지 않은 값만 실측이다. (팀 공유 문구에서는 "임의 데이터"라고 말했으므로, 화면 표기를 "(임의)"로 바꿀지는 사용자에게 먼저 물어볼 것.)
- 컬렉션은 BAYC, MAYC, Koda다. (제안서의 Otherdeed 표기는 오타였고 Koda가 맞다.)
- 화면에 내부 문서를 가리키는 문구(KPI 문서, 제안서, Methods 등)를 쓰지 않는다. 실제 서비스 화면처럼 보여야 한다.
- 스타일은 OpenSea 컬렉션 페이지 느낌의 어두운 UI. 포인트 색은 파랑, 초록, 보라. 터미널 느낌, 앰버색, 번호 매긴 패널, 장식 문구는 쓰지 않는다.
- 폰트: 본문은 Instrument Sans, 숫자는 Geist Mono(파일에 포함됨). 한글은 기기 기본 폰트(맑은 고딕, Apple SD Gothic Neo)로 폴백한다.
- 비율은 소수점 둘째 자리까지. 차트는 눈금, 격자, 축 라벨이 있어야 한다.
- Segment map과 Conversion by collection은 값 라벨을 항상 보이지 않고 hover 툴팁으로만 보인다.
- 불필요한 기능(틀 고정, 병합 셀 등)을 넣지 않는다. 담백하게.
- 사용자 집단 이름은 "HRR 사용"이 아니라 **"Utility 사용자 HRR / Utility 미사용자 HRR"**로 쓴다(헷갈린다는 지적이 있었음).

## 탭 구성
Overview(퍼널, 컬렉션별 전환율, 컬렉션 표) · Utility(UAR, URR) · Economic(HRR, ΔHRR) · Segments(세그먼트 지도, 표, 프로필) · Prediction(사용자별 전환 확률, 영향 요인, 모델 성능)
뺀 것: Evidence 탭, ROC curve, 정의 설명 패널, Economic Productivity 패널.

## 데이터
- 실측: `data/real_holders.csv`의 보유 지갑 수(Etherscan, 2026-10-13 기준: BAYC 5,582 / MAYC 12,078 / Koda 3,223). 나머지 CSV는 전부 임의 데이터입니다.
- 임의 데이터끼리 맞춰 둔 관계: 퍼널의 Player 수 = UAR의 Experience 사용자 수, 사용자+미사용자 = 실측 보유 지갑 수, URR의 최초 사용자 수 = UAR 사용 보유자 수의 합.
- 퍼널의 D7, D30 괄호는 Player 대비 유지율(Player Retention). Visitor와 Player는 직전 단계 대비.

## 알려진 한계 (개발자 메모)
- 실측은 보유 지갑 수 하나뿐입니다. 전환율, Utility 사용, 유지율, 예측은 모두 임의 데이터입니다.
- 보유 지갑 수는 Etherscan Holders 표기값이라 컨트랙트 주소(스테이킹·에스크로 등)가 포함돼 있습니다. 팀의 측정 기준은 컨트랙트 제외입니다.
- 관측기간과 N일(D30, D90) 값은 임의로 가정한 것입니다.
- 세 컬렉션 합계의 보유 지갑 수는 한 지갑이 여러 컬렉션을 가지면 중복 집계됩니다.

## 실제 데이터를 붙이려면
- 보유자와 이전 기록: Alchemy 또는 Dune(Transfer 이벤트). 이것으로 HRR(컬렉션 단위, 토큰 단위)은 공개 데이터만으로 계산 가능합니다.
- 방문, 플레이, Utility 사용 로그는 Yuga Labs 데이터가 필요합니다(user_id와 wallet_address 매핑 포함).
- `index.html`의 `__DATA`와 `dash.calc(...)` 부분만 바꾸면 화면은 그대로 동작합니다.

## 이어받는 도구에 붙여넣을 첫 프롬프트
```
이 폴더의 HANDOFF.md와 README.md를 먼저 읽어줘. index.html은 정적 대시보드야.
HANDOFF.md의 "사용자가 정한 규칙"을 지키면서 작업해줘.
1) 먼저 index.html을 브라우저로 열어서 5개 탭이 오류 없이 그려지는지 확인해줘.
2) GitHub 저장소 https://github.com/seongchul33/otherside-dashboard 에는 오래된 index.html 한 개가 있어.
   저장소를 clone해서 이 폴더의 파일들로 덮어쓰고 commit, push해줘. (내가 로그인한 git 계정을 쓰면 돼.)
3) 1~2분 뒤 https://seongchul33.github.io/otherside-dashboard/ 가 최신 화면인지 확인해줘.
그다음에 내가 요청하는 수정을 이어서 해줘.
```
