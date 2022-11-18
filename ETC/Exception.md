## 오류와 예외

오류와 예외를 혼동하는 경우가 많은데 이 둘을 분리하여 생각해야 합니다.

오류(error)는 시스템이 종료되어야 할 수준의 상황과 같이 수습할 수 없는 심각한 문제를 의미합니다.  개발자가 이를 미리 예측하여 방지할 수 없습니다.

반면 예외(Exception)는 개발자가 구현한 로직에서 발생한 실수나 사용자의 영향에 의해 발생합니다.

오류와 달리 개발자가 미리 예측하여 방지할 수 있기에 상황에 맞는 예외처리(Exception Handle)를 해야합니다.

<br>

### 예외

예외 처리는 크게 아래 3 블록으로 구분할 수 있습니다.

> **try, catch, finally**

try 부분에서는 예외 상황을 미리 예측하고 처리할 수 있습니다.

catch 부분은 try에서 예외 상황이 발생 시 발생한 오류와 관련된 Exception을 처리합니다.

finally는 예외의 발생여부과 관계 없이 무조건 실행됩니다.

![](https://velog.velcdn.com/images/rivkode/post/47df9ca2-520b-4962-a56c-14e9b004edaa/image.png)

<br>


아래 예시는 자바에서 정수 int형을 0으로 나눌때 발생되는 ArithmeticException 예외 발생 예시입니다.

```java
public class ExceptionExam {
        public static void main(String[] args) {
            int i = 10;
            int j = 0;
            try{
                int k = i / j; // 예상되는 예외 구문
                System.out.println(k);
            }catch(ArithmeticException e){ // 예외 발생시 실행되는 구문
                System.out.println("0으로 나눌 수 없습니다. : " + e.toString());
            }finally { // 예외와 관계없이 실행되는 구문
                System.out.println("오류가 발생하든 안하든 무조건 실행되는 블록입니다.");
            }
        }
    }
```

<br>

실행결과는 아래와 같습니다.

<br>

```
0으로 나눌 수 없습니다. : java.lang.ArithmeticException: / by zero

오류가 발생하든 안하든 무조건 실행되는 블록입니다.
```
<br>

i 와 j 에 정수를 할당하고 try 구문을 실행하는 시점에 integer을 0으로 나누게 되면 ArithmeticException 예외가 발생되어 나눈 값인 k가 출력되지 않고 catch 구문으로 이동합니다.

따라서 해당 예외 정보를 출력한 후 finally 구문으로 이동하여 해당 print문을 출력 후 종료됩니다.

<br>

## 예외처리의 throws, throw new 키워드의 역할은 뭘까요 ?

예외처리를 할때 try catch 문과 함께 throws, throw new 를 자주 볼 수 있습니다.
throws 란 해석 그대로 예외를 던져준다라는 의미를 가집니다.


즉 throws 키워드를 사용한다는 것은 예외 발생이 예상되는 메소드에서 처리하는 것이 아니고 _"해당 메소드를 받는 부분에서 다시 처리를 해주기 위해 예외를 던진다."_ 라고 생각하면 된다.

다시 말해  **예외**를 **폭탄**이라고 생각한다면 여러사람이 둘러앉아 하나의 폭탄을 놔두고 서로에게 던지는 상황을 생각하면 이해하기 쉬울 듯 합니다.

이 상황에서 처리를 한다는 것은 마지막에 **예외**를 받는 사람이 예상되는 **예외**에 대해 catch 문으로 받은 뒤 원하는 동작을 실행하는 것 입니다.


<br>


아래 예시는 **throws 상황을 연출**하기 위해 만들어졌습니다.
<br>

>inputStream, outputStream 을 close 할때
2개의 IOException 발생이 예상됨

ByteExam2.java

```java
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;

public class ByteExam2 {
    public static void main(String[] args){
        long startTime = System.currentTimeMillis();

        FileInputStream fis = null;
        FileOutputStream fos = null;
        try {
            fis = new FileInputStream("src/programmers/intermediate/IO/ByteExam2.java");
            fos = new FileOutputStream("byte.txt");

            int readCount = -1;
            byte[] buffer = new byte[512];
            while((readCount = fis.read(buffer))!= -1){
                fos.write(buffer, 0, readCount);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }finally{
            try {  
                fos.close(); // 예외발생
            } catch (IOException e) {
                e.printStackTrace();
            }
            try { 
                fis.close(); // 예외발생
            } catch (IOException e) {
                e.printStackTrace();
            }
        }

        long endTime = System.currentTimeMillis();

        System.out.println(endTime - startTime);
    }
}
```

<br>

### throws (예외 던지기)
### throw new (예외 생성)



>예외 발생을 메소드 분리 및 thorw new, throws 를 통해 처리

ByteExam2.java - 예외를 처리
FioCloseException.java - 예외를 던짐
FisCloseException.java - 예외를 던짐


<br>

ByteExam2.java

```java
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;

public class ByteExam2 {
    public static void main(String[] args){
        long startTime = System.currentTimeMillis();

        FileInputStream fis = null;
        FileOutputStream fos = null;
        try {
            fis = new FileInputStream("src/programmers/intermediate/IO/ByteExam2.java");
            fos = new FileOutputStream("byte.txt");

            int readCount = -1;
            byte[] buffer = new byte[512];
            while((readCount = fis.read(buffer))!= -1){
                fos.write(buffer, 0, readCount);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }finally{
            try {
                FioCloseException.fioCloseException(fos);
            } catch (IOException e) {
                e.printStackTrace();
            }
            try {
                FisCloseException.fisCloseException(fis);
            } catch (IOException e) {
                e.printStackTrace();
            }
        }

        long endTime = System.currentTimeMillis();

        System.out.println(endTime - startTime);
    }
}

```

FioCloseException.java


```java
import java.io.FileOutputStream;
import java.io.IOException;

public class FioCloseException {
    public static void fioCloseException(FileOutputStream fos) throws IOException{
        try {
            fos.close();
        } catch (IOException e) {
            throw new IOException();
        }
    }
}

```




FisCloseException.java

```java
import java.io.FileInputStream;
import java.io.IOException;

public class FisCloseException {
    public static void fisCloseException(FileInputStream fis) throws IOException{
        try {
            fis.close();
        } catch (IOException e) {
            throw new IOException();
        }
    }
}

```

각각의 동작을 살펴보겠습니다.

FioCloseException.java(예외발생 및 던짐),  FisCloseException.java(예외발생 및 던짐)

위 두 클래스에서 발생된 예외를 ByteExam2.java 에서 catch문으로 다시 받아 e.printStackTrace(); 를 실행

다시말해 각 클래스에서 **폭탄**(예외) 이 발생되었지만 throws 키워드를 사용하여 ByteExam2.java 에서 처리하는 동작입니다.


<br>

[참고자료](https://coding-factory.tistory.com/280)