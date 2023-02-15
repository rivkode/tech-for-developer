# 캐스팅(Casting)

모든 연산에는 같은 타입끼리 연산이 가능합니다.

하지만 다른 타입끼리 연산을 수행해야하는 경우 같은 타입으로 형 변환을 해주는 것을 캐스팅(형변환)이라고 합니다.

형변환에 대해 간단히 알아보겠습니다.
```java
int number1 = 10; // 아무이상 없음

int number2 = 12.34; // 컴파일 오류
```

이는 실수를 정수형 int 자료형에 넣으려 하였기 때문입니다.

실수의 범위가 정수의 범위가 넓으므로 실수를 정수로 표현 불가능한 것과 비슷한 논리라고 생각하시면 편합니다.

이처럼 12.34 값을 int 로 넣어주려면 캐스팅을 해야합니다.

int number2 = (int) 12.34;

이렇게 하게되면 뒤에 소수점은 삭제되고 12 값이 number2 변수에 저장되게 됩니다.

왜냐하면 12.34에서 정수부분은 12이기 때문입니다.

# 업캐스팅

업캐스팅에 대해 알아보겠습니다.

업캐스팅이란 자식 클래스에서 부모 클래스로 형 변환 하는 것을 업캐스팅이라고 합니다.

아래 예시를 보겠습니다.

BridgeNumberGenerator.java
```java
package bridge.domain;

@FunctionalInterface
public interface BridgeNumberGenerator {

    int generate();
}
```


BridgeRandomNumberGenerator.java
```java
package bridge;

import bridge.domain.BridgeNumberGenerator;
import camp.nextstep.edu.missionutils.Randoms;

public class BridgeRandomNumberGenerator implements BridgeNumberGenerator {

    private static final int RANDOM_LOWER_INCLUSIVE = 0;
    private static final int RANDOM_UPPER_INCLUSIVE = 1;

    @Override
    public int generate() {
        return Randoms.pickNumberInRange(RANDOM_LOWER_INCLUSIVE, RANDOM_UPPER_INCLUSIVE);
    }
}
```

BridgeNumberGenerator 인터페이스가 있고

이를 구현한 BridgeRandomNumberGenerator  클래스가 있습니다.

여기서 BridgeRandomNumberGenerator 에서 BridgeNumberGenerator 로 형변환을 하는 것이 업캐스팅입니다.

왜냐하면

BridgeRandomNumberGenerator 에서 인터페이스인 BridgeNumberGenerator 클래스를 implements(상속) 받았기 때문에 더 넓은 범주인 BridgeRandomNumberGenerator 클래스는 부모 클래스인 BridgeNumberGenerator 클래스 형으로 캐스팅을 할 수 있는 것 입니다.

아래와 같이 업캐스팅을 할 수 있습니다.


```java
BridgeNumberGenerator numberGenerator = (BridgeNumberGenerator) new BridgeRandomNumberGenerator();
```

다시말해 업캐스팅의 경우 기본적으로 하위 클래스의 형에서 상위 클래스의 형으로 캐스팅 시키는것입니다. 클래스 형만 정확하다면 묵시적으로 캐스팅이 가능합니다.

# 다운캐스팅

기본적으론 **업캐스팅 한 것을 다시 원래의 형으로 복원 시켜주는 것입니다.**

따라서 업캐스팅과는 다르게 원래의 형을 꼭 명시해주어야합니다.

위의 예제에서 다운 캐스팅을 한다면 아래와 같이 선언할 수 있습니다.

```java
BridgeRandomNumberGenerator randomNumberGenerator = (BridgeRandomNumberGenerator) numberGenerator();
```