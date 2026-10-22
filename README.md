# Otherside Holder → Player Conversion (임의 데이터 대시보드)

`index.html` 하나로 동작하는 정적 페이지입니다. 폰트와 데이터가 파일 안에 들어 있고, 차트 라이브러리(d3 7.9.0)만 jsDelivr에서 불러옵니다(인터넷 필요).

- 저장소: https://github.com/seongchul33/otherside-dashboard (main, 현재 `index.html` 한 개가 올라가 있음)
- 배포 주소(GitHub Pages): https://seongchul33.github.io/otherside-dashboard/

## 로컬에서 보기
`index.html`을 브라우저로 열면 됩니다.

## 수정 후 배포
이 폴더에서 수정한 뒤 저장소에 push하면 1~2분 뒤 배포 주소에 반영됩니다.
```
git clone https://github.com/seongchul33/otherside-dashboard.git
# 수정한 파일로 덮어쓰기
git add .
git commit -m "update dashboard"
git push
```

## 폴더
- `index.html` 대시보드 본체(CSS, 데이터, 계산, 차트 코드가 모두 들어 있음)
- `data/` 화면에 쓰인 CSV 원본(참고용). 같은 값이 `index.html`의 `__DATA`에 들어 있습니다.
- `fonts/` 사용하는 글자만 남긴 폰트 파일과 라이선스(OFL). `index.html`에는 이미 포함되어 있습니다.
- `HANDOFF.md` 이어서 작업할 때 필요한 맥락
