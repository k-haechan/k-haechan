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
  <a href="mailto:gibbm1127@naver.com"><img src="https://img.shields.io/badge/Email-03C75A?style=for-the-badge&logo=naver&logoColor=white" alt="Email"></a>
  <a href="https://solved.ac/gocks0203" target="_blank"><img src="https://mazassumnida.wtf/api/v2/generate_badge?boj=gocks0203" alt="Solved.ac"></a>
  <img src="https://komarev.com/ghpvc/?username=k-haechan&style=for-the-badge&color=blueviolet" alt="Profile Views"/>
</p>

</div>

---

<h2 align="center">🌟 Featured Projects</h2>

<table>
<tr>
<td colspan="2">

### 🏆 Hakku (학꾸) &nbsp;·&nbsp; SSAFY 1학기 관통 프로젝트 최우수상 (서울 17반 1등)
**AI 퍼스널컬러 커머스 플랫폼 — 결제 서버 · 스토리지 보안 · AI 챗봇**
[ [Repo](https://github.com/k-haechan/hakku) · [Live Demo](https://hakku.rearleg.com/) ]

AI 퍼스널컬러 진단으로 꾸미기 아이템을 추천하는 커머스·커뮤니티 플랫폼. Nginx 뒤에 6개 서비스가 독립 실행되는 **폴리글랏 마이크로서비스** 구조.

**💡 Why** &nbsp; 팀원과 **페어프로그래밍**으로 협업하며 **백엔드 아키텍처 리뷰·보안 취약점 점검**을 맡아, 결제 서버를 설계·구현하고 스토리지 서버 분리의 보안 설계와 AI 챗봇의 뼈대를 이끎.

**🛠 Stack** &nbsp; `Java 17` `Spring Boot 4.0` `Spring Security` `JPA` `Kafka (KRaft)` `토스페이먼츠` `PostgreSQL` `Redis` `Go` `FastAPI` `OpenAI` `Vue 3` `Docker` `Nginx`

**✨ Highlights**

① **intent-first 멱등 결제 설계** — `idempotency_key` UNIQUE로 과금 전 PENDING 의도를 선커밋하고, PG 호출을 트랜잭션 밖에서 수행해 이중 결제와 "돈은 빠졌는데 주문은 없는" 커밋-실패 갭을 구조적으로 차단.

② **트랜잭셔널 Outbox + Kafka 릴레이** — 상태 변경과 이벤트를 같은 트랜잭션으로 기록, `acks=all`·멱등 producer로 at-least-once 발행. 반복 실패 메시지는 DEAD로 격리해 결제 이벤트 유실 0.

③ **웹훅 위조 방어 · 스토리지 보안 분리** — PG 웹훅을 HMAC-SHA256 상수시간 비교로 검증(타이밍 공격 방지), 이미지 I/O는 Go 네이티브 서버로 분리하고 Bearer JWT 소유자 검증으로 접근 제어.

👥 **팀 프로젝트 (2인 페어프로그래밍)** — 결제 · 보안 · 아키텍처 리뷰 주도
📅 2026.05 – 06

</td>
</tr>
<tr>
<td colspan="2">

### 🚀 SSAFY Study Platform
**AI 퀴즈·실시간 알림 스터디 백엔드 — 20명 실사용**
[ [Repo](https://github.com/k-haechan/study_backend) · [Live Demo](https://www.ssafy-study.site/) ]

유튜브 강의형 학습 콘텐츠에 더해, AI가 학습 글을 기반으로 퀴즈를 자동 생성하고 SSE로 실시간 알림을 제공하는 스터디 플랫폼. SSAFY 스터디원 **20명이 실제로 사용**하는 서비스.

**💡 Why** &nbsp; 강의식 스터디의 참여율 저하 문제를 "비동기 학습 + AI 자동 퀴즈"로 해결하기 위해 직접 설계·구현. LLM을 단순 챗봇이 아닌 **"콘텐츠 → 구조화된 학습 데이터" 변환 파이프라인**으로 활용.

**🛠 Stack** &nbsp; `Spring Boot 4.0` `Spring Security` `JWT` `MySQL` `Redis` `Flyway` `Groq API (Llama 3.3-70B)` `AWS S3` `SSE` `SpringDoc`

**✨ Highlights**

① **LLM 기반 퀴즈 자동 생성·채점** — `GroqClient`로 Llama 3.3-70B를 호출해 포스트 본문을 객관식 퀴즈로 자동 생성, 정규화된 스키마로 서버 자동 채점·시도 이력 제공.

② **S3 고아 이미지 정리 스케줄러** — `ImageStatus`로 임시/확정 상태를 추적하고 `ImageCleanupScheduler`로 미연결 이미지를 주기적으로 정리해 비용·정합성 문제 해소.

③ **이벤트 기반 비동기 알림** — `NotificationCreatedEvent → EventListener → PushService`로 생성/전송을 디커플링, SSE로 실시간 알림 경량 구현.

👤 **1인 백엔드** — 기획 · 백엔드 · 인프라 주도
📅 2026.02 – 03

</td>
</tr>
<tr>
<td width="50%" valign="top">

### 📦 SNS Service
*실시간 소셜 네트워킹 백엔드*

[ [Repo](https://github.com/k-haechan/sns1-server) ]

기획부터 인프라·배포까지 1인 책임한 SNS 서비스.

193개 커밋 전부 직접 작성, Terraform/GHA로 IaC·CI/CD 자동화.
**AWS Java SDK 버그 발견·제보(#6127)**.

**Stack:** `Spring Boot` `MySQL` `MongoDB` `Redis` `Terraform` `AWS`
📅 2025.07 – 09

</td>
<td width="50%" valign="top">

### 📦 Cotree
*교육 플랫폼 · 팀 5인*

[ [Repo](https://github.com/k-haechan/WEB3_4_SsamMuDan_BE) ]

인프런 형태 온라인 교육 플랫폼. 회원/인증 도메인 전담.

복합 인덱스 직접 설계로 리뷰 조회 응답 **2배 이상**(783ms→) 개선.

**Stack:** `Spring Boot` `JWT` `OAuth2` `QueryDSL` `MySQL`
📅 2025.03 – 05

</td>
</tr>
</table>

---
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
  <img src="https://mazassumnida.wtf/api/v2/generate_badge?boj=gocks0203" alt="Solved.ac" height="180" />
</a>

<br/><br/>

<a href="https://github.com/k-haechan">
  <img src="https://raw.githubusercontent.com/k-haechan/k-haechan/output/github-contribution-grid-snake.svg" alt="Contribution Snake" />
</a>

</div>

---
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

**삼성 청년 SW AI 아카데미 (SSAFY)** &nbsp; *SW 역량 강화* &nbsp; `2026.01 – 진행 중`

- Java·Python 알고리즘·자료구조 집중 학습, CS 핵심 개념 체계화
- 팀 프로젝트 협업·백엔드 개발
- 🏆 **1학기 관통 프로젝트 경진대회 최우수상 (서울 17반 1등)** — Hakku(학꾸)

### 📜 Certifications

<p align="center">
  <img src="https://img.shields.io/badge/정보처리기사-0078D4?style=for-the-badge&logoColor=white" alt="정보처리기사"/>
  <img src="https://img.shields.io/badge/SQLD-CC2927?style=for-the-badge&logo=microsoftsqlserver&logoColor=white" alt="SQLD"/>
  <img src="https://img.shields.io/badge/빅데이터분석기사-4479A1?style=for-the-badge&logoColor=white" alt="빅데이터 분석기사"/>
</p>

---
<h2 align="center">📬 Contact</h2>

<div align="center">

> "문제·아이디어·협업 — 무엇이든 환영합니다."

<p>
  <a href="mailto:gibbm1127@naver.com"><img src="https://img.shields.io/badge/Email-gibbm1127@naver.com-03C75A?style=for-the-badge&logo=naver&logoColor=white" alt="Email"></a>
  <a href="https://github.com/k-haechan"><img src="https://img.shields.io/badge/GitHub-@k--haechan-181717?style=for-the-badge&logo=github&logoColor=white" alt="GitHub"></a>
  <a href="https://cheer-for-your-life.tistory.com/"><img src="https://img.shields.io/badge/Blog-cheer--for--your--life-FF5722?style=for-the-badge&logo=blogger&logoColor=white" alt="Blog"></a>
  <a href="https://portfolio.haechan.site/"><img src="https://img.shields.io/badge/Portfolio-haechan.site-4CAF50?style=for-the-badge&logo=googlechrome&logoColor=white" alt="Portfolio"></a>
</p>

</div>
