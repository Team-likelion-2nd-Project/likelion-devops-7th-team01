# 수강신청 시스템 (Course Registration System)

> **협업이 처음이신가요?** 이슈 생성부터 PR 머지까지 전 과정은 [협업 가이드](./docs/GUIDE.md)를 먼저 읽어주세요.

> **수강신청 오픈 시각의 트래픽 폭증 상황에서도 안정적으로 동작하는, HPA 오토스케일링 기반 수강신청 시스템**

![Team](https://img.shields.io/badge/Team-01-151515?style=for-the-badge)
![React](https://img.shields.io/badge/React-151515?style=for-the-badge&logo=react&logoColor=61DAFB)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-151515?style=for-the-badge&logo=springboot&logoColor=6DB33F)
![MySQL](https://img.shields.io/badge/MySQL-151515?style=for-the-badge&logo=mysql&logoColor=4479A1)
![AWS](https://img.shields.io/badge/AWS-151515?style=for-the-badge&logo=amazonwebservices&logoColor=FF9900)


[![데모 영상](https://img.youtube.com/vi/{{YOUTUBE_ID}}/maxresdefault.jpg)]({{YOUTUBE_URL}})

{{서비스 2~3문장 설명. 대상 사용자와 핵심 가치 중심으로.}}

- **배포 주소:** {{https://example.com}}
- **시연 영상:** [YouTube]({{YOUTUBE_URL}})
- **문서 최종 정리일:** `YYYY-MM-DD` / **구현 기준일:** `YYYY-MM-DD`

---

## 팀 구성

| 이름 | 역할 | 담당 | GitHub |
|------|------|------|--------|
| 박영찬 | 팀장 / 인프라1 | Terraform, EKS | [@ycpark8156](https://github.com/ycpark8156) |
| 이용민 | 인프라2 | CI/CD, 모니터링, Terraform | [@leeym27](https://github.com/leeym27) |
| 김상협 | 풀스택1 | 수강신청 (API + UI) | [@HyeobSang](https://github.com/HyeobSang) |
| 김차니 | 풀스택2 | 시간표·인증 (API + UI) | [@chaneee93](https://github.com/chaneee93) |

---

## 레포지토리

이 레포는 문서 허브입니다. 실제 코드는 아래 레포에서 관리합니다.

| 영역 | 레포 | 담당 |
|------|------|------|
| Frontend | [team01-frontend](https://github.com/Team-likelion-2nd-Project/likelion-devops-7th-team01-frontend) | 김상협, 김차니 |
| Backend | [team01-backend](https://github.com/Team-likelion-2nd-Project/likelion-devops-7th-team01-backend) | 김상협, 김차니 |
| Infra | [team01-infra](https://github.com/Team-likelion-2nd-Project/likelion-devops-7th-team01-infra) | 박영찬, 이용민 |

---

## 빠른 심사 흐름 (5분)

1. {{데모 영상}} 을 확인합니다.
2. {{배포 주소}} 를 엽니다.
3. 테스트 계정으로 로그인합니다. (`ID: {{demo}}` / `PW: {{demo1234}}`)
4. 강의 목록에서 수강신청을 진행합니다.
5. 시간표 화면에서 신청한 강의가 반영되었는지 확인합니다.
6. (선택) Grafana 대시보드에서 부하 테스트 시 파드가 늘어나는 모습을 확인합니다.

---

## Core Design

- **오토스케일링 우선** — 이 프로젝트의 핵심은 기능이 아니라 HPA 기반 오토스케일링 시연입니다.
- **단일 백엔드 서비스** — 마이크로서비스로 분리하지 않고, 하나의 Spring Boot 애플리케이션으로 수강신청·시간표 기능을 모두 처리합니다.
- **동시성 안전성** — DB 트랜잭션 락과 Redis를 함께 사용해 정원 초과와 시간 중복 신청을 방지합니다.
- **정적/동적 자원 분리** — 프론트엔드는 S3+CloudFront로, 오토스케일링이 필요한 백엔드만 EKS로 배포합니다.
- **비밀정보는 코드에 두지 않음** — Secrets Manager와 EKS Pod Identity로 자격증명을 안전하게 관리합니다.

---

## Architecture

<!-- 아키텍처 다이어그램 이미지는 나중에 docs/images/architecture.png로 추가 예정 -->
<!-- ![아키텍처](./docs/images/architecture.png) -->

```
사용자
  -> CloudFront + S3 (React, 정적 배포)
  -> ALB Ingress
  -> EKS Backend (Spring Boot, HPA 적용)
  -> RDS(MySQL) / ElastiCache(Redis)
  -> Cognito (인증)
  -> 응답
```

| 영역 | 기술 |
|------|------|
| Frontend | React (S3 + CloudFront 배포) |
| Backend | Spring Boot (단일 서비스, EKS 배포) |
| Database | RDS (MySQL) |
| 캐시 | ElastiCache (Redis) |
| Infra | Terraform, EKS, Cluster Autoscaler, Kustomize |
| CI/CD | GitHub Actions (OIDC 인증) |
| 인증 | Cognito |

---

## 주요 기능

| 기능 | 설명 | 로그인 필요 |
|------|------|------------|
| 강의 목록 조회 | 개설된 강의 목록을 확인 | X |
| 수강신청/취소 | 정원 및 시간 중복을 검증하여 신청·취소 | O |
| 시간표 자동생성 | 신청 완료된 강의를 요일×교시 표로 자동 구성 | O |

주요 화면: 로그인 / 강의목록·신청 / 시간표 — 자세한 구성은 Wiki > UI Screens 참고.
API 상세 경로와 요청/응답 구조는 Wiki > API Specification 을 따릅니다.

---

## Documentation

상세 설계·회의 기록은 **GitHub Wiki** 에서 관리합니다.

| 카테고리 | 문서 |
|----------|------|
| **Start Here** | 기획 배경 · UI Screens |
| **Architecture** | System Architecture · ERD · API Specification |
| **Operations** | 배포 가이드 · 회의록 · 트러블슈팅 |

---

## 범위 경계

**현재 제공:**

- 강의 조회, 수강신청/취소
- 정원 관리, 동시성 제어(DB 락 + Redis)
- 시간표 자동생성
- HPA 기반 오토스케일링 (수강신청 API 대상)

**현재 미제공:**

- 게시판/공지 기능 — 오토스케일링 이라는 핵심 목표에 기여하지 않아 제외
- 파일 업로드(S3 Presigned URL) — 동일한 이유로 제외
- 강의 관리자 화면 — 강의 데이터는 DB 시드 스크립트로 사전 입력

**배포 단계:** `dev` → **`demo` (현재)** → `prod` (미선언)

---

## 보안과 개인정보 경계

이 저장소와 하위 레포는 모두 공개 저장소입니다. 다음 정보를 절대 포함하지 않습니다.

- 인증·클라우드 비밀값, `.env` 실제 값, 인증서·키 파일
- 실제 사용자 개인정보, 운영 DB 계정 정보
- 내부 인프라 식별자 및 서버 직접 접근 URL

비밀값이 실수로 커밋되면 GitHub이 push를 차단합니다. 이미 커밋된 경우 **즉시 해당 키를 폐기하고 재발급**하세요. 커밋을 되돌리는 것만으로는 이력에 남습니다.

---

## 로컬 실행

로컬 실행 방법은 각 레포 README를 참고하세요.

- Backend 실행법: [team01-backend README](https://github.com/Team-likelion-2nd-Project/likelion-devops-7th-team01-backend)
- Frontend 실행법: [team01-frontend README](https://github.com/Team-likelion-2nd-Project/likelion-devops-7th-team01-frontend)
- Infra(Terraform/K8s) 실행법: [team01-infra README](https://github.com/Team-likelion-2nd-Project/likelion-devops-7th-team01-infra)

**검증**

```bash
{{./gradlew test}}
cd frontend && npm run build
```

---

## 기여 방법

- **규칙 요약** — [CONTRIBUTING.md](./CONTRIBUTING.md)
- **실행 방법 상세** — [협업 가이드](./docs/GUIDE.md)

## License

이 프로젝트는 [MIT License](./LICENSE) 를 따릅니다.
