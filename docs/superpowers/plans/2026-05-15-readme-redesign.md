# README Redesign Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** GitHub 프로필 README(`k-haechan/k-haechan`)를 spec 정의대로 6개 섹션으로 재구성하고, snake animation 자동화 워크플로우를 추가한다.

**Architecture:** 단일 `README.md` 파일을 섹션별로 점진적으로 재작성한다(Hero → Featured Projects → Skills → Activity → Experience & Certs → Contact). HTML `<table>` 태그로 카드형 레이아웃을 안정적으로 렌더링하고, 외부 SVG API와 1개의 GitHub Actions 워크플로우(snake)로 동적 신호를 자동화한다. 각 섹션이 독립 commit이 되어 중간 시점에도 README가 항상 일관된 상태를 유지한다.

**Tech Stack:** Markdown · HTML(table layout) · GitHub Actions(`Platane/snk@v3`) · 외부 SVG API(github-readme-stats, mazassumnida, capsule-render, komarev, devicon, shields)

**Spec:** `docs/superpowers/specs/2026-05-15-readme-redesign-design.md`

---

## File Structure

| Path | Action | Purpose |
|---|---|---|
| `README.md` | Replace | 새 6개 섹션 구조의 README (Task 1에서 전체 덮어쓰기, 이후 task에서 섹션 추가) |
| `.github/workflows/snake.yml` | Create | 매일 snake animation SVG 생성 후 `output` 브랜치에 푸시 |

`.github/` 디렉터리가 존재하지 않을 수 있음 → Task 7에서 생성 포함.

---

## Task 0: Preflight — Resolve Open Questions

**Files:** None (read-only checks + 결정 기록)

- [ ] **Step 1: SSAFY-STUDY 메인 저장소 확정**

다음 두 후보 중 README에 링크할 정식 메인을 결정한다:

```
A. https://github.com/k-haechan/study_backend       (개인 저장소)
B. https://github.com/ssafy-spring-study/<repo>    (Organization)
```

판단 방법:
- 두 저장소를 브라우저에서 열어 commit 활동·README 완성도·실제 배포 코드 위치 비교
- 사용자가 SSAFY 동기들에게 공식적으로 공유한 저장소가 어느 쪽인지 확인

결정된 URL을 메모해 둔다 (Task 2에서 직접 사용).

**Result:** `RESOLVED_REPO_URL = <decided URL>` ← Task 2에서 이 값으로 치환.

- [ ] **Step 2: Git remote 확인**

```bash
git -C /Users/hc/WorkPlace2/githubpage/k-haechan remote -v
```

Expected output 후보:
- `origin  https://github.com/k-haechan/k-haechan.git (fetch)` ✓ 프로필 README 저장소 — 진행
- 다른 URL → 사용자에게 확인 후 진행 판단 (이 디렉터리가 정말 프로필 README repo인지 점검)

- [ ] **Step 3: 현재 README.md 상태 확인**

```bash
git -C /Users/hc/WorkPlace2/githubpage/k-haechan status
git -C /Users/hc/WorkPlace2/githubpage/k-haechan diff README.md | head -20
```

`README.md`에 uncommitted 변경이 있으면, Task 1이 *전체 덮어쓰기* 하므로 그 변경은 자동으로 폐기된다. 보존하고 싶은 부분이 있다면 Task 1 시작 전에 수동으로 메모.

---

## Task 1: Build Hero Section (전체 README 덮어쓰기)

**Files:**
- Modify (overwrite): `/Users/hc/WorkPlace2/githubpage/k-haechan/README.md`

이 task는 README 전체를 새 skeleton + Hero section만 포함하는 형태로 *덮어쓴다*. 다음 task들이 차례로 섹션을 채워나간다.

- [ ] **Step 1: README.md 전체를 다음 내용으로 덮어쓰기**

