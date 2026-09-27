# session2-sample

멋쟁이사자처럼 AWS + Docker 배포 세션(2차시) 실습용 샘플 백엔드입니다.
각자 해커톤 프로젝트를 배포하면 팀마다 스택/설정 파일 유무가 달라 실습 중 변수가 많아지기 때문에,
모두가 동일한 이 프로젝트를 clone 받아 배포 실습을 진행합니다.

## 스택

- Java 17
- Spring Boot 3.5.14
- Gradle
- Spring Data JPA + MySQL

## 기능

- `GET /api/posts` — 게시글 목록 조회
- `GET /api/posts/{id}` — 게시글 단건 조회
- `POST /api/posts` — 게시글 작성 (`{"title": "...", "content": "..."}`)
- `DELETE /api/posts/{id}` — 게시글 삭제
- `GET /actuator/health` — 헬스체크 (배포 확인용)

## 로컬에서 실행하기

1. MySQL을 로컬에 설치하고 데이터베이스를 하나 만듭니다.
   ```sql
   CREATE DATABASE session2db;
   ```
2. `src/main/resources/application.yml`의 `username`/`password`를 본인 MySQL 계정 정보로 수정합니다.
3. 실행:
   ```bash
   ./gradlew bootRun
   ```
   (Gradle Wrapper가 없다면 IntelliJ에서 열었을 때 자동으로 생성되거나, `gradle wrapper` 명령으로 만들 수 있습니다. 다만 이 프로젝트를 EC2에 배포할 때는 Gradle Wrapper 없이도 진행 가능합니다 — 세션 실습 자료 참고.)

## 참고

이 프로젝트의 `application.yml`에는 로컬 개발용 기본값이 그대로 들어 있습니다 (일부러 `.gitignore`에서 제외).
실제 배포 시에는 Docker Compose의 환경변수(`SPRING_DATASOURCE_URL` 등)가 이 값을 덮어쓰게 되는데,
이건 Spring Boot의 설정 우선순위(relaxed binding)를 보여주기 위한 의도적인 구성입니다.
