# IEN-25 README 개편 구현 계획

> **작업자 필수 절차:** `superpowers:subagent-driven-development` 또는 `superpowers:executing-plans`를 사용해 각 작업을 순서대로 수행한다.

**목표:** 마이크로사이트 `/about`의 최신 소개 정보를 누락 없이 반영한 GitHub 프로필 README를 만든다.

**구성:** 단일 `readme.md` 안에서 대표 이미지, 소개, 학력과 기술, 발자취, 대학 활동, 장비, 연락처를 순서대로 제공한다. 학력·주요 발자취·대학 활동은 표로 정리하고, 작업 장비는 긴 설명의 가독성을 위해 분류별 목록으로 정리한다. 기존 `.gitignore` 변경은 작업 범위에서 제외한다.

**기술:** GitHub 호환 Markdown, 제한적인 HTML 배지

## 전체 제약

- 한국어 원문을 사용하고 기술명·제품명·서비스명은 고유 표기를 유지한다.
- `/about`의 항목과 설명을 모두 기본 상태에서 노출한다.
- 영어 번역문, 애니메이션, 웹 전용 카드 UI는 옮기지 않는다.
- 기존 `.gitignore` 변경을 수정하거나 커밋하지 않는다.

---

### Task 1: README 전체 개편

**파일:**

- 수정: `readme.md`

**입력:**

- `../ienlab_react_microsite/src/ui/public/about/AboutScreen.tsx`
- `../ienlab_react_microsite/src/locales/ko/strings.json`

**결과:**

- 상단 대표 이미지와 소개 문구
- 학력 2건과 기술 스택 3개 그룹
- 주요 발자취 7건
- 대학 활동 9건
- 작업 장비 10건과 설명
- 포트폴리오, GitHub, Instagram, 이메일, 블로그 링크

- [x] **1단계: `readme.md`를 다음 섹션 순서로 교체**

```text
대표 이미지
안녕하세요, 아이엔입니다 👋
About
학력 및 기술 스택
기억할 만한 순간들
대학 활동
작업 장비
연락처
```

- [x] **2단계: 원본 항목 수를 정적 검사**

실행:

```bash
rg -c '^\| 20' readme.md
rg -c '^### ' readme.md
```

예상 결과: 연도 기반 표 행 18개, 장비 분류 제목 4개 이상이다.

- [x] **3단계: Markdown 공백 오류 검사**

실행:

```bash
git diff --check -- readme.md
```

예상 결과: 출력 없이 종료 코드 0이다.

- [x] **4단계: 원본과 README를 수동 대조**

다음 항목 수를 확인한다.

```text
학력 2
기술 스택 그룹 3
주요 발자취 7
대학 활동 9
작업 장비 10
연락처 5
```

### Task 2: 최종 변경 범위 확인

**파일:**

- 확인: `readme.md`
- 확인: `docs/superpowers/specs/2026-07-24-ien-25-readme-redesign.md`
- 확인: `docs/superpowers/plans/2026-07-24-ien-25-readme-redesign.md`

- [x] **1단계: 변경 파일 확인**

실행:

```bash
git diff --name-only 9150f36..HEAD
git diff --check 9150f36..HEAD -- readme.md docs/superpowers/specs/2026-07-24-ien-25-readme-redesign.md docs/superpowers/plans/2026-07-24-ien-25-readme-redesign.md
```

예상 결과: README와 설계·계획 문서 세 파일만 출력되고, 공백 오류 없이 종료 코드 0이다.

- [x] **2단계: 링크 형식 확인**

실행:

```bash
rg -n 'https://www\.ien\.zone/project|https://github\.com/ienground|https://www\.instagram\.com/ienlab|mailto:my@ien\.zone|https://blog\.ien\.zone' readme.md
```

예상 결과: 연락처 링크 5종이 모두 검색된다.