```markdown
<!-- Header banner -->
<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=12&height=180&section=header&fontSize=0" alt="header"/>
</p>

<div align="center">

# Hi there, I'm Haechan Kim 👋

> "문제의 본질을 정확히 이해하고,
>  다양한 경험에서 비롯한 적절한 도구와 방법으로 빠르게 해결합니다."

🔭 **현재 관심사:** AI 에이전트 도구로 개발·배포 프로세스 자동화
&nbsp;&nbsp;&nbsp;&nbsp;· Claude Code · Codex CLI · Gemini CLI
&nbsp;&nbsp;&nbsp;&nbsp;· superpowers / gstack / bmad — Skill 프레임워크 분석

<p>
  <a href="https://cheer-for-your-life.tistory.com/" target="_blank"><img src="https://img.shields.io/badge/Blog-FF5722?style=for-the-badge&logo=blogger&logoColor=white" alt="Blog"></a>
  <a href="mailto:gibbm1127@naver.com"><img src="https://img.shields.io/badge/Email-007396?style=for-the-badge&logo=naver&logoColor=white" alt="Email"></a>
  <a href="https://solved.ac/gocks0203" target="_blank"><img src="http://mazassumnida.wtf/api/v2/generate_badge?boj=gocks0203" alt="Solved.ac"></a>
  <img src="https://komarev.com/ghpvc/?username=k-haechan&style=for-the-badge&color=blueviolet" alt="Profile Views"/>
</p>

</div>

---

<!-- TODO(task-2): Featured Projects -->
<!-- TODO(task-3): Skills & Learning -->
<!-- TODO(task-4): Activity -->
<!-- TODO(task-5): Experience & Certifications -->
<!-- TODO(task-6): Contact -->
```

- [ ] **Step 2: 로컬에서 마크다운 렌더링 확인**

VS Code: `Cmd+Shift+V` (마크다운 프리뷰)
또는 `grip` 사용:
```bash
pip install grip 2>/dev/null || true
grip /Users/hc/WorkPlace2/githubpage/k-haechan/README.md
# 브라우저에서 http://localhost:6419 열기
```

확인 항목:
- 헤더 배너 이미지가 로드된다
- 인사말과 태그라인이 중앙 정렬된다
- "현재 관심사" 줄들이 들여쓰기되어 표시된다
- 4개 뱃지(Blog · Email · Solved.ac · Profile Views)가 한 줄에 정렬된다

- [ ] **Step 3: Commit**

```bash
git -C /Users/hc/WorkPlace2/githubpage/k-haechan add README.md
git -C /Users/hc/WorkPlace2/githubpage/k-haechan commit -m "feat: rebuild hero section per redesign spec"
```

---

## Task 2: Build Featured Projects Section

**Files:**
- Modify: `/Users/hc/WorkPlace2/githubpage/k-haechan/README.md`

- [ ] **Step 1: `<!-- TODO(task-2): Featured Projects -->` 라인을 다음 내용으로 교체**

`<RESOLVED_REPO_URL>` 부분을 Task 0 Step 1에서 결정한 SSAFY-STUDY 메인 저장소 URL로 *반드시* 교체한다.

