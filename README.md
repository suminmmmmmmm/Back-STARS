# Back-STARS
SK쉴더스 루키즈 최종프로젝트 백엔드 리포지토리 입니다.

🏗 System Architecture

본 프로젝트는 MSA(Microservice Architecture) 기반 백엔드 구조로 설계되었습니다.
개발 단계에서는 서비스별로 포트를 분리하여 독립적으로 개발·테스트하였으며,
배포 환경에서는 Gateway를 통해 단일 엔드포인트로 통합하여 클라이언트가 내부 구조를 인지하지 않도록 구성했습니다.

🔌 Service Ports (Local Development)
Service	Port
Gateway	8080
Congestion Service	8081
Place Service	8082
User Service	8083
<img width="1650" height="750" alt="image" src="https://github.com/user-attachments/assets/715df914-354a-4a62-ba7a-5dde2956afbc" />
본 프로젝트는 **MSA 기반 백엔드 구조**로 설계되었습니다.
> 
| 구조           | 설명                                             |
| ------------ | ---------------------------------------------- |
| **Gateway**   |모든 클라이언트 요청의 진입점 / 라우팅, CORS, Timeout 설정을 중앙에서 관리  |
| **User Service (REST API)**   | 회원가입, 로그인, 사용자 정보 관리 / 인증&인가 처리 및 사용자 식별 책임     |
| **Place Service (REST API)**   | 관광지, 음식점, 숙박, 행사 정보 제공/ Elasticsearch 기반 장소 검색 및 조회 담당/ 타사 리뷰 요약, 관광지 추천 API 제공         |
| **Congestion Service (SSE API)**    | 실시간 인구 밀집도, 사고·통제, 날씨 정보 처리 / Server-Sent Events(SSE)를 통해 클라이언트에 실시간 스트리밍 제공            |

<details>
<summary>로컬에서 postgreSQL 테스트</summary>

1. Docker 이미지 다운로드 및 컨테이너 실행
    `docker pull postgres:latest`

2. PostgreSQL 컨테이너 실행
    `docker run --name my-postgres -e POSTGRES_USER=root -e POSTGRES_PASSWORD=admin -e POSTGRES_DB=stars_db -p 5432:5432 -d postgres:latest`

3. Spring Boot 애플리케이션 설정
    - 이제, Spring Boot 애플리케이션에서 PostgreSQL과 연결 설정. application.properties에 PostgreSQL 데이터베이스 설정 추가
    ```
    spring.datasource.url=jdbc:postgresql://localhost:5432/stars_db
    spring.datasource.username=root
    spring.datasource.password=admin
    spring.datasource.driver-class-name=org.postgresql.Driver
    spring.jpa.database-platform=org.hibernate.dialect.PostgreSQLDialect
    spring.jpa.hibernate.ddl-auto=update
    ```
</details>


<details>
<summary>PostgreSQL과 프로젝트 같이 띄우는 법</summary>

1. 프로젝트 최상위 디렉토리 (/place-service, docker-compose.yml과 Dockerfile이 있는 위치)에서 docker compose up --build 실행
2. 빌드가 완료되면 자동으로 Spring 로고가 나오면서 실행됨
3. 다른 cmd 창에서 docker exec -it my_postgres bash 실행
4. psql -U root -d stars_db 실행하면 접속이 될 것임
5. 접속한 후 \dt 로 테이블 존재 확인 가능, select 문으로 데이터 확인 가능
+ select * from area; 로 결과를 본 후, q 를 눌러야 다시 명령창으로 돌아갈 수 있음

</details>

<summary>토큰 redis에 저장</summary>


📄 API Documentation (Postman)
https://documenter.getpostman.com/view/29374455/2sB2qZEN9h



📊 ERD
https://www.erdcloud.com/d/hC5ZaGYqaP3oha66s





🧩 주요 기능 (Key Features)
| 기능           | 설명                                             |
| ------------ | ---------------------------------------------- |
| **회원가입/로그인**   |회원가입 시 DB에 유저정보가 등록되어 사용자 인증 정보를 통해 로그인     |
| **혼잡도 제공**   | 장소별 실시간 인구 밀집 데이터를 기반으로 관광지 혼잡도를 시각화하여 제공      |
| **관광지 추천**   | 사용자 선택 조건 및 알고리즘 기준에 따라 관광지 추천 목록 제공           |
| **행사 목록**    | 현재 서울에서 진행 중이거나 예정된 문화·관광 행사 목록 제공             |
| **장소 검색**    | 검색 엔진(Elasticsearch)을 활용하여 등록된 관광지를 조건 기반으로 검색 |
| **챗봇**       | 사용자의 관광 관련 질문에 대해 AI 기반 답변 제공                  |
| **유동인구 정보**  | 관광지의 실시간 유동인구 수를 제공하며, 성별·연령대별 정보 확장 가능 구조     |
| **타사 리뷰 요약** | 네이버지도·카카오맵 리뷰를 감정 분석하여 장점/단점을 요약 제공            |
| **리뷰 작성**    | 사용자가 관광지에 대한 후기를 직접 작성할 수 있는 기능                |
| **대중교통 정보**  | 관광지 접근에 필요한 대중교통(지하철·버스 등) 정보 제공               |


**기술스택**
<img width="1718" height="970" alt="image" src="https://github.com/user-attachments/assets/b316b541-eca1-4ed2-a1f3-595c983b5a34" />
<img width="1714" height="928" alt="image" src="https://github.com/user-attachments/assets/1e55017a-3216-4d89-b2bf-7d2ddbabd1b0" />




