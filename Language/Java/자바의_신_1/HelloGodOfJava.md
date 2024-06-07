# Hello God Of Java

java를 직접 컴파일 하고 실행해보자

command 창에서 `set %PATH%` 명령을 하게 되면 Path를 확인해볼 수 있다.

# HelloGodOfJava 만들기

자바 프로그램을 실행하는 과정은 `코드작성 → 컴파일 → 실행` 순으로 진행된다.

여기서 컴파일은 javac 를 통해서 .java 파일을 .class 파일로 컴파일할 수 있으며 .class 파일을 실행하기 위해서는 java 명령어를 통해서 .class 파일을 실행할 수 있다.

# HelloGodOfJava 컴파일하고 실행하기

폴더에 HelloGodOfJava.java 파일이 있다면

`javac HelloGodOfjava.java` 명령어로 컴파일을 할 수 있다.

그러면 HelloGodOfJava.class 파일이 생성되고

`java HelloGodOfJava` 명령어로 해당 .class 파일을 실행할 수 있다.

하지만 실행하게 되면

`Exception in thread "main" java.lang.NoSuchMEthodError: main` 을 만나게 된다.

이는 main 스레드에 main 메서드가 없어서 예외가 발생했다는 의미이다.

# main 메서드를 만들자

main() 메서드의 형태는 아래와 같이 생겼다

```java
public static void (String[] args) {
}
```

java 명령으로 시작하는 자바 프로그램은 이 main() 메서드가 코드의 진입점이 된다.

## 스스로의 질문

```java
public class Calculator {
    public static void main(String[] args) {
        Profile p = new Profile("jonghun", 110);

        p.printProfile();
    }
}
```

```java
public class Profile {
    private String name;
    private int age;

    public Profile(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public void setName(String name) {
        this.name = name;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public void printProfile() {
        System.out.println("My Name is : " + this.name + "My age is : " + this.age);
    }
}
```

에서 아래와 같이 컴파일을 하게 되면 정상적으로 자바 프로그램이 실행될까 ?

현재 상황

- a 디렉터리에 Calculator.java, Profile .java 파일이 존재한다.
- http://Calculator.java 만 컴파일을 하고 http://Profile.java 파일은 컴파일 하지 않는다
- http://Calculator.java 파일 내에서 Profile 을 호출하고 있다.

```java
// 컴파일 명령어
javac Calculator.java

// 실행 명령어
java Calculator
```

실행이 가능하다.

이유는 ?

의존성을 자동적으로 처리해주기 때문이다.

요약해보면

`javac` 컴파일러는 `Calculator` 클래스가 `Profile` 클래스를 참조하는 것을 인식하고, `Profile.java` 파일을 자동으로 찾아 컴파일합니다. 따라서 `Calculator.java` 파일만 컴파일하더라도 두 파일이 모두 컴파일되어 프로그램이 정상적으로 실행될 수 있습니다.

이 자동 의존성 처리 덕분에, 다음과 같은 컴파일 명령어는 종종 모든 의존 파일을 명시하지 않고도 사용할 수 있습니다