```markdown
<h2 align="center">🌟 Featured Projects</h2>

<table>
<tr>
<td colspan="2">

### 🌟 SSAFY-STUDY Platform
**AI 비동기 학습 플랫폼 — 20명+ 운영 중 · 진행형**
[ [Repo](<RESOLVED_REPO_URL>) · [Live Demo](https://www.ssafy-study.site/) ]

강의 영상·학습 자료를 업로드하면 AI가 자동으로 퀴즈를 생성하고, 개인별 학습 진척을 관리하는 비동기 학습 플랫폼.
GitHub Organization 기반으로 Issue·PR을 통한 과제·코드리뷰까지 병행하는 실습형 운영 구조.

**💡 Why** &nbsp; 강의식 스터디의 참여율 저하·일정 충돌 문제를 해결하기 위해, "비동기 학습 + 자동 퀴즈 + 실습형 PR 리뷰"라는 새로운 운영 구조를 직접 설계하고 플랫폼으로 구현. 결과적으로 20명+ 스터디원이 이탈 없이 학습을 이어가고 있음.

**🛠 Stack** &nbsp; `Spring Boot` `JPA` `Spring Security` `JWT` `MySQL` `Redis` `Next.js` `Groq API` `AWS (EC2·S3·RDS·CloudFront)` `Docker` `Terraform` `GitHub Actions`

**✨ Highlights**

① **AI 제공자 추상화 레이어 설계** — Spring AI + Gemini API 한국 리전 403 에러를 추적해 환경 제약이 원인임을 발견. Groq로 단순 교체가 아닌 Provider Abstraction Layer를 설계해, 비즈니스 로직 변경 없이 AI 제공자를 교체 가능한 구조로 완성.

② **DB 캐싱으로 AI 호출 비용·지연 동시 해결** — 동일 자료에 반복되는 AI 호출의 비용·지연 문제를 자료 단위 DB 캐싱으로 해결. 첫 호출 후 모든 동일 요청은 DB 즉시 반환.

③ **Spec-Driven Development(SDD) 적용** — `CLAUDE.md` / `plan.md` 기반 하네스 엔지니어링으로 개발 진행. 에이전트 의존성 배제, 멱등성 spec 설계로 1인 개발에서도 일관된 속도·품질 확보.

👤 **1인 개발** — 기획 · 백엔드 · 프론트엔드 · 인프라 · 스터디 운영 주도
📅 2026.03 – 진행 중

</td>
</tr>
<tr>
<td width="50%" valign="top">

### 📦 Cotree
*Code Only · 라이브 데모 종료*

[ [Repo](https://github.com/k-haechan/WEB3_4_SsamMuDan_BE) ]

인프런 형태 온라인 교육 플랫폼.

Spring Security + JWT 회원·인증 도메인 설계,
쿼리 최적화로 핵심 API 응답 **2배 이상** 개선.

**Stack:** `Spring Boot` `JWT` `MySQL` `AWS`
**📅** 2025.03 – 04

</td>
<td width="50%" valign="top">

### 📦 SNS1
*Code Only · 라이브 데모 종료*

[ [Repo](https://github.com/k-haechan/sns1-server) ]

1인 개발 SNS 서비스.

기획부터 인프라·배포까지 1인 책임.
Terraform/GHA로 IaC·CI/CD 자동화.
**AWS Java SDK 버그 발견·재현·제보**.

**Stack:** `Spring Boot` `Terraform` `AWS`
**📅** 2025.07 – 08

</td>
</tr>
</table>

---
```

- [ ] **Step 2: `<RESOLVED_REPO_URL>` placeholder가 실제 URL로 교체되었는지 확인**

```bash
grep -n "RESOLVED_REPO_URL" /Users/hc/WorkPlace2/githubpage/k-haechan/README.md
```

Expected: 출력 없음 (모든 placeholder가 실제 URL로 교체됨).

- [ ] **Step 3: 마크다운 프리뷰로 렌더링 확인**

