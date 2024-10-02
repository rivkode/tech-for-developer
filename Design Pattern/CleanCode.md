# Clean Code

<br>

<br>

# 1장 깨끗한 코드

<br>

```
이 안에 들어있는 내용은 책에 있는 내용이다.
```

아래에 적는 내용은 나의 생각

<br>

<br>

```
한 마디로 요약하면 '주의'다. 이것이 이 책의 주제다. 부제를 붙이라면
'코드를 주의 깊게 짜는 방법'이 적당하겠다.

깨끗한 코드는 주의 깊게 작성한 코드다. 누군가 시간을 들여 깔끔
하고 단정하게 정리한 코드다.

세세한 사항까지 꼼꼼하게 신경 쓴 코드다. 주의를 기울인 코드다.
```

여기서 말하는 주의란 뭘까 ?

내 생각에 여기서 말하는 주의는 코드를 작성하는 사람이 코드를 대하는 모든 능력인 것 같다.

<br>

```
켄트벡이 제안한 단순한 코드 규칙

- 모든 테스트를 통과한다
- 중복이 없다
- 시스템 내 모든 설계 아이디어를 표현한다
- 클래스, 메서드, 함수 등을 최대한 줄인다
```

단순하고 명확하다. 이 내용은 명료하면서도 매우 중요한 내용이니 꼭 기억하자.

<br>

```
여러 기능을 수행하는 객체나 메서드도 찾는다. 객체가 여러 기능을 
수행하면 여러 객체로 나눈다. 메서드가 여러 기능을
수행한다면 메서드 추출 리팩터링 기법을 적용해 기능을 명확히 기술하는
메서드 하나와 기능을 실제로 수행하는 메서드 여러개로 나눈다.
```

여기서 하나의 기능을 어떻게 바라보는게 좋은지가 고민이다.

작은 기능 하나를 확실하게 하는게 좋다고 하는데, 작은 기능을 어떻게 정의하면 좋을까 ?

<br>

```
중복 줄이기, 표현력 높이기, 초반부터 간단한 추상화 고려하기. 내게는 
이 세 가지가 깨끗한 코드를 만드는 비결이다.
```

중복을 줄이기 위해서는 최초로 코드를 작성할 때, 기능을 구성할 때 중복되는 부분이 있는지를 잘 체크하여 구현해 나가는 것도 좋은
방법이라 생각이 된다.

표현력은 좋은 단어, 네이밍이라고 생각이 되는데, 이 부분은 많이 코드를 작성하다 보면 어느 정도 자연스럽게 될 것이라고 생각이 된다.

왜냐하면 자주 사용하는 기능과 내용들이 쌓이다 보면 네이밍을 짓는데에는 약간의 노하우가 생기지 않을까 ?

추상화는 아직 많이 어려운 것 같다. 오늘 회사 코드를 보았는데, 추상화 클래스가 매우 많았다. 그 코드에 녹아든 개념들을 잘 이해하면서
코드를 작성할 때 잘 녹여보자.


<br>

```
보이 스카우트 규칙

캠프장은 처음 왔을 때보다 더 깨끗하게 해놓고 떠나라 
```

나는 이 비유를 듣자말자 화장실이 생각났다.

화장실은 누구나 사용하는 공간이다. 화장실을 들어갈때보다 나갈때 더 깨끗하게 사용해놓고 나간다면 후에 화장실을 사용하는 사람들은
더 그 화장실을 사용하고 싶을 것이다.

그리고 그 사용자는 나 자신이 또한 될 수 있다는 것을 잊지말자.

시간이 지날수록 코드가 깨끗해지는 프로젝트를 상상해보면 너무 좋지 않은가 ? 뭔가 벅차오르기도 한다.

하지만 이는 어찌보면 당연한 얘기기도 하다.

<br>

