# SH Cho 개인 사이트 — 운영 안내

이 폴더는 GitHub Pages에 그대로 올리면 동작하는 정적 사이트입니다.

```
sunghyo-cho-portfolio/
├── index.html       메인 이력 페이지 (한·영 통합)
├── notes.html       업계 노트 페이지
├── posts.json       노트 글 데이터 (이 파일만 편집하시면 새 글이 올라갑니다)
├── robots.txt       검색엔진 크롤러 정책
├── sitemap.xml      검색엔진 색인 도우미
└── README.md        본 안내문
```

---

## 1. 새 노트(뉴스+코멘트) 올리는 방법

`posts.json` 한 파일만 수정하시면 됩니다. 파일 안의 `posts` 배열 맨 앞에 다음 형식으로 객체 하나를 추가하십시오. (페이지는 자동으로 날짜 역순 정렬합니다.)

```json
{
  "date": "2026-05-12",
  "source": "Reuters",
  "url": "https://www.reuters.com/business/example/",
  "title_ko": "한국어 뉴스 제목",
  "title_en": "English news title",
  "comment_ko": "여기에 성효님의 코멘트를 한국어로 작성하십시오.",
  "comment_en": "Write your commentary in English here."
}
```

**주의 사항**

- 객체 사이는 쉼표(`,`)로 구분하되 마지막 객체 뒤에는 쉼표를 붙이지 마십시오. JSON 문법 오류가 가장 흔한 사고 원인입니다.
- 큰따옴표(`"`)만 허용되고 작은따옴표(`'`)는 안 됩니다.
- `date`는 `YYYY-MM-DD` 형식.
- `comment_ko`와 `comment_en`을 모두 채우셔도 되고, 한쪽만 채우셔도 됩니다. 비워 두면 해당 언어에서는 코멘트가 표시되지 않습니다.

GitHub 웹 편집기로 편집하시는 가장 쉬운 절차:
1. 저장소에서 `posts.json` 클릭
2. 우상단 연필 아이콘 클릭
3. 위 형식대로 객체 추가
4. 하단 `Commit changes` 클릭
5. 1~2분 후 사이트 반영

JSON 문법 검증이 걱정되시면 https://jsonlint.com 에 붙여넣어 검사 후 커밋하십시오.

---

## 2. 미리보기 (배포 전)

`index.html`이나 `notes.html`을 더블클릭하면 브라우저에서 열립니다. 단, `notes.html`의 글 목록은 로컬 파일에서는 보안 정책상 표시되지 않을 수 있습니다(브라우저가 `posts.json` 로드를 차단). 정상 표시는 GitHub Pages에 배포된 후 확인하시면 됩니다.

---

## 3. GitHub Pages 배포 (한 번만 하시면 됩니다)

### 3-1. GitHub 계정 준비
1. https://github.com 에서 계정 생성. 사용자명은 가능하면 본명에 가깝게 (예: `sunghyocho`).
2. 무료 플랜으로 충분합니다.

### 3-2. 저장소 생성
1. 우상단 `+` → **New repository**.
2. **Repository name** 에 `username.github.io` 형식 (예: `sunghyocho.github.io`). 이 이름이어야 사용자 페이지로 곧장 연결됩니다.
3. **Public** 으로 설정.
4. `Create repository`.

### 3-3. 파일 업로드
1. 새 저장소 화면 → **uploading an existing file** 링크.
2. 이 폴더 안의 모든 파일을 끌어다 놓기 (`index.html`, `notes.html`, `posts.json`, `robots.txt`, `sitemap.xml`, `README.md`).
3. `Commit changes`.

### 3-4. Pages 활성화
1. 저장소 **Settings** → **Pages**.
2. **Source**: `Deploy from a branch`, **Branch**: `main`, 폴더 `/ (root)`.
3. `Save`.
4. 1~2분 후 상단에 `Your site is live at https://username.github.io/` 표시.

---

## 4. 커스텀 도메인 sunghyocho.com 연결

### 4-1. 도메인 구매
- **Cloudflare Registrar** (https://dash.cloudflare.com) — 가장 저렴, 원가 판매.
- **가비아** (https://www.gabia.com) — 국내 결제 편의.

### 4-2. DNS 설정 (Cloudflare 기준)

```
Type   Name   Value
A      @      185.199.108.153
A      @      185.199.109.153
A      @      185.199.110.153
A      @      185.199.111.153
CNAME  www    [본인의 GitHub사용자명].github.io
```

### 4-3. GitHub 저장소에 도메인 등록
1. 저장소 → **Settings** → **Pages** → **Custom domain** 에 `sunghyocho.com` 입력 → `Save`.
2. 자동으로 `CNAME` 파일 생성됨.
3. DNS 전파 후 (10분 ~ 24시간) **Enforce HTTPS** 체크.

---

## 5. 검색엔진 등록 (선택, 권장)

1. **Google Search Console** (https://search.google.com/search-console)
   - 도메인 인증 → `https://sunghyocho.com/sitemap.xml` 제출.
2. **Naver 서치어드바이저** (https://searchadvisor.naver.com)
   - 동일 절차.

---

## 6. 점검 체크리스트

- [ ] index.html 더블클릭 시 정상 표시 (KO/EN 토글, 모바일 레이아웃)
- [ ] GitHub Pages 활성화 후 https://username.github.io 접속 정상
- [ ] notes.html 글 목록 정상 로드 (배포 후)
- [ ] sunghyocho.com 도메인 연결 후 HTTPS 정상
- [ ] Google Search Console에 sitemap.xml 제출

---

## 7. 자주 발생하는 사고와 대처

**Q. posts.json 수정 후 사이트가 깨졌습니다.**
A. JSON 문법 오류 가능성 99%. https://jsonlint.com 에 파일 내용을 붙여넣어 오류 위치 확인. 가장 흔한 원인: 마지막 객체 뒤 쉼표, 작은따옴표 사용, 큰따옴표 누락.

**Q. notes.html에 글이 "불러오지 못했습니다"라고 뜹니다.**
A. (1) `posts.json` 문법 오류 (위 답 참고), (2) `posts.json` 파일이 같은 폴더에 없음, (3) GitHub 커밋 직후 1~2분간 캐시 지연.

**Q. 도메인 연결 후 'NotServed' 또는 인증서 오류가 뜹니다.**
A. DNS 전파 시간이 부족합니다. 24시간까지 기다려 보십시오. 그래도 안 되면 GitHub Pages 설정에서 도메인을 한 번 지웠다가 다시 입력.

문의가 있으시면 언제든 말씀해 주십시오.
