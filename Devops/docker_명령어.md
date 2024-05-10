# Docker compose 명령어

시나리오

- 현재 위치는 프로젝트 루트 위치
- Dockerfile 존재
- docker-compose.yml 존재
- gradlew 존재

<br>

```
# gradlew 빌드
./gradlew build -x test

# docker build
docker build -t jonghuni/synergy_be:0.1 .

# 만약 cache를 하고싶지 않다면
docker build --no-cache -t jonghuni/synergy_be:0.1 .

# docker compose 실행
docker compose up -d
```

