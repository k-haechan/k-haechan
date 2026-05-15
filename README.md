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

### 🚀 SSAFY-STUDY Platform
**AI 비동기 학습 플랫폼 — 20명+ 운영 중 · 진행형**
[ [Repo](https://github.com/k-haechan/study_backend) · [Live Demo](https://www.ssafy-study.site/) ]

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
📅 2025.03 – 04

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
📅 2025.07 – 08

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
<!-- TODO(task-4): Activity -->
<!-- TODO(task-5): Experience & Certifications -->
<!-- TODO(task-6): Contact -->
