---

# 🏃 건강 루틴 트래커 (Health Routine Tracker)

## 📌 1. 프로젝트 개요

**프로젝트명**: 건강 루틴 트래커 (Health Routine Tracker)
**목표**: 사용자가 수면, 운동, 식사, 음수량 등 건강 루틴을 기록하고, 댓글·좋아요 기능을 통해 상호작용하며, 통계 및 차트를 통해 습관을 관리할 수 있는 웹 애플리케이션을 개발한다.
**기간**: 2025년 9월 6일 \~ 2025년 9월 12일 (총 7일)
**팀 구성**: 6명 (프론트엔드 3명, 백엔드 3명)

---

## ⚙️ 2. 주요 기능 및 기술 스택

### 2.1 주요 기능

1. 회원가입/로그인 (JWT 인증)
2. 데일리 루틴 관리 (CRUD) – 수면, 운동, 식사, 물 섭취량, 메모
3. 댓글 및 좋아요 기능
4. 통계 및 시각화 (주간/월간, 달력 뷰)
5. 마이페이지 (내 기록 요약)

### 2.2 기술 스택

* **프론트엔드**: React, TypeScript, Vite, React Router, React Query, TailwindCSS, Recharts
* **백엔드**: Spring Boot 3.x, Spring Security, Spring Data JPA, MariaDB, JWT, Lombok, Gradle
* **공통**: GitHub, Notion, Postman, Vercel(FE 배포), Railway/Render(BE 배포)

---

## 📋 3. 요구사항 명세서

### 3.1 기능 요구사항

| ID   | 기능명      | 설명                   | 입력값/출력값                   | 우선순위 |
| ---- | -------- | -------------------- | ------------------------- | ---- |
| F-01 | 회원가입     | 사용자 등록               | email, password, nickname | 상    |
| F-02 | 로그인      | JWT 발급               | email, password → JWT     | 상    |
| F-03 | 루틴 작성    | 수면, 운동, 식사, 물, 메모 기록 | routine 데이터               | 상    |
| F-04 | 루틴 조회    | 사용자별 루틴 목록/상세        | userId, date              | 상    |
| F-05 | 루틴 수정    | 기존 루틴 데이터 변경         | routineId, 수정 데이터         | 중    |
| F-06 | 루틴 삭제    | 루틴 제거                | routineId                 | 중    |
| F-07 | 댓글 작성    | 루틴에 댓글 등록            | routineId, content        | 중    |
| F-08 | 댓글 수정/삭제 | 댓글 관리                | commentId                 | 중    |
| F-09 | 좋아요 토글   | 루틴 좋아요/취소            | routineId, userId         | 중    |
| F-10 | 통계 조회    | 주간/월간 루틴 통계          | 기간 데이터                    | 중    |
| F-11 | 달력 뷰     | 루틴 등록 현황 표시          | 월별 데이터                    | 하    |
| F-12 | 마이페이지    | 내 기록 및 통계 확인         | userId                    | 중    |

---

## 👩‍💻 4. 직무 역할 및 활용 도구

* **FE1**: Auth UI, 네비게이션 레이아웃
* **FE2**: 루틴 CRUD UI, 댓글/좋아요 UI
* **FE3**: 마이페이지, 차트, 달력
* **BE1**: Auth API, JWT 인증, Spring Security 설정
* **BE2**: 루틴 CRUD API, 통계 API
* **BE3**: 댓글/좋아요 API, 예외처리

활용 도구: GitHub, Figma, Notion, Postman, MariaDB Workbench

---

## 📦 5. 산출물 리스트

* 프로젝트 기획서 및 계획서
* 요구사항 명세서 (FR/NFR)
* DB ERD 다이어그램
* API 명세서 (Swagger, Markdown 문서)
* FE/BE 소스코드 (GitHub)
* 배포 링크 (FE, BE)
* 최종 발표 자료 (PPT)

---

## ⏰ 6. 마일스톤

* **Day 1**: 환경 세팅, DB 설계, API 설계
* **Day 2\~3**: Auth + 루틴 CRUD 개발
* **Day 4**: 댓글/좋아요 개발
* **Day 5**: 통계/달력 개발
* **Day 6**: 통합 테스트, 버그 수정
* **Day 7**: 발표 준비 및 시연

---

## 📑 7. API 명세서

### 7.1 MEMBER-SERVICE (인증/회원 관리)

