1. 새로운 레포지토리 생성
   설명:
   GitHub에서 새로운 레포지토리 challenge-backend-20-를 생성합니다.

URL: https://github.com/rivkode/challenge-backend-20-.git
역할:

새로운 레포지토리의 생성.
이후 기존 레포지토리의 내용을 복사해 올 공간을 마련.
2. 기존 레포지토리를 bare clone
   bash
   코드 복사
   git clone --bare https://github.com/rivkode/wanted-preonboarding-challenge-backend-20.git
   설명:
   기존 레포지토리를 bare 형식으로 클론합니다.

역할:

작업 디렉토리 없이 Git 메타데이터와 객체만 포함된 bare 리포지토리를 생성.
주로 원격 저장소를 복사할 때 사용되며, 커밋 기록, 브랜치, 태그 등 모든 정보를 그대로 복사합니다.
3. 클론된 디렉토리로 이동
   bash
   코드 복사
   cd wanted-preonboarding-challenge-backend-20.git
   설명:
   클론된 bare 리포지토리 디렉토리로 이동합니다.

역할:

다음 단계에서 mirror-push를 수행할 수 있도록 클론된 bare 리포지토리 디렉토리로 이동합니다.
4. 새로운 레포지토리로 mirror-push
   bash
   코드 복사
   git push --mirror https://github.com/rivkode/challenge-backend-20-.git
   설명:
   새로운 레포지토리로 모든 참조(브랜치, 태그 등)를 복사하여 푸시합니다.

역할:

기존 레포지토리의 모든 브랜치와 태그를 새로운 레포지토리로 완벽하게 복제.
기존의 커밋 기록을 포함한 모든 정보를 새로운 레포지토리로 이전합니다.
5. 클론된 임시 디렉토리 삭제
   bash
   코드 복사
   cd ..
   rm -rf wanted-preonboarding-challenge-backend-20.git
   설명:
   작업이 완료되면 클론된 bare 리포지토리 디렉토리를 삭제합니다.

역할:

더 이상 필요 없는 임시 디렉토리를 삭제하여 로컬 환경을 정리합니다.
추가 설정: 기본 브랜치 변경
설명:
GitHub에서 새로운 레포지토리(challenge-backend-20-)의 기본 브랜치를 feature/jonghun-lee로 설정합니다.

역할:

새로운 레포지토리에서 feature/jonghun-lee 브랜치를 기본 브랜치로 설정하여 커밋 기록을 유지하고 작업을 계속할 수 있게 합니다.
위 과정을 통해 기존 레포지토리의 모든 커밋 기록이 새로운 레포지토리로 복사되고, 커밋 기록이 유지되며, 초록 잔디를 확인할 수 있습니다. 각 단계가 하는 역할을 잘 이해하고 진행하면 문제 없이 작업을 완료할 수 있습니다.