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