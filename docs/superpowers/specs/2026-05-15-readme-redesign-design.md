# GitHub 프로필 README 재설계 — 설계 문서

**날짜:** 2026-05-15
**대상 저장소:** `k-haechan/k-haechan` (GitHub 프로필 README)
**현재 상태:** `README.md` 작성 진행 중 (uncommitted 변경 존재)

---

## 1. 목표 (Goals)

다양한 방문자에게 **"이 사람이 누구인지"를 5~10초 안에 전달하는** 프로필 README를 만든다. 현재 README는 시각적 구성과 기술 아이콘은 정돈되어 있으나, 본인의 정체성·관심사·실제 결과물이 잘 드러나지 않아 "다른 신입 백엔드 README와 구분되지 않는" 인상을 준다.

### 해결하려는 핵심 문제

- **"내가 누구인지 잘 안 드러남"** — 사용자가 자가진단한 가장 큰 약점.
- 가치관(보안·유지보수성)은 있으나 그 가치관의 *근거*가 보이지 않음.
- 실제 결과물(SSAFY-STUDY Platform 등 강력한 프로젝트)이 README에 반영되어 있지 않음.

### 성공 기준

- 첫 화면에서 본인의 정체성·관심사·연락 채널이 동시에 노출된다.
- Featured Projects 카드 1~3개가 일관된 시각 언어로 클릭을 유도한다.
- "현재 살아있는 페이지"라는 신호가 자동화된 위젯으로 자연스럽게 만들어진다.
- 채용 담당자의 키워드 매칭(기술 스택 검색)에 적합하게 카테고리가 정비되어 있다.

---

## 2. 사용자 컨텍스트 (Context)

| 항목 | 내용 |
|---|---|
| 이름 | 김해찬 |
| 전공 | 국민대학교 정보보안암호수학과 (2018.03 – 2024.02) |
| 현재 단계 | 취준생 (신입 준비 중) |
| 언어 전략 | 한국어 중심 (일부 영문 — 기술용어·섹션명) |
| 자동화 의욕 | 적극 도입 (GitHub Actions 기반 동적 위젯 환영) |
| 핵심 자산 | 대표 프로젝트 (SSAFY-STUDY Platform, Cotree, SNS1), 기술 블로그(저활동), Solved.ac 활동, 인턴십·자격증 (정보처리기사·SQLD·빅데이터분석기사) |

### 정체성 핵심

- "**문제의 본질을 정확히 이해하고, 다양한 경험에서 비롯한 적절한 도구와 방법으로 빠르게 해결하는 개발자**"
- **다리 정체성:** 정보보안암호수학 전공 → 백엔드/인프라 1인 개발 경험 → AI 에이전트 도구 적극 활용으로 확장
- 현재 관심: AI 에이전트 도구로 개발·배포 프로세스 자동화 (Claude Code · Codex CLI · Gemini CLI), superpowers / gstack / bmad 등 Skill 프레임워크 분석, 본인만의 에이전트 자동화 도구 제작

---

## 3. 채택한 접근 방식 (Approach B — 스토리텔링형 변형)

세 가지 후보(이력서형 / 스토리텔링형 / 쇼케이스형) 중 **스토리텔링형**을 채택하되, 유지보수 부담이 큰 "Now" 섹션은 제외하고 그 책임을 Hero의 "현재 관심사" 한 줄과 자동화된 Activity 섹션에 분산시킨다.

### 핵심 원칙

- **신선도가 위, 누적 자산이 아래** — 정적 README가 흔한 시대에 *방금 갱신된 페이지*는 그 자체로 차별화 신호.
- **자동 갱신 가능한 신호는 동적, 나머지는 의도적으로 정적** — Stale 위험 회피.
- **카드는 클릭 유도가 목적** — README에서 모든 걸 설명하지 않고, Repo·Demo·Portfolio로 가는 다리.

---

## 4. 전체 섹션 구조

