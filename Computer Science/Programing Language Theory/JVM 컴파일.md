# JVM 컴파일 과정

1. javac 가 .java 파일을 .class 파일로 만든다
2. jvm이 class 파일을 로드하며 해당 아키텍처(cpu)에 맞기 머신 코드로 컴파일 한다
3. 컴파일된 함수를 class와 연관시켜 class의 method가 호출될 때 compile된 machine code를 실행시킨다

![](https://file.notion.so/f/s/2301952a-63f3-49bc-aef9-89b52e0e25ab/Untitled.png?id=dd557e34-31b7-42a4-880b-95664896b2aa&table=block&spaceId=c17c101c-472c-46ef-bb90-be55e8941139&expirationTimestamp=1691164800000&signature=hSvCekonXiotPpErsioogXhBx3SP7w_i-ZODOilTDcE&downloadName=Untitled.png)


하지만 .class 파일을 실행할때 바로 jvm이 머신코드로 컴파일 하지 않는다.

먼저 bytecode interpreter를 이용해서 bytecode를 실행한다 전체 단 한번 실행되는 코드처럼 굳이 컴파일 할 이유가 없는 바이트 코드를 컴파일하게 되면 시간적 비용이 비효율적으로 소모되기 때문이다. 하지만 여러번 실행을 거치며 해당 코드가 많이 실행되는 코드라고 판단되면(Warmed Hot) 그제서야 JIT-Compiler를 이용하여 컴파일을 진행한다.

![](https://file.notion.so/f/s/e050754e-4cdc-420f-bcd7-e5f9244467f5/Untitled.png?id=39e078f0-c836-46ef-9d41-ddd281f1c063&table=block&spaceId=c17c101c-472c-46ef-bb90-be55e8941139&expirationTimestamp=1691164800000&signature=uMr5h00xl36R6CrllQihFXzip-zbnJTanU_crdF7eyE&downloadName=Untitled.png)

여기서 JIT 컴파일러와 Bytecode Interpreter의 작동방식으로 인하여 다음과 같은 문제가 발생할 수 있습니다

1. JIT 컴파일러의 최적화:
    - JIT 컴파일러는 반복적으로 실행되는 코드를 최적화하기 위해 추적합니다.
    - 이 때, 임계구역의 코드가 최적화 대상이 될 수 있습니다.
    - 최적화된 코드는 순서나 재진입 시의 동작이 예상치 못한 결과를 가져올 수 있습니다.
2. JIT 컴파일러와 인터프리터의 혼용:
    - JIT 컴파일러가 동작하는 동안, 인터프리터도 함께 동작합니다.
    - 이는 최적화된 코드와 인터프리터가 혼재하여 임계구역 접근 제어를 어렵게 만들 수 있습니다.
    - 예를 들어, 최적화된 코드를 실행하는 도중 인터프리터로 전환되면서 임계구역 접근이 동기화되지 않을 수 있습니다.
3. 컴파일러 최적화와 hoisting:
    - JIT 컴파일러는 코드를 최적화하기 위해 hoisting 기법을 사용할 수 있습니다.
    - hoisting은 반복문 안에서 반복적으로 실행되는 코드를 반복문 밖으로 옮기는 최적화 기법입니다.
    - 이 때, 임계구역 관련 코드가 hoisting되면 임계구역 접근 제어가 제대로 이루어지지 않을 수 있습니다.