확인 항목:
- 메인 카드(SSAFY-STUDY)가 가로 풀폭으로 렌더링된다
- Cotree·SNS1 보조 카드가 좌우 50%씩 분할되어 표시된다
- 모든 링크가 클릭 가능
- 백틱(`)으로 감싼 기술 스택이 코드 스타일로 표시된다

- [ ] **Step 4: Commit**

```bash
git -C /Users/hc/WorkPlace2/githubpage/k-haechan add README.md
git -C /Users/hc/WorkPlace2/githubpage/k-haechan commit -m "feat: add featured projects section (SSAFY-STUDY + 2 supporting cards)"
```

---

## Task 3: Build Skills & Learning Section

**Files:**
- Modify: `/Users/hc/WorkPlace2/githubpage/k-haechan/README.md`

- [ ] **Step 1: `<!-- TODO(task-3): Skills & Learning -->` 라인을 다음 내용으로 교체**

```markdown
<h2 align="center">🚀 Skills & Learning</h2>

<table align="center">
  <tr>
    <td align="center" width="160"><b>Languages</b></td>
    <td>
      <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/java/java-original.svg" width="36" alt="Java"/>
      <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/python/python-original.svg" width="36" alt="Python"/>
      <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/cplusplus/cplusplus-original.svg" width="36" alt="C/C++"/>
    </td>
  </tr>
  <tr>
    <td align="center"><b>Backend</b></td>
    <td>
      <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/spring/spring-original.svg" width="36" alt="Spring Boot"/>
      &nbsp;Spring Security · JPA
    </td>
  </tr>
  <tr>
    <td align="center"><b>Frontend</b></td>
    <td>
      <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/nextjs/nextjs-original.svg" width="36" alt="Next.js"/>
      <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/html5/html5-original.svg" width="36" alt="HTML"/>
      &nbsp;Thymeleaf
    </td>
  </tr>
  <tr>
    <td align="center"><b>Database</b></td>
    <td>
      <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/mysql/mysql-original.svg" width="36" alt="MySQL"/>
      <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/redis/redis-original.svg" width="36" alt="Redis"/>
    </td>
  </tr>
  <tr>
    <td align="center"><b>Infra & DevOps</b></td>
    <td>
      <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/amazonwebservices/amazonwebservices-original-wordmark.svg" width="36" alt="AWS"/>
      <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/docker/docker-original.svg" width="36" alt="Docker"/>
      <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/terraform/terraform-original.svg" width="36" alt="Terraform"/>
      &nbsp;<sub>EC2 · S3 · RDS · CloudFront</sub>
    </td>
  </tr>
  <tr>
    <td align="center"><b>Test & CI/CD</b></td>
    <td>
      <img src="https://img.shields.io/badge/JUnit5-25A162?style=flat-square&logo=junit5&logoColor=white" alt="JUnit5"/>
      <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/github/github-original.svg" width="36" alt="GitHub Actions"/>
      &nbsp;Mockito · Jacoco
    </td>
  </tr>
  <tr>
    <td align="center"><b>🌱 Currently<br>Exploring</b></td>
    <td>
      <code>Claude Code</code> · <code>superpowers</code> · <code>gstack</code> · <code>bmad</code><br>
      <sub>AI Agent Skill 프레임워크 · Spec-Driven Development</sub>
    </td>
  </tr>
</table>

---
```

⚠️ **JUnit 아이콘 결정:** Devicon에는 안정적인 JUnit 아이콘이 없으므로 처음부터 `shields.io` 뱃지로 작성. 다른 항목과 시각 크기를 맞추기 위해 `style=flat-square` 사용.

- [ ] **Step 2: 마크다운 프리뷰로 렌더링 확인**

확인 항목:
- 7개 행(Languages / Backend / Frontend / Database / Infra & DevOps / Test & CI/CD / Currently Exploring)이 모두 표시된다
- 모든 devicon 아이콘이 로드된다
- "Currently Exploring" 행이 `<code>` 스타일로 다른 행과 시각적으로 구별된다

- [ ] **Step 3: Commit**

```bash
git -C /Users/hc/WorkPlace2/githubpage/k-haechan add README.md
git -C /Users/hc/WorkPlace2/githubpage/k-haechan commit -m "feat: add skills & learning section with currently-exploring row"
```

---

## Task 4: Build Activity Section

**Files:**
- Modify: `/Users/hc/WorkPlace2/githubpage/k-haechan/README.md`

- [ ] **Step 1: `<!-- TODO(task-4): Activity -->` 라인을 다음 내용으로 교체**

```markdown
<h2 align="center">📊 Activity</h2>

<div align="center">

<a href="https://github.com/k-haechan">
  <img src="https://github-readme-stats.vercel.app/api?username=k-haechan&show_icons=true&theme=radical" alt="GitHub Stats" height="180" />
</a>
<a href="https://github.com/k-haechan">
  <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=k-haechan&layout=compact&theme=radical" alt="Top Languages" height="180" />
</a>

<br/>

<a href="https://github.com/k-haechan">
  <img src="https://github-readme-streak-stats.herokuapp.com/?user=k-haechan&theme=radical" alt="GitHub Streak" height="180" />
</a>
<a href="https://solved.ac/gocks0203">
  <img src="http://mazassumnida.wtf/api/v2/generate_badge?boj=gocks0203" alt="Solved.ac" height="180" />
</a>

<br/><br/>

<a href="https://github.com/k-haechan">
  <img src="https://raw.githubusercontent.com/k-haechan/k-haechan/output/github-contribution-grid-snake.svg" alt="Contribution Snake" />
</a>

</div>

---
```

- [ ] **Step 2: 마크다운 프리뷰로 렌더링 확인**

확인 항목:
- GitHub Stats / Top Langs 위젯이 좌우로 정렬된다
- Streak / Solved.ac 위젯이 좌우로 정렬된다
- Snake animation 이미지가 *아직 깨져 표시*되는 것은 정상 — Task 7·8에서 워크플로우가 SVG를 생성·푸시한 뒤에 보임

- [ ] **Step 3: Commit**

```bash
git -C /Users/hc/WorkPlace2/githubpage/k-haechan add README.md
git -C /Users/hc/WorkPlace2/githubpage/k-haechan commit -m "feat: add activity section with stats, streak, solved.ac, and snake placeholder"
```

---

## Task 5: Build Experience & Certifications Section

**Files:**
- Modify: `/Users/hc/WorkPlace2/githubpage/k-haechan/README.md`

- [ ] **Step 1: `<!-- TODO(task-5): Experience & Certifications -->` 라인을 다음 내용으로 교체**

```markdown
<h2 align="center">🎓 Experience & Certifications</h2>

### 🏫 Education

**국민대학교** &nbsp; *정보보안암호수학과* &nbsp; `2018.03 – 2024.02`

- C/C++ 기반 암호 모듈 최적화, PKI 인증·서명 로직 구현
- Python 기반 통계 분석·전처리·시각화

### 💼 Programs

**프로그래머스 데브코스** &nbsp; *클라우드 기반 백엔드 엔지니어링* &nbsp; `2024.11 – 2025.04`

- Spring Framework·MySQL 기반 백엔드 개발
- Terraform AWS 인프라 코드 관리(IaC)
- GitHub CI/CD 파이프라인·RESTful API 협업

**삼성 청년 SW AI 아카데미 (SSAFY)** &nbsp; *SW 역량 강화* &nbsp; `2026.01 – 2026.03`

- Java·Python 알고리즘·자료구조 집중 학습
- CS 핵심 개념 체계화, 팀 프로젝트 협업·백엔드 개발

### 📜 Certifications

<p align="center">
  <img src="https://img.shields.io/badge/정보처리기사-0078D4?style=for-the-badge&logoColor=white" alt="정보처리기사"/>
  <img src="https://img.shields.io/badge/SQLD-CC2927?style=for-the-badge&logo=microsoftsqlserver&logoColor=white" alt="SQLD"/>
  <img src="https://img.shields.io/badge/빅데이터분석기사-4479A1?style=for-the-badge&logoColor=white" alt="빅데이터 분석기사"/>
</p>

---
```

- [ ] **Step 2: 마크다운 프리뷰로 렌더링 확인**

확인 항목:
- Education / Programs / Certifications 3개 하위 섹션이 모두 표시된다
- 자격증 뱃지 3개가 정상 렌더링된다 (한글 텍스트 포함 뱃지에서 한글이 깨지지 않는지)

⚠️ shields.io 뱃지에서 한글이 깨지는 경우(드물지만 발생 가능) 다음으로 교체:
```html
<img src="https://img.shields.io/badge/Information%20Processing%20Engineer-0078D4?style=for-the-badge" alt="정보처리기사"/>
```

- [ ] **Step 3: Commit**

```bash
git -C /Users/hc/WorkPlace2/githubpage/k-haechan add README.md
git -C /Users/hc/WorkPlace2/githubpage/k-haechan commit -m "feat: add experience & certifications section"
```

---

## Task 6: Build Contact Section

**Files:**
- Modify: `/Users/hc/WorkPlace2/githubpage/k-haechan/README.md`

- [ ] **Step 1: `<!-- TODO(task-6): Contact -->` 라인을 다음 내용으로 교체**

```markdown
<h2 align="center">📬 Contact</h2>

<div align="center">

> "문제·아이디어·협업 — 무엇이든 환영합니다."

<p>
  <a href="mailto:gibbm1127@naver.com"><img src="https://img.shields.io/badge/Email-gibbm1127@naver.com-007396?style=for-the-badge&logo=naver&logoColor=white" alt="Email"></a>
  <a href="https://github.com/k-haechan"><img src="https://img.shields.io/badge/GitHub-@k--haechan-181717?style=for-the-badge&logo=github&logoColor=white" alt="GitHub"></a>
  <a href="https://cheer-for-your-life.tistory.com/"><img src="https://img.shields.io/badge/Blog-cheer--for--your--life-FF5722?style=for-the-badge&logo=blogger&logoColor=white" alt="Blog"></a>
  <a href="https://portfolio.haechan.site/"><img src="https://img.shields.io/badge/Portfolio-haechan.site-4CAF50?style=for-the-badge&logo=googlechrome&logoColor=white" alt="Portfolio"></a>
</p>

</div>
```

- [ ] **Step 2: 모든 TODO 마커가 제거되었는지 확인**

```bash
grep -n "TODO(task-" /Users/hc/WorkPlace2/githubpage/k-haechan/README.md
```

Expected: 출력 없음 (모든 섹션이 채워짐).

- [ ] **Step 3: 마크다운 프리뷰로 렌더링 확인**

확인 항목:
- CTA 인용구가 중앙 정렬된다
- 4개 채널 뱃지가 한 줄에 정렬된다 (또는 자연스럽게 줄바꿈)
- 모든 링크가 클릭 가능

- [ ] **Step 4: Commit**

```bash
git -C /Users/hc/WorkPlace2/githubpage/k-haechan add README.md
git -C /Users/hc/WorkPlace2/githubpage/k-haechan commit -m "feat: add contact section"
```

---

## Task 7: Add Snake Animation Workflow

**Files:**
- Create: `/Users/hc/WorkPlace2/githubpage/k-haechan/.github/workflows/snake.yml`

- [ ] **Step 1: `.github/workflows` 디렉터리 생성**

```bash
mkdir -p /Users/hc/WorkPlace2/githubpage/k-haechan/.github/workflows
```

- [ ] **Step 2: `snake.yml` 파일 생성**

다음 내용으로 `/Users/hc/WorkPlace2/githubpage/k-haechan/.github/workflows/snake.yml` 작성:

```yaml
name: Generate Snake Animation

on:
  schedule:
    - cron: "0 0 * * *"  # 매일 00:00 UTC
  workflow_dispatch:
  push:
    branches:
      - main

permissions:
  contents: write

jobs:
  generate:
    runs-on: ubuntu-latest
    steps:
      - name: Generate snake SVG
        uses: Platane/snk@v3
        with:
          github_user_name: k-haechan
          outputs: |
            dist/github-contribution-grid-snake.svg

      - name: Push to output branch
        uses: crazy-max/ghaction-github-pages@v3
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

핵심 동작:
- `Platane/snk@v3`이 `k-haechan`의 contribution graph를 SVG로 생성해 `dist/`에 저장
- `crazy-max/ghaction-github-pages@v3`가 `dist/` 내용을 `output` 브랜치 root로 업로드
- 결과 SVG는 `https://raw.githubusercontent.com/k-haechan/k-haechan/output/github-contribution-grid-snake.svg`에서 접근 가능 (Task 4 Activity 섹션이 참조하는 URL)

- [ ] **Step 3: Commit**

```bash
git -C /Users/hc/WorkPlace2/githubpage/k-haechan add .github/workflows/snake.yml
git -C /Users/hc/WorkPlace2/githubpage/k-haechan commit -m "ci: add snake animation workflow"
```

---

## Task 8: Push and Verify on GitHub

**Files:** None (push + browser verification)

- [ ] **Step 1: 모든 커밋을 origin에 push**

```bash
git -C /Users/hc/WorkPlace2/githubpage/k-haechan push origin main
```

Expected: Task 1~7의 7개 commit이 모두 origin/main에 반영됨.

- [ ] **Step 2: snake 워크플로우 실행 확인**

`push to main` 트리거가 워크플로우를 자동으로 실행한다.
GitHub 웹에서 `https://github.com/k-haechan/k-haechan/actions`에 접속해 "Generate Snake Animation" 실행이 시작되는지 확인.

자동 실행이 시작되지 않으면 수동 실행:
- Actions 탭 → "Generate Snake Animation" 워크플로우 → "Run workflow" 버튼 클릭

워크플로우 완료 (~1분) 후 다음 확인:
- `output` 브랜치가 생성되었는지: `https://github.com/k-haechan/k-haechan/tree/output`
- `output` 브랜치에 `github-contribution-grid-snake.svg` 파일이 존재하는지
- `https://raw.githubusercontent.com/k-haechan/k-haechan/output/github-contribution-grid-snake.svg` URL이 200으로 SVG를 반환하는지

- [ ] **Step 3: 프로필 페이지 시각 확인**

브라우저에서 `https://github.com/k-haechan` 접속.

확인 항목 (위에서 아래로):

| 섹션 | 확인 사항 |
|---|---|
| ① Hero | 헤더 배너 / 인사 / 태그라인 / 현재 관심사 / 4개 뱃지(Profile Views 포함) |
| ② Featured Projects | SSAFY-STUDY 메인 카드 가로 풀폭, Cotree·SNS1 보조 카드 좌우 50% |
| ③ Skills & Learning | 7개 행 모두 정상 (특히 JUnit5 뱃지 정상 표시) |
| ④ Activity | Stats / Top Langs / Streak / Solved.ac + Snake animation |
| ⑤ Experience & Certs | Education / Programs / Certifications |
| ⑥ Contact | CTA + 4개 채널 뱃지 |

- [ ] **Step 4: 깨진 이미지 / 레이아웃 이슈 발견 시 수정**

자주 발생하는 이슈와 수정법:

**Capsule render 색감이 radical 테마와 불일치:**
- `customColorList=12`를 다른 인덱스(1~30 중)로 시도
- 또는 직접 색상 지정: `color=ee5a92,9b6dff` (radical 핑크/퍼플)

**Streak stats heroku 슬립 인스턴스 첫 로드 지연:**
- 잠시 후 새로고침. 정상 동작.

**Snake SVG가 표시 안 됨:**
- `output` 브랜치 존재 확인
- `https://raw.githubusercontent.com/k-haechan/k-haechan/output/github-contribution-grid-snake.svg` 직접 접근 시도
- 워크플로우 로그 확인 (Actions 탭)

**한글 자격증 뱃지 깨짐:**
- shields.io 뱃지의 한글 인코딩 문제일 가능성. URL 인코딩 적용 또는 영문 표기로 교체

각 수정은 별도 커밋으로:
```bash
git -C /Users/hc/WorkPlace2/githubpage/k-haechan add README.md
git -C /Users/hc/WorkPlace2/githubpage/k-haechan commit -m "fix: <one-line description>"
git -C /Users/hc/WorkPlace2/githubpage/k-haechan push origin main
```

- [ ] **Step 5: 최종 확인 — Out of Scope 항목 미포함 검증**

```bash
grep -i "trophy\|tistory.*post\|now\|copyright\|©\|010-" /Users/hc/WorkPlace2/githubpage/k-haechan/README.md
```

Expected: 의도하지 않은 항목 미포함 확인 (Tistory blog 링크는 Hero·Contact에 정적 링크로만 존재해야 하며, 자동 임베드 워크플로우/RSS 호출 코드는 없어야 함).

---

## Self-Review Checklist (실행 전 마지막 확인)

- [ ] Spec의 모든 섹션(Hero / Featured Projects / Skills & Learning / Activity / Experience & Certs / Contact)이 task로 매핑되었다
- [ ] Spec의 자동화 인프라(snake workflow)가 Task 7로 추가된다
- [ ] Spec의 Out of Scope 항목(Tistory 자동 피드, Trophy, 전화번호, 저작권 표기, Now 섹션, 다국어 풀버전, 인터랙티브 컴포넌트)이 plan 어디에도 추가되지 않았다
- [ ] SSAFY-STUDY Repo 링크가 `<RESOLVED_REPO_URL>` placeholder가 아닌 실제 URL로 교체되도록 Task 0 Step 1에 명시되었다
- [ ] Snake workflow의 출력 경로(`dist/github-contribution-grid-snake.svg`)와 Activity 섹션의 참조 URL(`output/github-contribution-grid-snake.svg`)이 일치한다 (workflow가 `dist/` → `output` 브랜치 root로 업로드)
- [ ] 각 task가 독립 commit이 되어 중간 시점에도 README가 일관된 상태를 유지한다 (TODO 마커가 다음 task로 자연스럽게 연결됨)

---

## Risk & Rollback

이 변경은 단일 README 파일 + 단일 워크플로우의 추가/수정이며 모든 작업이 git commit으로 분리되어 있다. 문제 발견 시:

```bash
# 특정 task 시점으로 되돌리기
git -C /Users/hc/WorkPlace2/githubpage/k-haechan log --oneline
git -C /Users/hc/WorkPlace2/githubpage/k-haechan revert <commit-sha>
git -C /Users/hc/WorkPlace2/githubpage/k-haechan push origin main
```

원격 강제 푸시는 권장하지 않음 — 이미 공개된 README이므로 revert 커밋이 안전.

---

## Done Definition

- [ ] Task 1~7의 모든 commit이 origin/main에 push됨
- [ ] `https://github.com/k-haechan` 프로필에서 6개 섹션이 모두 정상 렌더링됨
- [ ] Snake animation이 `output` 브랜치에 생성되고 README에서 표시됨
- [ ] 깨진 이미지·레이아웃 이슈 0건