| No. | Domain | Description  | Base URL | Detailed URL | Http Method | Full URL             | 담당자 (BE) | 상태   |
| --- | ------ | ------------ | -------- | ------------ | ----------- | -------------------- | -------- | ---- |
| 1   | MEMBER | 회원가입         | /auth    | /register    | POST        | /auth/register       | BE1      | 진행예정 |
| 2   | MEMBER | 로그인 (JWT 발급) | /auth    | /login       | POST        | /auth/login          | BE1      | 진행예정 |
| 3   | MEMBER | 회원정보 조회      | /members | /me          | GET         | /members/me          | BE1      | 진행예정 |
| 4   | MEMBER | 비밀번호 변경      | /members | /me/password | PATCH       | /members/me/password | BE1      | 진행예정 |
| 5   | MEMBER | 회원 탈퇴        | /members | /{id}        | DELETE      | /members/{id}        | BE1      | 진행예정 |

---

### 7.2 ROUTINE-SERVICE (루틴 관리)

| No. | Domain  | Description | Base URL  | Detailed URL | Http Method | Full URL             | 담당자 (BE) | 상태   |
| --- | ------- | ----------- | --------- | ------------ | ----------- | -------------------- | -------- | ---- |
| 1   | ROUTINE | 루틴 작성       | /routines | -            | POST        | /routines            | BE2      | 진행예정 |
| 2   | ROUTINE | 루틴 목록 조회    | /routines | ?from=\&to=  | GET         | /routines?from=\&to= | BE2      | 진행예정 |
| 3   | ROUTINE | 루틴 상세 조회    | /routines | /{id}        | GET         | /routines/{id}       | BE2      | 진행예정 |
| 4   | ROUTINE | 루틴 수정       | /routines | /{id}        | PATCH       | /routines/{id}       | BE2      | 진행예정 |
| 5   | ROUTINE | 루틴 삭제       | /routines | /{id}        | DELETE      | /routines/{id}       | BE2      | 진행예정 |

---

### 7.3 COMMENT-SERVICE (댓글 관리)

| No. | Domain  | Description | Base URL  | Detailed URL   | Http Method | Full URL                | 담당자 (BE) | 상태   |
| --- | ------- | ----------- | --------- | -------------- | ----------- | ----------------------- | -------- | ---- |
| 1   | COMMENT | 댓글 작성       | /routines | /{id}/comments | POST        | /routines/{id}/comments | BE3      | 진행예정 |
| 2   | COMMENT | 댓글 목록 조회    | /routines | /{id}/comments | GET         | /routines/{id}/comments | BE3      | 진행예정 |
| 3   | COMMENT | 댓글 수정       | /comments | /{id}          | PATCH       | /comments/{id}          | BE3      | 진행예정 |
| 4   | COMMENT | 댓글 삭제       | /comments | /{id}          | DELETE      | /comments/{id}          | BE3      | 진행예정 |

---

### 7.4 LIKE-SERVICE (좋아요 관리)

| No. | Domain | Description | Base URL  | Detailed URL | Http Method | Full URL             | 담당자 (BE) | 상태   |
| --- | ------ | ----------- | --------- | ------------ | ----------- | -------------------- | -------- | ---- |
| 1   | LIKE   | 좋아요 토글      | /routines | /{id}/like   | POST        | /routines/{id}/like  | BE3      | 진행예정 |
| 2   | LIKE   | 좋아요 개수 조회   | /routines | /{id}/likes  | GET         | /routines/{id}/likes | BE3      | 진행예정 |

---

### 7.5 STATS-SERVICE (통계 관리)

| No. | Domain | Description | Base URL | Detailed URL | Http Method | Full URL                          | 담당자 (BE) | 상태   |
| --- | ------ | ----------- | -------- | ------------ | ----------- | --------------------------------- | -------- | ---- |
| 1   | STATS  | 주간 통계 조회    | /stats   | /weekly      | GET         | /stats/weekly?userId=\&startDate= | BE2      | 진행예정 |
| 2   | STATS  | 월간 통계 조회    | /stats   | /monthly     | GET         | /stats/monthly?userId=\&month=    | BE2      | 진행예정 |

---

## 🗄️ 8. DB ERD 다이어그램

📌 User–Routine–Comment–Like 관계 ERD 포함 (이미지 첨부 예정)

---

## 🚀 9. 향후 계획

* 친구 팔로우/공유 기능
* 목표 설정 및 알림 기능
* 모바일 앱 확장 (React Native)
* AI 기반 건강 루틴 추천 기능

---

👉 이 `README.md`를 **GitHub 레포지토리 루트**에 넣으면 팀원들이 프로젝트 구조와 API를 한눈에 파악할 수 있습니다.

원하시면 제가 이 **README에 ERD 다이어그램 이미지 삽입 코드**까지 추가해드릴까요? (`/docs/erd.png` 식으로 넣어서)
