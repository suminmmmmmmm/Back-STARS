# Back-STARS
SK쉴더스 루키즈 최종 프로젝트 **백엔드 리포지토리**입니다.

## 프로젝트 소개
관광지 혼잡도 예측 및 스마트 관광 추천 시스템은 **기상 정보, 관광지 방문객 데이터, 문화행사 정보 , 인구 밀집도**를 실시간으로 수집 및 분석하여 관광지별 혼잡도를 시각화하고 방문객들에게 최적의 관광 경험을 제공하는 통합 관제 시스템입니다. 

## 프로젝트 구조
<img width="1560" height="880" alt="image" src="https://github.com/user-attachments/assets/72d456f5-c39d-46e1-87ff-3b5b6c687c2d" />
<img width="1502" height="726" alt="image" src="https://github.com/user-attachments/assets/376f7f22-b9c1-41e2-b0eb-ae148980d995" />



🏗 System Architecture

본 프로젝트는 MSA(Microservice Architecture) 기반 백엔드 구조로 설계되었습니다.
개발 단계에서는 서비스별로 포트를 분리하여 독립적으로 개발·테스트하였으며,
배포 환경에서는 Gateway를 통해 단일 엔드포인트로 통합하여 클라이언트가 내부 구조를 인지하지 않도록 구성했습니다.
---
🔌 Service Ports 
| Service | Port |
|--------|------|
| Gateway | 8080 |
| Congestion Service | 8081 |
| Place Service | 8082 |
| User Service | 8083 |

<img width="1650" height="750" alt="image" src="https://github.com/user-attachments/assets/715df914-354a-4a62-ba7a-5dde2956afbc" />

서비스 | API 유형 | 역할 설명
|--------|----------|-------------|
| **Gateway** | REST | 모든 클라이언트 요청의 진입점<br>라우팅, CORS, Timeout 설정 중앙 관리 |
| **User Service** | REST | 회원가입, 로그인, 사용자 정보 관리<br>JWT 기반 인증·인가 및 사용자 식별 |
| **Place Service** | REST | 관광지·음식점·숙박·행사 정보 제공<br>Elasticsearch 기반 장소 검색<br>타사 리뷰 요약 및 관광지 추천 API |
| **Congestion Service** | SSE | 실시간 인구 밀집도, 사고·통제, 날씨 정보 처리<br>SSE 기반 실시간 데이터 스트리밍 제공 |
---

📄 API Documentation (Postman)
https://documenter.getpostman.com/view/29374455/2sB2qZEN9h

📊 ERD
<img width="1470" height="1182" alt="image" src="https://github.com/user-attachments/assets/caa06431-b003-43d3-884b-9749352bb63e" />

NOTION
https://almond-comfort-a8a.notion.site/1-1c0fef49d8d580e29afcd1902561e2ad?pvs=74





## 🧩 주요 기능 (Key Features)

| 기능 | 설명 |
|------|------|
| 회원가입 / 로그인 | 회원가입 시 DB에 사용자 정보 저장 후 인증 정보 기반 로그인 |
| 혼잡도 제공 | 장소별 실시간 인구 밀집 데이터를 기반으로 관광지 혼잡도 시각화 |
| 관광지 추천 | 사용자 선택 조건 및 알고리즘 기준 관광지 추천 |
| 행사 목록 | 서울 지역 진행·예정 행사 목록 제공 |
| 장소 검색 | Elasticsearch 기반 관광지 조건 검색 |
| 챗봇 | 관광 관련 질문에 대한 AI 기반 응답 제공 |
| 유동인구 정보 | 실시간 유동인구 제공 (성별·연령대 확장 가능 구조) |
| 타사 리뷰 요약 | 네이버·카카오 리뷰 감정 분석 후 장단점 요약 |
| 리뷰 작성 | 사용자가 관광지 리뷰 작성 |
| 대중교통 정보 | 관광지 접근을 위한 대중교통 정보 제공 |
---

##담당기능
**Elasticsearch 기반 API 개발**

- 날씨·주차·사고 데이터를 Elasticsearch에 저장하고, 조건별 검색 및 조회가 가능한 API를 설계·개발했습니다.
- 데이터 특성에 맞는 검색 쿼리를 구성하고 중복 데이터를 제거하여 효율적인 조회가 가능하도록 구현했습니다.
- **음식점 데이터 수집 및 PostgreSQL 저장**
    - 외부 API를 연동하여 음식점 데이터를 수집하고, 서비스 데이터 구조에 맞게 가공하여 PostgreSQL에 저장했습니다.
    - 데이터 중복 저장 문제를 분석하고 저장 로직을 수정하여 데이터 정합성을 개선했습니다.
- **회원가입·로그인 API 개발**
    - 회원가입 및 로그인 API를 구현하고 JWT 토큰 기반 인증과 Redis를 활용한 토큰 관리 기능을 적용했습니다.
    - 중복 로그인 처리 등 실제 서비스 운영을 고려한 인증 로직을 보완했습니다.
      
## 🔐 Data & Authentication

- PostgreSQL을 사용하여 사용자 및 서비스 데이터를 관리
- 사용자 인증은 **JWT 기반**
- 발급된 토큰은 **Redis에 저장**하여 만료 및 로그아웃 관리

---

**기술스택**
<img width="1718" height="970" alt="image" src="https://github.com/user-attachments/assets/b316b541-eca1-4ed2-a1f3-595c983b5a34" />
<img width="1714" height="928" alt="image" src="https://github.com/user-attachments/assets/1e55017a-3216-4d89-b2bf-7d2ddbabd1b0" />





