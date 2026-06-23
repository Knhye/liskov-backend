<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=4F8EF7&height=200&section=header&text=집착&fontSize=80&fontColor=ffffff&fontAlignY=38&desc=사회%20초년생을%20위한%20자취%20매물%20분석%20플랫폼&descAlignY=60&descSize=20" width="100%"/>

<br/>

[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.5.6-6DB33F?style=for-the-badge&logo=springboot&logoColor=white)](https://spring.io/projects/spring-boot)
[![Java](https://img.shields.io/badge/Java-17-007396?style=for-the-badge&logo=openjdk&logoColor=white)](https://openjdk.org/)
[![MySQL](https://img.shields.io/badge/MySQL-9.1-4479A1?style=for-the-badge&logo=mysql&logoColor=white)](https://www.mysql.com/)
[![AWS EC2](https://img.shields.io/badge/AWS%20EC2-Deploy-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white)](https://aws.amazon.com/ec2/)
[![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-CI%2FCD-2088FF?style=for-the-badge&logo=githubactions&logoColor=white)](https://github.com/features/actions)

<br/>

> 🏆 **경소마고 2025년도 2학기 캡스톤 프로젝트 동상(4위) 수상**  
> 사회 초년생이 안전하게 자취방을 구할 수 있도록 AI 기반 매물 분석과 맞춤형 가이드를 제공하는 플랫폼

</div>

---

## 📖 목차

- [서비스 소개](#-서비스-소개)
- [주요 기능](#-주요-기능)
- [기술 스택](#-기술-스택)
- [시스템 아키텍처](#-시스템-아키텍처)
- [API 명세](#-api-명세)
- [프로젝트 구조](#-프로젝트-구조)
- [로컬 실행 방법](#-로컬-실행-방법)
- [CI/CD](#-cicd)

---

## 🏠 서비스 소개

**집착**은 자취방을 처음 구하는 사회 초년생을 위해 만들어진 플랫폼입니다.  
매물 사진을 업로드하면 AI가 위험 요소를 분석하고, GPT 기반으로 체크리스트와 대처 방안을 자동 생성해 줍니다.  
더 이상 혼자 막막하게 집 구하지 마세요.

---

## ✨ 주요 기능

| 기능 | 설명 |
|------|------|
| 🔐 **회원 인증** | JWT 기반 로그인 / 회원가입 / 토큰 갱신 |
| 🏘️ **매물 관리** | 매물 등록 · 조회 · 삭제 (소프트 딜리트) |
| 🔍 **AI 매물 분석** | 매물 사진 업로드 → AI 서버 전송 → 위험도 점수 및 항목별 분석 결과 반환 |
| 🛡️ **대처 방안 생성** | GPT 기반 위험 항목별 맞춤 대처 방안 자동 생성 |
| ✅ **체크리스트** | GPT 기반 계약 전 확인사항 체크리스트 자동 생성 및 관리 |
| 💰 **대출 정보** | 조건에 맞는 청년 대출 상품 안내 |

---

## 🛠 기술 스택

### Backend
![Java](https://img.shields.io/badge/Java%2017-007396?style=flat-square&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot%203.5-6DB33F?style=flat-square&logo=springboot&logoColor=white)
![Spring Security](https://img.shields.io/badge/Spring%20Security-6DB33F?style=flat-square&logo=springsecurity&logoColor=white)
![Spring Data JPA](https://img.shields.io/badge/Spring%20Data%20JPA-6DB33F?style=flat-square&logo=hibernate&logoColor=white)
![WebFlux](https://img.shields.io/badge/Spring%20WebFlux-6DB33F?style=flat-square&logo=spring&logoColor=white)
![JWT](https://img.shields.io/badge/JWT-000000?style=flat-square&logo=jsonwebtokens&logoColor=white)

### Database & Infra
![MySQL](https://img.shields.io/badge/MySQL%209.1-4479A1?style=flat-square&logo=mysql&logoColor=white)
![AWS EC2](https://img.shields.io/badge/AWS%20EC2-FF9900?style=flat-square&logo=amazonec2&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white)

### AI / External
![OpenAI](https://img.shields.io/badge/GPT%20API-412991?style=flat-square&logo=openai&logoColor=white)
![Custom AI](https://img.shields.io/badge/Custom%20AI%20Server-FF6F61?style=flat-square&logo=serverfault&logoColor=white)

---

## 🏗 시스템 아키텍처

```
┌─────────────────────────────────────────────────────────┐
│                     Client (Frontend)                   │
└───────────────────────────┬─────────────────────────────┘
                            │ REST API
┌───────────────────────────▼─────────────────────────────┐
│              Spring Boot Application (EC2)              │
│                                                         │
│  ┌─────────────┐  ┌──────────────┐  ┌───────────────┐  │
│  │  Auth API   │  │ Property API │  │ Analysis API  │  │
│  │  /api/auth  │  │/api/properties│  │ /api/analysis │  │
│  └─────────────┘  └──────────────┘  └───────┬───────┘  │
│                                             │           │
│  ┌──────────────┐  ┌─────────────┐         │           │
│  │Checklist API │  │  Loan API   │         │           │
│  │/api/checklist│  │  /api/loan  │         │           │
│  └──────┬───────┘  └──────┬──────┘         │           │
│         │                 │                │           │
│  ┌──────▼─────────────────▼──────┐  ┌──────▼───────┐  │
│  │       GPT OSS Service         │  │  AI Server   │  │
│  │     (Spring WebFlux)          │  │ (Image 분석) │  │
│  └───────────────────────────────┘  └──────────────┘  │
│                                                         │
│  ┌─────────────────────────────────────────────────┐   │
│  │              MySQL (JPA + Auditing)              │   │
│  └─────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────┘
```

---

## 📋 API 명세

<details>
<summary><b>🔐 인증 (Auth)</b></summary>

| Method | Endpoint | 설명 |
|--------|----------|------|
| `POST` | `/api/auth/signup` | 회원가입 |
| `POST` | `/api/auth/login` | 로그인 |
| `POST` | `/api/auth/refresh` | 액세스 토큰 갱신 |

</details>

<details>
<summary><b>🏘️ 매물 (Property)</b></summary>

| Method | Endpoint | 설명 |
|--------|----------|------|
| `GET` | `/api/properties` | 내 매물 전체 조회 |
| `GET` | `/api/properties/{id}` | 매물 단건 조회 |
| `POST` | `/api/properties` | 매물 등록 |
| `DELETE` | `/api/properties/{id}` | 매물 삭제 |

</details>

<details>
<summary><b>🔍 매물 분석 (Analysis)</b></summary>

| Method | Endpoint | 설명 |
|--------|----------|------|
| `POST` | `/api/analysis` | 매물 분석 요청 (이미지 업로드) |
| `GET` | `/api/analysis/{id}` | 분석 결과 조회 |

</details>

<details>
<summary><b>🛡️ 대처 방안 (Solution)</b></summary>

| Method | Endpoint | 설명 |
|--------|----------|------|
| `POST` | `/api/risk/solution` | 대처 방안 생성 |
| `GET` | `/api/risk/solution/{id}` | 대처 방안 조회 |

</details>

<details>
<summary><b>✅ 체크리스트 (Checklist)</b></summary>

| Method | Endpoint | 설명 |
|--------|----------|------|
| `POST` | `/api/checklist/generate` | 체크리스트 자동 생성 |
| `POST` | `/api/checklist` | 체크리스트 저장 |
| `GET` | `/api/checklist` | 내 체크리스트 전체 조회 |
| `GET` | `/api/checklist/{id}` | 체크리스트 단건 조회 |
| `PUT` | `/api/checklist/{id}` | 체크리스트 수정 |
| `DELETE` | `/api/checklist/{id}` | 체크리스트 삭제 |

</details>

<details>
<summary><b>💰 대출 (Loan)</b></summary>

| Method | Endpoint | 설명 |
|--------|----------|------|
| `POST` | `/api/loan` | 대출 정보 안내 |

</details>

---

## 📁 프로젝트 구조

```
src/main/java/com/example/liskovbackend/
├── config/              # SecurityConfig, JpaConfig, AppConfig
├── common/
│   ├── security/        # JWT Filter, JwtUtils, Role
│   └── util/            # ApiResponse, UserUtils
├── controller/          # REST API 컨트롤러
├── service/             # 비즈니스 로직
├── repository/          # Spring Data JPA Repository
├── entity/              # JPA 엔티티
├── dto/                 # Request / Response DTO
└── global/
    └── exception/       # GlobalExceptionHandler, Custom Exceptions
```

---

## 🚀 로컬 실행 방법

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
# 빌드
./gradlew clean build -x test

# 실행
java -jar build/libs/liskov-backend-0.0.1-SNAPSHOT.jar
```

서버가 기본적으로 `http://localhost:8080` 에서 실행됩니다.

---

## ⚙️ CI/CD

`master` 브랜치에 push 시 **GitHub Actions**가 자동으로 AWS EC2에 배포합니다.

```
Push to master
    │
    ▼
GitHub Actions (ubuntu-latest)
    │
    ├── Checkout code
    ├── SSH into EC2
    ├── git pull
    ├── gradle clean build -x test
    └── java -jar (nohup background)
```

---

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=4F8EF7&height=120&section=footer" width="100%"/>

</div>
