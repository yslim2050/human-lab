# HUMAN LAB 홈페이지 (GitHub Pages / Jekyll)

KAIST 인간-기계 상호작용 연구실(HUMAN Lab) 홈페이지를 GitHub Pages에서 운영할 수 있도록
Jekyll 정적 사이트로 재구성한 것입니다. 색상·치수는 기존 사이트에서 직접 추출한 값을
그대로 사용했습니다.

---

## 1. 배포 방법

### 1-1. 저장소 만들기
1. GitHub에서 새 저장소를 만듭니다.
   - 주소를 `사용자이름.github.io` 로 하면 → `https://사용자이름.github.io` 로 열립니다.
   - 다른 이름(예: `human-lab`)으로 하면 → `https://사용자이름.github.io/human-lab` 로 열립니다.
2. 이 폴더의 **모든 파일**을 저장소 최상위에 올립니다.

### 1-2. 프로젝트 저장소일 때만 — baseurl 설정
저장소 이름을 `human-lab` 처럼 따로 지었다면 `_config.yml` 에서 한 줄만 고칩니다.

```yaml
baseurl: "/human-lab"
```

`사용자이름.github.io` 저장소라면 `baseurl: ""` 그대로 두면 됩니다.
(GitHub Actions 워크플로를 쓰면 이 값이 자동으로 채워지므로 건드리지 않아도 됩니다.)

### 1-3. Pages 켜기
저장소 → **Settings → Pages → Build and deployment → Source** 를
**GitHub Actions** 로 선택합니다. 포함된 `.github/workflows/pages.yml` 이 자동으로 빌드·배포합니다.

### 1-4. 커스텀 도메인 (선택)
Settings → Pages → Custom domain 에 도메인을 넣고, DNS에 CNAME 레코드를 추가하면
`human.kaist.ac.kr` 같은 주소도 연결할 수 있습니다. (KAIST 전산팀 협조 필요)

---

## 2. 내용 수정 방법

**모든 수정은 웹 브라우저에서 GitHub 저장소 파일을 직접 편집해도 됩니다.**
파일을 고쳐 커밋하면 1~2분 뒤 사이트에 반영됩니다.

### 2-1. 게시판에 글 올리기
게시판은 폴더 하나당 하나씩입니다. 해당 폴더에 `.md` 파일을 추가하기만 하면
목록에 자동으로 올라갑니다(최신순 정렬).

| 게시판 | 폴더 | 사이트 주소 |
|---|---|---|
| Notice | `_notice/` | `/notice/` |
| Awards (News & Article) | `_news/` | `/awards/` |
| Projects | `_projects/` | `/projects/` |
| Consulting | `_consulting/` | `/consulting/` |
| Lectures | `_lectures/` | `/lab-intro/lectures/` |
| Gallery | `_gallery/` | `/lab-intro/gallery/` |

파일 이름은 `연-월-일-제목.md` 형식을 권장합니다. 내용 형식:

```markdown
---
title: "게시물 제목"
date: 2026-10-26
writer: 관리자
---

본문을 여기에 씁니다. 마크다운 문법을 쓸 수 있습니다.

- 목록도 가능
- **굵게**, [링크](https://example.com)

![사진 설명](/assets/img/gallery/사진파일.jpg)
```

사진·첨부파일은 `assets/img/` 또는 `assets/files/` 에 올린 뒤 위처럼 연결하면 됩니다.

### 2-2. 논문·특허·학위논문 목록
`_data/publications.yml` 한 파일에서 모두 관리합니다.
그룹별 목록 맨 위에 한 줄 추가하면 됩니다. HTML 태그를 쓸 수 있습니다.

```yaml
international_journal:
  - '저자들, <strong>Yong-Hwa Park</strong> (2026). 논문 제목, 저널명, 권, 페이지. <strong>(SCIE, IF 0.0)</strong>'
```

사용 가능한 그룹 이름:
`international_journal`, `international_conference`, `domestic_journal`,
`domestic_conference`, `invited`, `patents`, `ms_thesis`, `phd_dissertation`