```
새 코드를 짜면서 우리는 끊임없이 기존 코드를 읽는다. 비율은 10 : 1 
이 넘는다. 이렇게 읽기 비율이 높으므로 읽기 쉬운 코드는 매우 중요하다.
```

새로운 요구사항이 추가되었을때 주어진 시간 내에 잘 구현할 수 있는 방법은 기존의 코드가 읽기 쉽다면 더 빨리 이해하고 구현할 수 있을 것이다.

작은 단위로 잘게 나누고, 추상화를 잘 하고 ... 이는 그 다음 문제이고, 지금 말하고자 하는 것은 우선 코드를 작성할 때 읽기 쉽게 작성해보자는 것이다.
그 기술들 중 하나가 기능을 나누는 것이나 추상화가 된다고 생각한다.

<br>

<br>

# 2장 의미있는 이름

<br>

```
의도를 분명히 밝혀라

int d; // 경과 시간

int elapsedTimeInDays;
int daysSinceCreation;
int daysSinceModification;
int fileAgeInDays;
```

위 코드에서 `d` 가 가지는 의므를 알 수 있는 사람이 있을까 ? 절대 없다.. 그리고 애초에 알려고 하면 안된다.

저렇게 주석으로 적어놓는 것도 큰 문제다. 왜냐고 묻는다면 .. 저 의미를 알기 위해 주석을 찾아본다는 것은 말이 안되니까.

아래에 보이는 것 처럼 가능하면 의미를 가지도록 하는 것이 좋다.

<br>

```
읽는 사람들을 헷갈리게 하는 단어를 사용하지 말자

영어 대문자 O 와 소문자 l 은 단독으로 사용은 하지말자.
```

`O, o, 0, l I`

`o의 대문자, o의 소문자 o, 숫자 0, L의 소문자 l, i의 대문자 I `

어떤가 .. 보기에 비슷하여 헷갈리지 않는가 ? 단독으로 사용하지 말자..

<br>

<br>

# 3장 함수

<br>

```
작게 만들어라

함수를 만드는 첫번째 규칙은 작게 다. 함수를 만드는 둘쨰 규칙은 더 작게 다.

적절한 함수의 줄은 2 - 4줄 정도가 적당하다.
```

함수가 4줄을 넘어간다면 이전의 1, 2 번째에 했던 로직들을 기억하기 위해 다시 되돌아가서 봐야할 것 같다.

그러면 이 부분이 또 비용이 될 수 있으므로 4줄 이하를 제안한다고 생각한다.

당연하게도 함수가 줄이 짧을 수록 로직이 단순해지고 깔끔해지기도 한다. 

<br>

```
한가지만 해라

함수는 한 가지를 해야 한다. 그 한 가지를 잘 해야한다. 그 한 가지만을 해야 한다.
```

코드는 결국 이야기의 흐름이다. 함수가 한가지만 해야하는 이유를 잘 생각해보면, 하나의 주제에 대해 여러 이야기 내용을 담으려고
한다면 이 이야기는 중구난방이 되어버릴 것이다.

예를 들어 작은 클래스 단위로 각 클래스가 가지고 있는 함수의 흐름을 머릿속으로 떠올려 보았을 때, 그 함수들이 가지는 연결고리들을
연결지으면서 흐름을 연상하게 될 것이다.

이때, 이 연상의 흐름이 되는 단위는 함수가 될텐데 이 함수 내에서 만약 한 가지가 아니라 여러가지의 일들을 한다면 그때부터는
머리속이 복잡해질 것이다.

이 연상의 흐름이 되는 함수 단위를 잘게 쪼개어 머릿속으로 더 이해하기 쉽고 명확하게 한다면 더 읽기 쉬운 이해하기 쉬운 코드가 될 것이다.

<br>