```
┌─────────────────────────────────────────────────────────────┐
│ ① HERO         이름 + 태그라인 + 현재 관심사 + 뱃지            │
├─────────────────────────────────────────────────────────────┤
│ ② FEATURED PROJECTS  메인 1 (SSAFY-STUDY) + 보조 2          │
├─────────────────────────────────────────────────────────────┤
│ ③ SKILLS & LEARNING  6개 카테고리 + Currently Exploring     │
├─────────────────────────────────────────────────────────────┤
│ ④ ACTIVITY            Stats·Top Langs·Streak·Solved.ac·Snake│
├─────────────────────────────────────────────────────────────┤
│ ⑤ EXPERIENCE & CERTS  Education + Programs + Certifications │
├─────────────────────────────────────────────────────────────┤
│ ⑥ CONTACT             CTA + Email/GitHub/Blog/Portfolio     │
└─────────────────────────────────────────────────────────────┘
```

---

## 5. 섹션별 상세 설계

### ① Hero

**목적:** 첫 1.5초 안에 "누구·가치관·현재 관심사·어디서 더 볼 수 있는지" 전달.

**구성요소:**

1. **헤더 배너** — `capsule-render.vercel.app` 웨이브 헤더 (radical 색감과 조화)
2. **인사말** — `Hi there, I'm Haechan Kim 👋`
3. **태그라인 (인용블록):**
   > "문제의 본질을 정확히 이해하고, 다양한 경험에서 비롯한 적절한 도구와 방법으로 빠르게 해결합니다."
4. **현재 관심사 (3줄):**
   ```
   🔭 현재 관심사:
      AI 에이전트 도구로 개발·배포 프로세스 자동화
      · Claude Code · Codex CLI · Gemini CLI
      · superpowers / gstack / bmad — Skill 프레임워크 분석
   ```
5. **뱃지 행:** Blog · Email · Solved.ac · Profile Views (komarev)

**유지보수 정책:** 현재 관심사 한 줄은 6개월~1년 단위 수동 갱신.

---

### ② Featured Projects

**목적:** "이 사람이 무엇을 만들었고 왜 만들었는지"를 일관된 카드 형태로 노출.

**구조:** 2단 (메인 1 + 보조 2)

#### 메인 카드 — SSAFY-STUDY Platform

| 필드 | 값 |
|---|---|
| 제목 | 🌟 SSAFY-STUDY Platform |
| 부제 | AI 비동기 학습 플랫폼 — 20명+ 운영 중 · 진행형 |
| Repo | [TBD: study_backend vs ssafy-spring-study Org 중 메인 확정 필요] |
| Live Demo | https://www.ssafy-study.site/ |
| 설명 | 강의 영상·학습 자료를 업로드하면 AI가 자동으로 퀴즈를 생성하고, 개인별 학습 진척을 관리하는 비동기 학습 플랫폼. GitHub Organization 기반으로 Issue·PR을 통한 과제·코드리뷰까지 병행하는 실습형 운영 구조. |
| Why | 강의식 스터디의 참여율 저하·일정 충돌 문제를 해결하기 위해, "비동기 학습 + 자동 퀴즈 + 실습형 PR 리뷰"라는 새로운 운영 구조를 직접 설계하고 플랫폼으로 구현. 결과적으로 20명+ 스터디원이 이탈 없이 학습을 이어가고 있음. |
| Stack | Spring Boot · JPA · Spring Security · JWT · MySQL · Redis · Next.js · Groq API (← Gemini) · AWS (EC2·S3·RDS·CloudFront) · Docker · Terraform · GitHub Actions (AWS SSM) |
| Highlights | ① **AI 제공자 추상화 레이어 설계** — Spring AI + Gemini API 한국 리전 403 에러 추적 후 환경 제약 발견. Groq로 단순 교체가 아닌 Provider Abstraction Layer를 설계해 비즈니스 로직 변경 없이 AI 제공자 교체 가능한 구조 완성.<br>② **DB 캐싱으로 AI 호출 비용·지연 동시 해결** — 동일 자료에 반복되는 AI 호출의 비용·지연 문제를, 자료 단위 DB 캐싱으로 해결. 첫 호출 후 모든 동일 요청은 DB 즉시 반환.<br>③ **Spec-Driven Development(SDD) 적용** — CLAUDE.md / plan.md 기반 하네스 엔지니어링으로 개발 진행. 에이전트 의존성 배제, 멱등성 spec 설계로 1인 개발에서도 일관된 속도·품질 확보. |
| 역할 | 1인 개발 (기획·백엔드·프론트엔드·인프라·스터디 운영 주도) |
| 기간 | 2026.03 – 진행 중 |

#### 보조 카드 — Cotree

