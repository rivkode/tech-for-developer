# 상속 , @Transactional

다룰 키워드
- Proxy 객체
- @Transactional 동작 원리
- 스프링 컨테이너
- 상속 메서드

## 내용 설명

아래 BookService 클래스는 3개의 메서드 saveAllAndPrint(), saveAll(), save() 를 가지고 있다

스프링이 시작된 이후 어떤 과정을 거치는지 살펴보자

1. 스프링 IOC 컨테이너에서 @Service 내에 있는 @Component 어노테이션이 달린 클래스에 대해 정보를 가지고 있는다
2. BookService 를 컨테이너에 가져와서 보니 @Transactional 어노테이션을 달고 있는 메서드가 있으므로 기존의 BookService 클래스가 아닌 BookServiceProxy 객체를 새로 만들어 BookService를 상속받게 한다
3. 이 Proxy 객체에 대해 @Transactional 이 달린 메서드에 대해서는 메서드 시작부분에 startTransaction(), 종료부분에는 commit() 를 넣어줌으로써 Transaction 을 보장해준다
4. 그렇다면 아래 예시에서 각 메서드를 호출했을때 모든 메서드가 Transaction이 보장되는지 살펴보자


### save()

먼저 다른 클래스에서 BookService.save()로 메서드를 호출했다고 가정해보자

그렇다면 이는 @Transactional 이 붙어있는 메서드로 Proxy 객체에서 Transaction이 보장된다

왜 보장이 되는지 알아보자

BookService 클래스가 컨테이너로 들어갈때 BookService가 가지고 있는 메서드 중 save()는 @Transactional 어노테이션이 붙어있는 메서드이므로 시작점과 끝점에 각 startTransaction(), commit() 이 붙게된다

따라서 해당 메서드에 대해서는 Transaction이 보장된다

### saveAll()

saveAll()도 마찬가지로 BookService.saveAll()로 메서드를 호출했다고 가정한다

이 메서드 또한 @Transactional 이 붙어있는 메서드로 Transaction이 보장된다

다만 여기 saveAll() 에서는 save()를 호출하고 있는 방식이다

**BookService에서 호출하고 있는 save()는 BookService의 save() 일까 혹은 BookServiceProxy 의 save() 일까 ??**

분명 BookServiceProxy 는 BookService를 상속받고 있다

그렇다면 Proxy 객체에서 메서드를 호출하였을때는 어떤 메서드가 호출될까 ?

정답은 BookServiceProxy의 save()이다

왜냐하면 

### saveAllAndPrint()

이 메서드는 @Transactional 어노테이션이 붙어있지 않다

이럴 경우 Transaction이 보장이 될까 ?

보장이 안된다면 그 이유를 알아보자

1. bookService.saveAllAndPrint()를 호출한다
2. proxy 객체의 saveAllANdPrint() 메서드 내부의 super.saveAllAndPrint() 를 호출한다
3. super.saveAllAndPrint()는 부모의 메서드를 의미하므로 BookService.saveAllAndPrint()를 호출한다
4. saveAll() 과 println이 호출된다
5. 이 과정에서 saveAll()는 bookService 의 saveAll()이므로 Transaction ACID를 보장받지 못한다

위 과정을 통해 왜 saveAllAndPrint()가 Transaction 을 보장받지 못하는지 알아보았다



```java
package com.bigtech.abc.post;

import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;

import java.awt.print.Book;
import java.util.ArrayList;
import java.util.List;

@Service
public class BookService {

    public void saveAllAndPrint(List<Integer> numbers) {
        saveAll(numbers);
        System.out.println(numbers);
    }

    @Transactional
    public void saveAll(List<Integer> numbers) {
        //
        numbers.forEach((i -> save(i)));
        var n = numbers;
    }

    @Transactional
    public void save(Integer i) {
        if (i == 5) {
            throw new RuntimeException();
        }
        // save
    }

    /**
     * 스프링 내부에서 생성한 Proxy 객체, 실제 .java 코드에서는 보이지 않음
     */
    public class BookServiceProxy extends BookService {

        public void saveAllAndPrint(List<Integer> numbers) {
            super.saveAllAndPrint(numbers);
        }

        public void saveAll(List<Integer> lst) {
            // 시작
            startTransaction();
            try {
                super.saveAll(lst);
            } catch(Exception e) {
                rollback();
                throw e;
            }

            commit();
            // 커밋
        }

        public void save(Integer i) {
            // 시작
            startTransaction();
            try {
                super.save(i);
            } catch(Exception e) {
                rollback();
                throw e;
            }

            commit();
            // 커밋
        }
      }

      private void startTransaction() {

      }

      private void commit() {

      }

      private void rollback() {

      }


    }
}


```