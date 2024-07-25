# Docker로 스프링 프로젝트 배포하는 과정

배포에 사용되는 것
- 배포할 프로젝트
- docker
- Ec2
- Rds

배포하기 전 준비해야할 것
- spring project를 빌드한 .jar 파일
- docker 계정

배포 진행 과정

간단하게 정리하면

> 빌드한 .jar 파일을 docker image로 만들고 docker hub로 push후 ec2에서 해당 image를 run -d 하는 것이다

- docker hub 로그인
- docker 이미지 빌드
- 빌드한 이미지 dockerhub로 push
- ec2 인스턴스 접속
- 동일한 프로젝트 이전에 실행중인 것 있으면 kill / rm -f
- dockerhub에서 push 한 프로젝트 image docker pull
- 애플리케이션 실행 / docker run

위 내용을 자동화 하는것이 CI/CD

위 내용을 정리한 자료

[Docker 컨테이너로 Spring, MySQL 연동](https://velog.io/@rivkode/Docker-%EC%BB%A8%ED%85%8C%EC%9D%B4%EB%84%88%EB%A1%9C-Spring-MySQL-%EC%97%B0%EB%8F%99)
[Docker compose 로 Spring, MySQL 연동하기 (에러 : docker: 'compose' is not a docker command, docker desktop 삭제 및 설치)](https://velog.io/@rivkode/Docker-compose-%EB%A1%9C-Spring-MySQL-%EC%97%B0%EB%8F%99%ED%95%98%EA%B8%B0-%EC%97%90%EB%9F%AC-docker-compose-is-not-a-docker-command-docker-desktop-%EC%82%AD%EC%A0%9C-%EB%B0%8F-%EC%84%A4%EC%B9%98)
[Github Action, Docker compose를 활용한 배포 자동화 CI/CD + (Spring boot, MySQL)](https://velog.io/@rivkode/Github-Action-Docker-compose%EB%A5%BC-%ED%99%9C%EC%9A%A9%ED%95%9C-%EB%B0%B0%ED%8F%AC-%EC%9E%90%EB%8F%99%ED%99%94-CICD-Spring-boot-MySQL)
[Docker Nginx에서 HTTPS를 위한 SSL 인증서 적용 (Let's encrypt, Docker compose)](https://velog.io/@rivkode/Docker-Nginx%EC%97%90%EC%84%9C-HTTPS%EB%A5%BC-%EC%9C%84%ED%95%9C-SSL-%EC%9D%B8%EC%A6%9D%EC%84%9C-%EC%A0%81%EC%9A%A9-Lets-encrypt-Docker-compose)