| 필드 | 값 |
|---|---|
| 제목 | 📦 Cotree |
| 라벨 | Code Only (라이브 데모 종료) |
| Repo | https://github.com/k-haechan/WEB3_4_SsamMuDan_BE |
| 설명 | 인프런 형태 온라인 교육 플랫폼 |
| Highlights (압축) | Spring Security + JWT 회원·인증 도메인 설계, 쿼리 최적화로 핵심 API 응답 2배 이상 개선 |
| Stack | Spring Boot · JWT · MySQL · AWS |
| 기간 | 2025.03 – 04 |

#### 보조 카드 — SNS1

| 필드 | 값 |
|---|---|
| 제목 | 📦 SNS1 |
| 라벨 | Code Only (라이브 데모 종료) |
| Repo | https://github.com/k-haechan/sns1-server |
| 설명 | 1인 개발 SNS 서비스 |
| Highlights (압축) | 기획~인프라·배포까지 1인 책임. Terraform/GHA로 IaC·CI/CD 자동화. AWS Java SDK 버그 발견·재현·제보 |
| Stack | Spring Boot · Terraform · AWS |
| 기간 | 2025.07 – 08 |

#### 카드 렌더링 방식

- **HTML `<table>` 사용** — 셀 안에 이미지·뱃지·텍스트를 자유 배치 가능, GitHub 마크다운 파서가 안정적 처리.
- 메인 카드는 가로 풀폭 1단 셀, 보조 카드 2개는 가로 2단 셀로 배치.

---

### ③ Skills & Learning

**목적:** 채용 담당자의 키워드 매칭 + 학습 궤적의 동적 신호.

**카테고리 (HTML `<table>` 형태, 기존 디자인 언어 유지):**

| 카테고리 | 항목 |
|---|---|
| Languages | Java · Python · C/C++ |
| Backend | Spring Boot · Spring Security · JPA |
| Frontend | Next.js · Thymeleaf · HTML/CSS |
| Database | MySQL · Redis |
| Infra & DevOps | AWS (EC2·S3·RDS·CloudFront) · Docker · Terraform |
| Test & CI/CD | JUnit5 · Mockito · Jacoco · GitHub Actions |
| 🌱 Currently Exploring | Claude Code · superpowers · gstack · bmad — AI Agent Skill 프레임워크 / SDD 방법론 |

**아이콘:** 기존 devicon CDN 유지 (jsdelivr).

**유지보수 정책:** Currently Exploring 줄은 6개월 단위 수동 갱신 권장.

---

### ④ Activity

**목적:** "현재 살아있다"는 자동화된 신호.

**포함 위젯:**

1. **GitHub Stats** (radical 테마, 기존 유지)
2. **Top Languages** (radical 테마, 기존 유지)
3. **GitHub Streak** (`github-readme-streak-stats.herokuapp.com`)
4. **Solved.ac 큰 위젯** (`mazassumnida.wtf` 큰 박스 버전)
5. **Snake animation** (`Platane/snk` GitHub Action으로 매일 생성)

**제외 위젯 (의도적):**

- ❌ **Tistory 자동 임베드** — 사용자가 현재 블로그 글을 잘 올리지 않아, 자동 피드가 오히려 "마지막 글이 N개월 전" stale 인상을 줄 위험. Hero의 정적 Blog 뱃지(profile reference)는 유지.
- ❌ **GitHub Trophy** — 인플레이션이 심해 절제된 신호로 빼는 것이 더 강력.

**레이아웃:**

```
[GitHub Stats]         [Top Languages]
[GitHub Streak]        [Solved.ac 큰 위젯]
[Snake animation — 가로 풀폭]
```

---

### ⑤ Experience & Certifications

**목적:** 검증 가능한 트랙 압축 노출.

#### Education

| 학교 | 전공 | 기간 |
|---|---|---|
| 국민대학교 | 정보보안암호수학 | 2018.03 – 2024.02 |

**활동 요약:**
- C/C++ 기반 암호 모듈 최적화, PKI 인증·서명 로직 구현
- Python 기반 통계 분석·전처리·시각화

#### Programs

| 기관 | 과정 | 기간 |
|---|---|---|
| 프로그래머스 데브코스 | 클라우드 기반 백엔드 엔지니어링 | 2024.11 – 2025.04 |
| 삼성 청년 SW AI 아카데미 (SSAFY) | SW 역량 강화 | 2026.01 – 2026.03 |