```
함수 당 추상화 수준은 하나로

함수가 확실히 '한 가지' 작업만 하려면 함수 내 모든 문장의 추상화 
수준이 동일해야 한다.

예를 들어 `getHtml()` 은 추상화수준이 높다고 할 수 있고,
`String pagePathName = PathParser.render(pagepath);` 는 
추상화 수준이 중간이며,
`.append("\n")` 은 추상화 수준이 낮다고 할 수 있다.

만약 위 로직이 하나의 함수내에 있다면 읽는 사람은 그만큼 추상화 수준을 
높였다가 낮췄다가를 반복해야 한다.

이는 머릿속을 뒤섞기 시작할 것이고, 깨어진 창문처럼 사람들이 함수에 
세부사항을 점점 추가하게 된다.
```

아래에서 그 예시를 보자.

코드를 작성하다 든 생각인데 원래는 추상화 부분만 작성하려 했으나, class나 생성자 등 
다른 부분을 생략하기 보단 이 내용은 중요한 예시 중 하나이므로 최대한 생략하지 않고 자세하게
작성해보았다.

여러번 읽어보고 추상화 수준이 동일하다는게 어떤 의미를 가지는지 스스로 생각해보고 고민해보자.

<br>

<br>

```java
public class SetupTearDownIncluder {
    private PageData pageData;
    private boolean isSuite;
    private WikiPage testPage;
    private StringBuffer newPageContent;
    private PageCrawler pageCrawler;
    
    public static String render(PageData pageData) throws Exception {
        return render(pageData, false);
    }
    
    public static String render(PageData pageData, boolean isSuite) throws Exception {
        return new SetupTearDownIncluder(pageData).render(isSuite);
    }
    
    private SetupTearDownIncluder(PageData pageData) {
        this.pageData = pageData;
        testPage = pageData.getWikiPage();
        pageCrawler = testPage.getPageCrawler();
        newPageContent = new StringBuffer();
    }
    
    private String render(boolean isSuite) throws Exception {
        this.isSuite = isSuite;
        if (isSuite) {
            includeSetupAndTearDownPages();
        }
        return pageData.getHtml();
    }
    
    private boolean isTestPage() throws Exception {
        return pageData.hasAttribute("Test");
    }
    
    private void includeSetupAndTearDownPages() throws Exception {
        includeSetupPages();
        includePageContent();
        includeTeardownPages();
        updatePageContent();
    }
    
    private void includeSetupPages() throws Exception {
        if (isSuite) {
            includeSuiteSetupPage();
        }
        includeSetupPage();
    }
    
    private void includeSuiteSetupPage() throws Exception {
        include(SuiteResponder.SUITE_SETUP_NAME, "-setup");
    }
    
    private void includeSetupPage() throws Exception {
        include("setup", "-setup");
    }
    
    private void includePageContent() throws Exception {
        newPageContent.append(pageData.getContent());
    }
    
    private void includeTeardownPages() throws Exception {
        includeTeardownPage();
        if (isSuite) {
            includeSuiteTeardownPage();
        }
    }
    
    private void includeTeardownPage() throws Exception {
        include("TearDown", "-teardown");
    }
    
    private void includeSuiteTeardownPage() throws Exception {
        include(SuiteResponder.SUITE_TEARDOWN_NAME, "-teardown");
    }
    
    private void updatePageContent() throws Exception {
        pageData.setContent(newPageContent.toString());
    }
    
    private void include(String pageName, String arg) throws Exception {
        WikiPage inheritedPage = findInheritedPage(pageName);
        if (inheritedPage != null) {
            String pagePathName = getPathNameForPage(pageName);
            buildIncludeDirective(pagePathName, arg);
        }
    }
    
    private WikiPage findInheritedPage(String pageName) throws Exception {
        return PageCrawlerImpl.getInheritedPage(pageName, testPage);
    }
    
    private String getPathNameForPage(WikiPage page) throws Exception {
        WikiPagePath pagePath = pageCrawler.getFullPath(page);
        return PathParser.render(pagePath);
    }
    
    private void buildIncludeDirective(String pagePathName, String arg) {
        newPageContent
                .append("\n!include ")
                .append(arg)
                .append(" .")
                .append(pagePathName)
                .append("\n");
    }
}

```

