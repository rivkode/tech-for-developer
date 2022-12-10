## 변수 Scope 와 super의 사용

<br>


```java
public class A {
    public int num = 5;
    public int update() {
        num = num-1;
        return num;
    }
}

public class B  extends A{
    public int num = 3;
    public int update() {
        return num + 5;
    }


    public int update() {
        num = num + 5;
        return num;
    }



    public int update2() {
        super.update();
        return num;
    }

    public static void main(String[] args) {
        B b = new B();
        A a = b;
        System.out.println(b.num); // 3
        System.out.println(b.update()); // 8
        System.out.println(a.num); // 5
        System.out.println(a.update()); // 13
        System.out.println(a.num);
    }
}

```

<br>



b 객체를 생성하고 a 변수에 A타입으로 b 객체를 복사하였다.

핵심은 update() 함수에서 어떤 num의 값을 가져오느냐 이다

첫번째의 update() 함수에서는 num  값의 변경이 없이 +5만 해주어 반환하였으므로 이후에 다시 num을 호출하여도 값의 변화 없이 3이 그대로 나오는 것을 볼 수 있다.

두번째의 update() 함수에서는 num 값의 변경이 있다. num = num+5; 로 해당 라인을 만나게 되면 num이 +5 증가하게 된다 그 이후 num을 반환하므로 이후에 num을 다시 호출하면 +5 증가한 값을 볼 수 있다.

<br>

```java
public class A {
    public int num = 5;
    public int update() {
        num = num-1;
        return num;
    }
}

public class B  extends A{
    public int num = 3;
    public int update() {
        num = num + 5;
        return num;
    }

    public int update2() {
        super.update();
        return num;
    }

    public static void main(String[] args) {
        B b = new B();
        A a = b;
        System.out.println(b.num); // 3
        System.out.println(b.update()); // 8
        System.out.println(a.num); // 5
        System.out.println(b.update2());
        System.out.println(a.num);
    }
}

```

<br>


위 코드에서 질문은 update2() 함수의 super이다.

super이란 부모클래스의 참조변수이다.

update2() 함수를 살펴보면 super.update(); 이후에 return 으로 num을 넘기는 것을 볼 수 있다.

이는 부모 클래스인 A로 가서 update()함수를 실행시키는 명령어이다.

따라서 A클래스의 update()함수를 실행시키므로 b의 num에는 아무런 영향을 끼치지 않으므로 b.num = 8 값을 그대로 반환한다.

하지만 A클래스의 num 변수는 update() 함수가 실행되었으므로 -1이 감소하여 이후 a.num을 호출하였을때 5-1 = 4가 호출되는 것을 볼 수 있다.