(각 항목당 1~3줄 학습 결과 요약 동봉)

#### Certifications (shields.io 뱃지)

- 정보처리기사
- SQLD
- 빅데이터 분석기사

---

### ⑥ Contact

**목적:** 연락 행동의 마찰 최소화.

**CTA:** "문제·아이디어·협업 — 무엇이든 환영합니다."

**채널 (4개):**

- 📧 **Email:** gibbm1127@naver.com
- 💻 **GitHub:** @k-haechan
- 📝 **Blog:** cheer-for-your-life.tistory.com
- 🌐 **Portfolio:** portfolio.haechan.site

**제외:**

- ❌ **전화번호** — README는 영구 공개·인덱싱되므로 스팸·스크래핑 위험. 포트폴리오 사이트(접근 통제 가능)에만 노출.
- ❌ **저작권 표기 (`© 2026 ...`)** — 격식이 무거워 README의 가벼운 톤과 부조화.

---

## 6. 자동화 인프라 (Automation Infrastructure)

### 필요한 GitHub Actions 워크플로우

| 워크플로우 | 트리거 | 작업 | 파일 위치 |
|---|---|---|---|
| Snake animation 생성 | 매일 00:00 UTC + push | `Platane/snk@v3` 액션으로 contribution snake SVG 생성 → `output` 브랜치 푸시 | `.github/workflows/snake.yml` |

### 외부 SVG API (워크플로우 불필요, README 안에 직접 임베드)

- `github-readme-stats.vercel.app` — Stats / Top Languages
- `github-readme-streak-stats.herokuapp.com` — Streak
- `mazassumnida.wtf` — Solved.ac
- `komarev.com/ghpvc` — Profile Views
- `capsule-render.vercel.app` — Hero 헤더 웨이브
- `cdn.jsdelivr.net/gh/devicons/devicon` — Skills 아이콘
- `img.shields.io` — 뱃지·자격증

### 운영상 주의

- 외부 SVG API 다운 시 깨진 이미지 표시 가능성 (받아들이고 가는 것). 의식적으로 위젯 수를 5개 내외로 절제.
- Profile Views 카운터는 GitHub의 camo 캐싱 때문에 정확한 통계가 아닌 "장식+사회적 증거"로 받아들임.

---

## 7. Open Questions / Placeholders

구현 단계에서 사용자 확인이 필요한 항목:

1. **SSAFY-STUDY Platform 메인 저장소 확정** — `k-haechan/study_backend` (개인) vs `ssafy-spring-study/*` (Organization) 중 README에 링크할 정식 메인을 확정해야 한다.
2. **현재 관심사 한 줄** — 6개월~1년 단위 갱신을 위한 명시적 리듬을 정할지 (예: 분기 첫 달 1일 알림).
3. **Currently Exploring** — Skills 안의 학습 항목도 동일하게 갱신 리듬 필요.

---

## 8. 의도적으로 하지 않는 것 (Out of Scope)

본 재설계는 다음을 의도적으로 *포함하지 않는다* — 스코프 보호 및 향후 변경 가능성을 명시.

- **"Now" 섹션** — 유지보수 부담이 가장 크고 stale 위험이 높아 제외. 그 책임을 Hero의 "현재 관심사"와 Activity 자동 위젯에 분산.
- **Tistory 블로그 자동 피드** — 사용자가 현재 글 활동이 적어 역효과 위험.
- **GitHub Trophy** — 인플레이션 심한 자동 트로피 시스템, 절제로 차별화.
- **다국어 지원 (영문 풀버전)** — 한국어 중심 전략 유지. 기술용어만 영문 혼용.
- **인터랙티브 컴포넌트** — README는 정적 마크다운. 인터랙션은 portfolio 사이트가 책임.
- **기존 시각 언어 전면 교체** — radical 테마, 중앙 정렬, devicon 아이콘 등 기존 자산 유지. 구조와 컨텐츠만 재구성.

---

## 9. 다음 단계

1. 본 spec에 대한 사용자 검토 및 승인.
2. `superpowers:writing-plans` 스킬을 통한 구현 계획서 작성.
3. 구현 — 새 README.md 작성, `.github/workflows/snake.yml` 추가, 자격증 뱃지 생성.