2번 읽고, 3번 읽어보자. 클린코드에서 말하고자하는 추상화 수준이 어떤 것을 의미하는지 이해가 가는가 ?

`추상화 수준` 은 별개 아니고, 각 함수들의 로직 레이어이다.

다시 말해보면

가장 크게는 우리가 패키지 단위로 추상화 수준을 결정할 수 있다. 그리고 패키지 내 클래스, 클래스 내 함수, 함수 내 다시 함수, 함수 다시 함수 ...

로 이어지게 된다.

여기서 각 지점들에 대해 유사한 수준의 동작을 하게끔 결정하는 것이다.

<br>

```
Switch 문은 작게 만들기 어렵다.

다형성을 이용하여 저차원 클래스에 숨기고 반복하지 않도록 하자.
```

<br>

```
서술적인 이름을 사용하자.

testableHtml을 SetupTeardownIncluder 로 변경하였다.
includeSetupAndTeardownPages 등 서술적인 이름을 사용하였다.

이름이 길어도 괜찮다. 길고 서술적인 이름이 짧고 어려운 이름, 길고 
서술적인 주석보다 좋다.
```

<br>

```
함수 인수

함수에서 이상적인 인수 개수는 0개다.

그 다음 1개, 그 다음은 2개다. 3개는 가능하면 피하는 편이 좋다.

4개 이상은 특별한 이유가 필요하다.
```

`includeSetupPageInto(newPageContent);` 는 함수 이름과 인수 사이에 추상화 수준이 다르다.

<br>

```
오류 코드보다 예외를 사용하라

if (deletePage(page) == E_OK) {
    if (registry.deleteReference(page.name) == E_OK) {
    ...
    }
}

위와 같이 if 문으로 오류를 처리하기 보단 예외를 사용하면 오류 처리 코드가 
원래 코드에서 분리되므로 코드가 깔끔해진다.

try {
    deletePage(page);
    registry.deleteReference(page.name);
    configKeys.deleteKey(page.name.makeKey);
}
catch (Exception e) {
    logger.log(e.getMessage());
}

---

하지만 위 내용은 아래와 같이 변경할 수 있다.

---

public void delete(Page page) {

    try {
        deletePageAndALlReferences(page);
    } catch (Exception e) {
        logErrror(e);
    }
}

private void deletePageAndAllReferences(Page page) throws Exception {
    deletePage(page);
    registry.deleteReference(page.name);
    configKeys.deleteKey(page.name.makeKey());
}

private void logError(Exception e) {
    logger.log(e.getMessage());
}

```

마지막 delete() 함수를 보면 추상화 레벨도 유사하여 코드가 잘 읽히고, try catch 문이 있는 delete 함수도 깔끔하게 읽힌다.

함수의 추상화 수준을 잘 보고, try catch 문을 따로 함수로 분리하는 내용, 에러 로그를 따로 처리하는 내용을 잘 살펴보자.

물론 `logger.log(e.getMessage());` 부분은 하나밖에 없는데 굳이 함수로 분리해야 하나 ? 라고 생각할 수 있지만 추상화 수준이
다르므로 분리했다고 생각한다.

<br>

```
결론
```

프로그래머는 이야기를 작성하는 사람이다. 이야기는 독자로 하여금 편하고 잘 읽힐 수 있도록 작성해야하는 의무가 있다.
그러기 위해서 함수를 잘게 잘 나누고 추상화 수준을 비슷하게 갖추며 이름을 서술적으로 잘 지어보자.


# 4장 주석

<br>

# 9장 단위 테스트

