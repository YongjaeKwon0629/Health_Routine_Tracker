
## Health Routine Tracker — 백엔드 v1 명세(최종 전달본)

### 실행/접속
- Base URL: `/v1` (로컬 `http://localhost:8080/v1`)
- 문서: `/v1/swagger-ui.html` (OpenAPI: `/v1/v3/api-docs`)
- 헬스체크: `/v1/actuator/health`
- Postman 컬렉션: `health-routine-tracker/postman_collection.json`
- DB 스키마/시드: `Health_Routine_Tracker.sql`
- 실행: JDK 17 / `./gradlew bootRun` (Windows: `.\gradlew.bat bootRun`)

### 공통 응답 규약
- Envelope: `ApiResponse { success, data, message, code, details }`

| 필드 | 타입 | 설명 |
|---|---|---|
| success | boolean | true=성공, false=실패 |
| data | any | 응답 데이터(성공 시) |
| message | string | 선택 메시지 |
| code | string | 실패 시 오류코드 |
| details | object | 실패 시 추가정보(예: 중복일자 등) |

### 상태코드/에러코드
- 상태코드: 생성 201, 삭제 204(No Content), 그 외 표 참조

| HTTP | code | 의미 | 비고 |
|---|---|---|---|
| 409 | ROUTINE_DUPLICATE | 같은 날짜 루틴 중복 | details.date 포함 |
| 409 | USER_DUPLICATE | 이메일/닉네임 중복 |  |
| 404 | NOT_FOUND | 리소스 없음 |  |
| 403 | FORBIDDEN | 소유자 아님/권한없음 |  |
| 400 | VALIDATION_FAILED | 유효성 오류 |  |
| 401 | AUTH_REQUIRED | 인증 필요 | 추후 JWT 도입 시 사용 |
| 500 | SERVER_ERROR | 서버 오류 |  |

### 입력 규약
- 날짜: `YYYY-MM-DD`, 월: `YYYY-MM` (TZ: Asia/Seoul)
- 페이징: `page` 1부터 시작(응답도 1-base)
- 정렬: 기본 `date,desc` (`routineDate`로 매핑)
- exerciseType: `WALK | RUN | GYM | ETC`

### 엔드포인트 요약

#### Auth
| 메서드 | 경로 | 설명 | 본문/쿼리 | 성공 응답 |
|---|---|---|---|---|
| POST | `/auth/register` | 회원가입 | body: email, username, nickname, password | 201 + UserRes |
| POST | `/auth/login` | 로그인(임시 토큰) | body: email, password | 200 + LoginRes(token=`mock-<userId>`) |

#### Members(임시)
| 메서드 | 경로 | 설명 | 본문/쿼리 | 성공 응답 |
|---|---|---|---|---|
| POST | `/members/register` | 회원 생성(임시) | body: UserCreateReq | 200 + UserRes |
| GET | `/members/{id}` | 회원 단건 | path: id | 200 + UserRes |
| GET | `/members/me` | 마이페이지(임시) | query: id | 200 + UserRes |

#### Routines
| 메서드 | 경로 | 설명 | 본문/쿼리 | 성공 응답 | 비고 |
|---|---|---|---|---|---|
| POST | `/routines` | 루틴 생성 | body: RoutineUpsertReq | 201 + RoutineRes | 중복 시 409/ROUTINE_DUPLICATE |
| GET | `/routines` | 루틴 목록 | userId, from?, to?, page(1), size, sort | 200 + PageResponse<RoutineRes> | 정렬키 `date,desc` |
| GET | `/routines/{id}` | 루틴 상세 | id | 200 + RoutineRes |  |
| PATCH | `/routines/{id}` | 루틴 부분수정 | id, body: RoutineUpdateReq | 200 + RoutineRes |  |
| DELETE | `/routines/{id}` | 루틴 삭제 | id | 204 | 본문 없음 |
| GET | `/routines/by-date` | 날짜별 단건 | userId, date | 200 + RoutineRes |  |

#### Routine Comments
| 메서드 | 경로 | 설명 | 본문/쿼리 | 성공 응답 |
|---|---|---|---|---|
| POST | `/routines/{routineId}/comments` | 댓글 작성 | body: CommentCreateReq | 201 + CommentRes |
| GET | `/routines/{routineId}/comments` | 댓글 목록 | page(0), size(10) | 200 + PageResponse<CommentRes> |

#### Comments(레거시 개별 수정/삭제)
| 메서드 | 경로 | 설명 | 본문/쿼리 | 성공 응답 |
|---|---|---|---|---|
| PATCH | `/api/comments/{id}` | 댓글 수정 | body: CommentUpdateReq | 200 + CommentRes |
| DELETE | `/api/comments/{id}` | 댓글 삭제 | query: userId | 204 |

#### Routine Likes
| 메서드 | 경로 | 설명 | 본문/쿼리 | 성공 응답 |
|---|---|---|---|---|
| POST | `/routines/{routineId}/like` | 좋아요 토글 | query: userId | 200 + LikeToggleRes |
| GET | `/routines/{routineId}/likes` | 좋아요 개수 | - | 200 + number |
| GET | `/routines/{routineId}/like/me` | 내가 눌렀는지 | query: userId | 200 + boolean |

#### Stats
| 메서드 | 경로 | 설명 | 쿼리 | 성공 응답 |
|---|---|---|---|---|
| GET | `/stats/weekly` | 주간 통계(7일) | userId, startDate | 200 + WeeklyStatsRes |
| GET | `/stats/monthly` | 월 달력 통계 | userId, month | 200 + MonthlyCalendarRes |

### 데이터 모델 요약
| 테이블 | 주요 컬럼/제약 |
|---|---|
| users | `user_id PK`, `email UNIQUE`, `nickname UNIQUE`, `password_hash`, `created_at/updated_at` |
| routines | `routine_id PK`, `user_id FK`, `routine_date`, `UNIQUE(user_id, routine_date)`, 지표 필드들 |
| comments | `comment_id PK`, `routine_id FK`, `user_id FK`, `content`, `created_at/updated_at` |
| likes | `like_id PK`, `routine_id FK`, `user_id FK`, `UNIQUE(routine_id, user_id)` |

### QA/연동 체크리스트
- Swagger Try-It로 기본 플로우 확인(생성 201, 삭제 204, 오류코드 처리)
- 날짜/월 포맷, `page=1`, 정렬 `date,desc` 준수
- 에러 시 `code`/`details` 기반 UX 처리

### 미포함(차기 작업)
- 인증/인가(JWT), 비밀번호 해싱(Bcrypt)
- 배포 CORS 도메인(환경변수 주입), prod 프로파일/로그/모니터링

필요 시, 본 문서 하단에 팀별 체크포인트(담당/일정)만 추가해 쓰시면 됩니다.
