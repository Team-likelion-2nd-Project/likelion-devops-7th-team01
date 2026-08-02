# {{프로젝트명}} ({{PROJECT_NAME_EN}})

> **협업이 처음이신가요?** 이슈 생성부터 PR 머지까지 전 과정은 [협업 가이드](./docs/GUIDE.md)를 먼저 읽어주세요.

![Team](https://img.shields.io/badge/Team-team-01-151515?style=for-the-badge)
<!-- 사용 기술만 남기고 나머지는 삭제 -->
![React](https://img.shields.io/badge/React-151515?style=for-the-badge&logo=react&logoColor=61DAFB)
![TypeScript](https://img.shields.io/badge/TypeScript-151515?style=for-the-badge&logo=typescript&logoColor=3178C6)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-151515?style=for-the-badge&logo=springboot&logoColor=6DB33F)
![MySQL](https://img.shields.io/badge/MySQL-151515?style=for-the-badge&logo=mysql&logoColor=4479A1)
![AWS](https://img.shields.io/badge/AWS-151515?style=for-the-badge&logo=amazonwebservices&logoColor=FF9900)

> **{{한 문장 소개 — 누구의 어떤 문제를, 어떻게 해결하는 서비스인가}}**

[![데모 영상](https://img.youtube.com/vi/{{YOUTUBE_ID}}/maxresdefault.jpg)]({{YOUTUBE_URL}})

{{서비스 2~3문장 설명. 대상 사용자와 핵심 가치 중심으로.}}

- **배포 주소:** {{https://example.com}}
- **시연 영상:** [YouTube]({{YOUTUBE_URL}})
- **문서 최종 정리일:** `YYYY-MM-DD` / **구현 기준일:** `YYYY-MM-DD`

---

## 팀 구성

| 이름 | 역할 | 담당 | GitHub |
|------|------|------|--------|
| {{이름}} | 팀장 / BE | {{담당 도메인}} | [@{{id}}](https://github.com/{{id}}) |
| {{이름}} | BE | {{담당 도메인}} | [@{{id}}](https://github.com/{{id}}) |
| {{이름}} | FE | {{담당 화면}} | [@{{id}}](https://github.com/{{id}}) |
| {{이름}} | FE | {{담당 화면}} | [@{{id}}](https://github.com/{{id}}) |

---

## 빠른 심사 흐름 (5분)

> 심사위원·멘토가 5분 안에 핵심 기능을 확인할 수 있는 순서로 작성합니다.

1. 위 영상 썸네일을 클릭해 전체 시연을 확인합니다.
2. {{배포 주소}} 를 엽니다.
3. 테스트 계정으로 로그인합니다. (`ID: {{demo}}` / `PW: {{demo1234}}`)
4. {{핵심 기능 1}} 을 실행합니다.
5. {{핵심 기능 2}} 결과 화면에서 {{확인 포인트}} 를 확인합니다.

---

## Core Design

> 이 프로젝트가 **의도적으로 선택한 원칙**을 3~6개 적습니다. 기능 나열이 아니라 설계 판단을 씁니다.

- **{{원칙명}}** — {{무엇을 보장하고 무엇을 금지하는지}}
- **{{원칙명}}** — {{설명}}
- **{{원칙명}}** — {{설명}}

---

## Architecture

![아키텍처](./docs/images/architecture.png)

```
사용자
  -> {{Frontend}}
  -> {{Backend API}}
  -> {{Database}}
  -> {{외부 서비스 / AI}}
  -> 응답
```

| 영역 | 기술 |
|------|------|
| Frontend | {{React, TypeScript, Tailwind}} |
| Backend | {{Spring Boot, JPA}} |
| Database | {{MySQL 8.0}} |
| Infra | {{AWS EC2, S3, RDS}} |
| CI/CD | {{GitHub Actions}} |
| 인증 | {{JWT / OAuth2}} |

---

## 주요 기능

| 기능 | 설명 | 로그인 필요 |
|------|------|------------|
| {{기능명}} | {{한 줄 설명}} | X |
| {{기능명}} | {{한 줄 설명}} | O |
| {{기능명}} | {{한 줄 설명}} | O |

주요 화면: {{메인 / 목록 / 상세 / 마이페이지}} — 자세한 구성은 Wiki > UI Screens 참고.
API 상세 경로와 요청/응답 구조는 Wiki > API Specification 을 따릅니다.

---

## Documentation

상세 설계·회의 기록은 **GitHub Wiki** 에서 관리합니다.

| 카테고리 | 문서 |
|----------|------|
| **Start Here** | 기획 배경 · User Flows · UI Screens |
| **Architecture** | System Architecture · ERD · API Specification |
| **Operations** | 배포 가이드 · 회의록 · 트러블슈팅 |

---

## 범위 경계

> 심사에서 가장 신뢰를 얻는 항목입니다. **되는 것과 안 되는 것을 정확히** 씁니다.

**현재 제공:**

- {{구현 완료 기능}}
- {{구현 완료 기능}}

**현재 미제공:**

- {{미구현 기능 — 왜 범위 밖인지 한 줄}}
- {{미구현 기능}}

**배포 단계:** `dev` → **`demo` (현재)** → `prod` (미선언)

---

## 보안과 개인정보 경계

이 저장소는 공개 저장소입니다. 다음 정보를 절대 포함하지 않습니다.

- 인증·클라우드 비밀값, `.env` 실제 값, 인증서·키 파일
- 실제 사용자 개인정보, 운영 DB 계정 정보
- 내부 인프라 식별자 및 서버 직접 접근 URL

비밀값이 실수로 커밋되면 GitHub이 push를 차단합니다. 이미 커밋된 경우 **즉시 해당 키를 폐기하고 재발급**하세요. 커밋을 되돌리는 것만으로는 이력에 남습니다.

---

## 로컬 실행

**사전 요구사항:** {{Node 20+, JDK 17, MySQL 8.0}}

**Backend**

```bash
cp backend/.env.example backend/.env
{{./gradlew bootRun}}
```

**Frontend**

```bash
cd frontend
npm install
npm run dev
```

- backend: `http://localhost:8080`
- frontend: `http://localhost:3000`
- env 템플릿: `backend/.env.example`, `frontend/.env.example`

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
