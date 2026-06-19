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
- **공개 레포 + GitHub Pages**로 운영합니다. 무료 플랜은 공개 레포만 Pages를 띄울 수 있어서요.
- 가이드는 내부용 문서지만 키·개인정보 같은 민감 데이터는 없습니다. 다만 적극적으로 외부에 알릴 대상은 아니라 **검색 색인만 차단**해 둡니다.
  - `robots.txt` 에 `Disallow: /`
  - 각 페이지(`index.html`·`viewer.html`) `<head>` 에 `<meta name="robots" content="noindex, nofollow">`
  - → 검색엔 안 잡히고 **URL을 아는 사람만** 봅니다 (공개 URL 기반의 "캐주얼 차단").
- 더 가려야 할 내용이 생기면 **비공개 레포 + Vercel Pro**로 전환하세요. (판단 기준·방법은 `docs/github.md` 의 "외부 공개용 / 내부 공유용" 매트릭스 참조)

### Pages (이미 활성화됨)

`main` 브랜치 / 루트(`/`)에서 Pages가 켜져 있습니다 → `https://kakao-impact-foundation.github.io/ax-guides/`
`docs/*.md` 를 고쳐 push 하면 1~2분 뒤 자동 반영됩니다. 설정 확인이 필요할 때만:

```bash
gh api repos/kakao-impact-foundation/ax-guides/pages --jq '.html_url'
```

또는 GitHub 웹에서 `Settings → Pages`.

---

관련 운영 문서: `01.kakaoimpact-AX/_workspace/deploy-security/`