```
TDD 법칙 세가지

첫째 법칙 : 실패하는 단위 테스트를 작성할 때까지 실제 코드를 작성하지 않는다.
둘째 법칙 : 컴파일은 실패하지 않으면서 실행이 실패하는 정도로만 단위 테스트를 작성한다.
셋째 법칙 : 현재 실패하는 테스트를 통과할 정도로만 실제 코드를 작성한다.
```


```
깨끗한 테스트 코드 유지하기

'지저분해도 빨리' 가 주제어였다. 이후 테스트코드는 잘 설계하거나 주의해서 분리할 
필요가 없었다. 그저 돌아가면 되었다.

... 중략

실제 코드를 변경해 기존 테스트 케이스가 실패하기 시작하면, 지저분한 코드로 인해, 
실패하는 테스트 케이스를 추가하는 시간이 더 걸린다.
테스트 케이스를 유지하고 보수하는 비용도 늘어단다.

...

테스트 코드는 실제 코드 못지 않게 중요하다.
```

```
테스트 이스가 없다면 모든 변경이 잠정적인 버그다. 아키텍처가 아무리 유연하더라도, 
설계를 아무리 잘 나누었더라도, 테스트 케이스가 없으면
개발자는 변경을 주저한다. 버그가 숨어들까 두렵기 때문이다.
```

```
테스트 당 assert 하나

assert 문이 단 하나인 함수는 결론이 하나라서 코드를 이해하기 쉽고 빠르다.

하지만 하나로 하기 위해 테스트를 분리하다 보면 중복되는 코드들이 많아진다. 
그러면 @Before 을 사용하면 되지 않나 ? 이렇게 하다보면 배보다 배꼽이 더 커진다.
assert를 여러개로 사용하는 편이 나을 수 도 있다.
```

위와 같이 assert를 여러개로 나누어서 사용해야할 경우 private 메서드로 빼는 것도 좋은 선택이 될 수 있다.

결국 위에서 설명하고자 하는 개념은 함수, 메서드의 목적이 명확해야하며 그 수가 적을 수록 좋다는 것이다.

```
테스트 당 개념 하나.

규칙은

개념 당 assert문 수를 최소로 줄여라.
테스트 함수 하나는 개념 하나만 테스트 하라.
```

```
FIRST

Fast
Independent
Repeatable
Self-Validating
Timely
```


# 10장 클래스

```
클래스 체계

변수는 아래와 같이 나열된다.
static + public 이 가장 먼저, 그 다음으로는 static + private
그 다음은 private이 나오게 된다.

변수목록 다음으로는 함수가 나오게 된다.

private 함수는 자신을 호출하는 public 함수 바로 아래 넣는다. 즉 추상화 단계가
순차적으로 내려간다. 그래서 코드는 신문 기사처럼 읽힌다.
```

```
클래스는 작아야 한다

클래스를 만들 때 첫 번째 규칙은 크기다. 클래스는 작아야 한다. 두 번째
규칙도 크기다. 더 작아야 한다.

다만 함수와는 다르게 물리적인 행 수로 크기를 측정하는 것은 아니다.

클래스는 클래스가 맡은 책임을 센다.
```



```java
public class SuperDashboard extends JFrame implements MetaDataUser {
    public Component getLastFocusedComponent();
    public void setLastFocused(Component lastFocused);
    public int getMajorVersionNumber();
    ...
    
}


```

```
단일 책임 원칙

단일 책임 원칙 Single Responsibility Principle SRP 는 클래스나
모듈을 변경할 이유가 하나, 단 하나뿐이어야 한다는 원칙이다.
```

```
규모가 어느 수준에 이르는 시스템은 논리가 많고도 복잡하다. 이런 
복잡성을 다루려면 체계적인 정리가 필수다. 그래야 개발자가 무엇이 
어디에 있는지 쉽게 찾는다.

큼직한 다목적 클래스 몇 개로 이루어진 시슽메은 변경 시 당장 알 필요가
없는 사실까지 들이밀어 독자를 방해한다.



```