### 2-3. 구성원 명단
`_data/members.yml` 에서 그룹(`professor`, `researcher`, `phd`, `master`, `alumni`, `staff`)별로 관리합니다.

```yaml
phd:
  - name: "홍길동 (Hong, Gil Dong)"
    position: "Ph.D. Candidate"
    education:
      - "2024 BS Mechanical Engineering, KAIST"
    interest: "Structural Health Monitoring"
    hobby: "등산"
    email: "gdhong@kaist.ac.kr"
```

### 2-4. 메뉴 구조
`_data/nav.yml` 을 고치면 상단 탭과 좌측 서브메뉴가 함께 바뀝니다.

### 2-5. 일반 페이지 글
`lab-intro/`, `research/` 폴더의 `.html` 파일을 직접 편집합니다.
본문에서 쓸 수 있는 스타일:

- `<h3>소제목</h3>` → 파란 짧은 선이 붙은 섹션 제목
- `<ul class="dots"> <li>항목</li> </ul>` → 점 목록
- `<a class="link" href="...">링크</a>` → 파란 링크

---

## 3. 사진 넣기

현재 사진은 모두 비워 두었습니다(요청에 따라). 넣는 위치는 다음과 같습니다.

| 용도 | 넣을 곳 |
|---|---|
| 메인 비주얼 (984×353) | `assets/img/main/` → `_layouts/home.html` 의 `.visual-slot` 교체 |
| 구성원 사진 (120×150) | `assets/img/members/` → `_layouts/members.html` 의 `.photo-slot` 교체 |
| 게시물 사진 | `assets/img/gallery/` 등 → 게시물 본문에서 직접 링크 |
| PDF 등 첨부 | `assets/files/` |

---

## 4. 색상 — 원본 추출값

`assets/css/style.css` 상단의 CSS 변수에 정리되어 있습니다.
전체 색은 이 변수만 고치면 한 번에 바뀝니다.

| 용도 | 값 |
|---|---|
| 헤더 바탕 / 포인트 | `#0579cd` |
| 좌측 서브메뉴 헤더 | `#0570be` ~ `#046ab4` |
| 푸터 / SITE LINK 제목 | `#08112a` |
| 포인트 노랑 (more 버튼, 활성 탭) | `#ffb400` (탭 그라데이션 윗부분 `#f2ab01`) |
| 상단 메뉴 글자 | `#424242` (16px / 700) |
| 페이지 대제목 | `#252525` (30px / 700) |
| 본문 글자 | `#8a8a8a` / `#646464` / `#333333` |
| 좌측 메뉴 비활성 / 활성 | `#444444` / `#0579cd` (바탕 `#f8f8f8`) |
| 브레드크럼 | `#7e7f7f` (11px / 700) |
| 푸터 글자 | `#97989e` |
| 구분선 | `#dddddd`, `#e9e9e9`, `#d9d9d9` |

레이아웃 치수도 원본과 동일합니다: 본문 폭 1000px, 헤더 124px, 상단 메뉴 65px,
좌측 메뉴 240px, 본문 영역 722px, 폰트 Noto Sans KR.

---

## 5. 로컬에서 미리보기 (선택)

```bash
bundle install
bundle exec jekyll serve
# http://localhost:4000
```

---

## 6. 원본 대비 달라진 점

- **방문자 카운터**: 원본은 서버에서 집계했습니다. 정적 사이트에서는 불가능하여
  브라우저 저장소 기반으로 대체했습니다. 실제 집계가 필요하면 GoatCounter나
  Google Analytics를 `_includes/footer.html` 에 넣으세요.
- **LOGIN / JOIN**: 회원 기능은 정적 사이트에서 동작하지 않아 제외했습니다.
  필요하면 GitHub 저장소 권한으로 관리자를 나누는 방식을 권합니다.
- **게시판 검색**: 원본은 서버 검색이었고, 여기서는 현재 목록 안에서 제목을
  걸러내는 방식입니다. 글이 많아지면 Lunr.js 같은 검색 스크립트를 붙일 수 있습니다.
- **사진**: 요청에 따라 모두 자리만 비워 두었습니다.
