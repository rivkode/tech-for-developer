NCP 문서 읽기

# 전체적인 순서

1. 서버 생성
2. 포트 포워딩, 공인 IP 설정
   a. 서버를 서비스 목적으로 이용하거나 VPC 환경에서 생성한 서버에 접속하기 위해 공인 IP를 할당합니다. 또한 Classic 환경에서는 비공인 IP만 할당된 서버에 인터넷을 통해 접속하기 위해 포트 포워딩을 설정합니다. 참고할 수 있는 사용 가이드는 다음과 같습니다.
3. ACG 설정
   a. 생성된 서버의 네트워크 접근을 제어하기 위해 방화벽 역할을 하는 ACG(Access Control Group)를 설정합니다. 참고할 수 있는 사용 가이드는 다음과 같습니다.
4. 관리자 비밀번호 확인
5. 서버 접속
   a. 접속시 putty 사용
6. 서버 사용

todo
1. java 설치
2. docker 설치
3. docker compose 실행

# linux 환경에서 java 설치

1. sudo  권한으로 apt 업데이트 후 openjdk 17버전을 설치한다
sudo apt update

2. 설치한 java 버전을 확인한다.
sudo apt install openjdk-17-jdk

3. 설치된 java 경로를 확인한다.
java --version

4. environment 파일에서 JAVA_HOME 환경변수를 설정합니다.

```
PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin"
JAVA_HOME="/usr/lib/jvm/java-17-openjdk-amd64"
```


5. source 명령어를 실행하여 변경값이 적용되었는지 확인합니다.
```
source /etc/environment
echo $JAVA_HOME
```


# docker 설치

sudo apt-get update

필요한 패키지 설치
sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common

gpg키 및 저장소 추가

sudo mkdir -p /etc/apt/keyrings

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg


```
echo \
"deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
$(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

도커엔진설치

sudo apt update

sudo apt install docker-ce docker-ce-cli containerd.io

도커 버전 확인

sudo docker version

컨테이너 실행 테스트
sudo docker run --rm hello-world

스프링 부트 실행

프로젝트 클론
git clone 프로젝트

application.properties, docker-compose.yml, Dockerfile 추가

# docker compose 캐시 하지 않고 빌드하기

./gradlew build -x test

docker compose build --no-cache

docker compose up