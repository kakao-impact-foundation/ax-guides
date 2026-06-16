# ax-guides

카카오임팩트 재단 AX의 **내부 가이드 모음**입니다. 가이드 원본(Markdown)과, 그것을 보기 좋게 렌더한 **정적 사이트**를 한 레포에서 관리합니다.

## 구조

```
ax-guides/
├── index.html          # 가이드 허브 (카드 목록)
├── viewer.html         # 가이드 뷰어 (docs/*.md 를 렌더)
├── docs/               # 가이드 원본 (Markdown) — 여기만 고치면 사이트에 반영
│   └── github.md       # GitHub 사용 가이드
├── assets/
│   ├── styles.css      # kakao!mpact 디자인 토큰 차용 (크림 배경·검정 외곽선·옐로 강조)
│   └── img/            # 로고·마크
└── .nojekyll           # GitHub Pages의 Jekyll 처리 비활성화
```

## 가이드 추가하는 법

1. `docs/` 에 새 Markdown 파일을 추가합니다 (예: `docs/slack.md`).
2. `viewer.html` 의 `DOCS` 객체에 한 줄 등록합니다.
   ```js
   const DOCS = {
     github: { file: 'docs/github.md', title: 'GitHub 사용 가이드' },
     slack:  { file: 'docs/slack.md',  title: '슬랙 사용 가이드' },   // 추가
   };
   ```
3. `index.html` 에 카드 한 장을 추가합니다 (`href="viewer.html?doc=slack"`).

## 로컬 미리보기

`file://` 로 열면 브라우저 보안 때문에 `docs/*.md` fetch가 막힙니다. 로컬 서버로 여세요.

```bash
cd ax-guides
python3 -m http.server 8000
# → http://localhost:8000
```

## 배포

- 디자인 톤: `_design/kakaoimpact - theme (Template)` 의 색·타이포·외곽선 토큰 차용.
- 가이드 내용에 내부 정보(계정 컨벤션·내부 링크 등)가 있어 **비공개 레포**로 운영합니다.
- **GitHub Pages는 비영리 인증(GitHub for Nonprofits, Team 플랜) 승인 후** 비공개 레포 상태로 켭니다. (무료 플랜은 공개 레포만 Pages가 가능)
- 승인 전 임시 공유가 필요하면 위 로컬 서버로 미리보거나, 별도 협의 후 결정합니다.

---

관련 운영 문서: `01.kakaoimpact-AX/_workspace/deploy-security/`
