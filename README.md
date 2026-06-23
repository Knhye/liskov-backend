# 집착 — 사회 초년생을 위한 자취 매물 분석 플랫폼

> 경북 소프트웨어 마이스터 고등학교 캡스톤 프로젝트 (2025 동상)

매물 사진을 업로드하면 AI가 위험 요소를 분석하고, GPT 기반 체크리스트와 대처 방안을 자동 생성해 주는 **백엔드 API 서버**입니다.

---

## 기술 스택

| 분류 | 기술 |
|---|---|
| Framework | Spring Boot 3.5 |
| Language | Java 17 |
| ORM | Spring Data JPA |
| Database | MySQL 9.1 |
| Auth | JWT |
| HTTP Client | Spring WebFlux |
| AI | OpenAI GPT API, Custom AI Server |
| CI/CD | GitHub Actions + AWS EC2 |

---

## 주요 기능

| 기능 | 설명 |
|---|---|
| 회원 인증 | JWT 기반 회원가입 · 로그인 · 토큰 갱신 |
| 매물 관리 | 매물 등록 · 조회 · 삭제 (소프트 딜리트) |
| AI 매물 분석 | 매물 사진 업로드 → AI 서버 전송 → 위험도 점수 및 항목별 분석 |
| 대처 방안 생성 | GPT 기반 위험 항목별 맞춤 대처 방안 자동 생성 |
| 체크리스트 | GPT 기반 계약 전 확인사항 체크리스트 자동 생성 및 관리 |
| 대출 정보 | 조건에 맞는 청년 대출 상품 안내 |

---

## 시작하기

### 사전 요구사항

- Java 17+
- MySQL 8.0+
- Gradle

### 환경 설정

`src/main/resources/application-secret.yml` 파일을 생성하고 아래 항목을 설정합니다.

```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/{DB_NAME}
    username: {DB_USERNAME}
    password: {DB_PASSWORD}

jwt:
  secret: {JWT_SECRET_KEY}

gpt:
  api-key: {OPENAI_API_KEY}
```

### 빌드 및 실행

```bash
./gradlew clean build -x test
java -jar build/libs/liskov-backend-0.0.1-SNAPSHOT.jar
```

서버가 실행되면 `http://localhost:8080` 에서 접근할 수 있습니다.

---

## API 개요

| 태그 | 엔드포인트 | 설명 |
|---|---|---|
| **Auth** | `POST /api/auth/signup` | 회원가입 |
| | `POST /api/auth/login` | 로그인 |
| | `POST /api/auth/refresh` | 액세스 토큰 갱신 |
| **Property** | `GET /api/properties` | 내 매물 전체 조회 |
| | `GET /api/properties/{id}` | 매물 단건 조회 |
| | `POST /api/properties` | 매물 등록 |
| | `DELETE /api/properties/{id}` | 매물 삭제 |
| **Analysis** | `POST /api/analysis` | 매물 분석 요청 (이미지 업로드) |
| | `GET /api/analysis/{id}` | 분석 결과 조회 |
| **Solution** | `POST /api/risk/solution` | 대처 방안 생성 |
| | `GET /api/risk/solution/{id}` | 대처 방안 조회 |
| **Checklist** | `POST /api/checklist/generate` | 체크리스트 자동 생성 |
| | `POST /api/checklist` | 체크리스트 저장 |
| | `GET /api/checklist` | 내 체크리스트 전체 조회 |
| | `GET /api/checklist/{id}` | 체크리스트 단건 조회 |
| | `PUT /api/checklist/{id}` | 체크리스트 수정 |
| | `DELETE /api/checklist/{id}` | 체크리스트 삭제 |
| **Loan** | `POST /api/loan` | 대출 정보 안내 |

---

## 프로젝트 구조

```
src/main/java/com/example/liskovbackend/
├── config/          # SecurityConfig, JpaConfig, AppConfig
├── common/
│   ├── security/    # JWT Filter, JwtUtils, Role
│   └── util/        # ApiResponse, UserUtils
├── controller/      # REST API 컨트롤러
├── service/         # 비즈니스 로직
├── repository/      # Spring Data JPA Repository
├── entity/          # JPA 엔티티
├── dto/             # Request / Response DTO
└── global/
    └── exception/   # GlobalExceptionHandler, Custom Exceptions
```

---

## 라이선스

Private — 경북 소프트웨어 마이스터 고등학교 캡스톤 프로젝트
