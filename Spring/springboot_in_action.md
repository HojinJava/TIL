## Keyword
`in Action` `spring boot`

## 상황
- 'TDD,리팩토링,클린코드' 자바지기 강의를 들으면서, ATDD 실습프로젝트에서 스프링부트가 나옴. JPA,spring boot, mock 모두 너무 낯설어서 자바지기에세 공부 우선순위를 물어봤는데 spring을 현업에서 사용하고 있으면 springboot 먼저 공부해보면 어떻겠냐는 답변을 들었다. 고른 책은 '스프링부트 코딩공작소(길벗)'으로 2016년 도서로 원제를 보니 in action 시리즈 중에 하나다. 스프링부트 2.0이 나온 시점에서 최신판을 다룬 책을 볼까 했는데 개념을 이해하기에는 이 책이 더 나을 꺼라는 판단이 들었다. 
스프링부트 튜토리얼이 잘 되어있기때문에 튜토리얼과 함께 좀 더 개념적인 부분을 익혀서 써보려고 한다. 
  - 좋은 원서로 볼까 했는데, 영어,개념 두가지에 동시에 신경쓰는 것보다 처음 개념을 잡을때는 익숙한 말로 배우는게 낫다는 생각이 들었다. 영어를 원어민 수준으로 하는게 아니라면 새로운 걸 배우는 시점에서 먼저 한글로 된 책으로 빠르게 개념에 익숙해지는게 낫지 않을까? 

## 배운 것 정리 
### 1장. 스프링부트 소개
- 한 줄 요약: 스프링부트는 구성 및 설정작업을 간단하게 할 수 있어서 개발자가 비즈니스 로직에 집중하게 도와준다.
- 비즈니스 로직에 집중하게 해준다. 복잡한 설정과 반복되는 설정은 스프링부트가 처리한다.
    + 스프링으로 웹 어플리케이션 개발시에 항상 해주어야하는 구성 작업은 개발자가 아닌 스프링부트가 한다! 
    + 두 가지 저항을 줄임 : 애플리케이션 로직 작성 외에 구성작업에 쓰이는 시간, 의존성 관리(의존 라이브러리 추가 등)
- 크게 네가지 특성이 있음 : 자동구성, 스타터 의존성, 명령줄인터페이스(cli), 액추에이터
  + 04/26까지 이해한 것 
  - 액추에이터: 작동 중인 애플리케이션의 내부를 살펴볼 수 있는 기능 제공! / 7장에서 더 
  - 스타터 의존성 : 어떤 기능(예. JPA, security)를 사용하려면, 그에 맞는 라이브러리를 직접 추가할 필요없이 그저 스타터 의존성을 사용해서 해당기능을 끌어오면 된다.(스타터가 이미 라이브러리 호환성까지 체크해두어 버전을 고민할 필요도 없음)
  - 자동구성 - 어떻게 클래스패스 참고해서 자동구성하는지? [추가]-이해가 더 필요함
    >  예를 들어 스프링 부트가 애플리케이션 클래스패스에서 H2 데이터베이스 라이브러리를 발견한다면 내장 H2 데이터베이스를 자동으로 구성할 것이다. JdbcTemplate이 클래스패스에 있다면 JdbcTemplate빈도 구성할 것 이다. 이런 빈을 구성하는 작업은 하지 않아도 되는데 스프링 부트가 빈을 자동으로 구성하여 여러분이 작성한 빈에 주입(Inject)할 준비를 해준다.
  - springboot cli
    > 스프링 부트 CLI는 개발자가 코드 작성에만 집중할 수 있도록 스타터 의존성과 자동 구성을 활용한다.
    > 스프링 부트 CLI가 어떤 타입을 사용했는지 발견하여 이 타입이 작동할 수 있게 클래스패스에 알맞은. 스타터 의존성을 추가하기 때문이다. 이 의존성이 클래스패스에 있으면 일련의 자동 구성이 일어나서. HTTP 요청에 컨트롤러가 응답할 수 있도록 DispatcherServlet과 스프링 MVC를 활성화한다.
    - 이걸 사용하면 코드 컴파일할 필요조차 없음
- 스프링부트의 오해
    - 스프링부트는 애플리케이션 서버가 아님
      - commandline으로 실행할 수 있는 jar파일로 웹 애플리케이션을 개발할 수 있어서 그렇게 보임.
      - 스프링 부트는 톰켓과 같은 서블릿 컨테이너를 포함하고 있기 때문에 jar로 실행되는 것뿐임.
      - 내장 서블릿 컨테이너가 애플리케이션 서버기능을 실행하는 것일뿐 스프링부트 자체가 제공하는 것은 아님.
    - JPA나 JMS 같은 엔터프라이즈 자바 명세를 구현하지 않음.
      > 스프링 부트가 엔터프라이즈 기능을 지원하는 빈들을 자동으로 스프링에 구성하기 때문에 엔터프라이즈 자바 명세를 몇 가지 지원하기는 한다. 예를 들어 스프링 부트는 JPA를 구현하지 않지만 하이버네이트(Hibernate) 같은 JPA 구현체에 대응하는 빈을 알맞게 자동 구성하여 JPA를 지원한다. 
    - 스프링 부트는 자동 구성을 하려고 어떤 형태의 코드도 생성하지 않는다.
      > spring 4.0의 조건부 구성기능이나 maven, gradle 의 의존성해결기능을 활용해서 애플리케이션 컨텍스트에 자동으로 빈을 구성하는 것임

### 7장. 스프링부트 테스트하기
- 한 줄 요약: 
- 테스트의 의미
    + 애플리케이션이 예상대로 동작하는지 확인하는 것
        > 테스트가 실패한다면 더 해야할 일이 남은 것이다. 테스트를 통과한다면 목표에 잘 도달한 것이다. 적어도 작성할 수 있는 테스트가 더 있다는 것을 알기 전까지는 말이다.
    + 애플리케이션을 계속해서 발전시키는 과정에서 오류 발생을 잡아낼 수 있는 안전장치이다.
    + [내가 추가] 잘 작성된 테스트케이스는 해당 애플리케이션 기능에 대한 이해를 돕는다. 오픈소스 분석에서 테스트케이스를 보면서 감을 잡듯이. 
- 스프링에서의 테스트
    + 스프링 특성인 느슨한 결합, 인터페이스 기반 설계, POJO 사용으로 unit test가 용이함
    + 통합테스트를 위해서는 각 컴포넌트를 구성하고 연결하기 위해 (실제 애플리케이션에 스프링을 사용하듯이) 스프링의 설정과 구성을 사용해야함
        * [내가 추가] 처음 스프링 프로젝트에 테스트를 작성할때, 메소드 단위의 유닛테스트를 하다가 다른 컴포넌트를 불러와서 테스트를 할때 계속 에러가 나서 당황한 적이 있다. 그 떄를 잊지 말자...
    > **스프링 프레임워크가 수행하는 가장 핵심적인 작업은 애플리케이션을 구성하는 컴포넌트를 모두 연결하는 것이다.**
    > 스프링은 컴포넌트 검색과 자동 연결(Auto wired) 등 부가적인 기능과 캐싱, 트랜잭션, 보안 등 선언적인 기능을 제공한다. 스프링이 하는 모든 일을 감안하면 복잡한 일은 (통합 테스트에서조차도) 스프링에 맡기는 것이 가장 좋다.
    - 스프링 애플리케이션을 통합테스트할때는 출시환경에서 실행할 때와 동일한 방식으로 테스트 대상 빈을 연결하는 것이 가장 중요하다.
        + [SLiPP의 테스트기반 스터디(2018/04/04 6주차)](https://www.slipp.net/wiki/pages/viewpage.action?pageId=30769385)에서 [작성한 코드](https://github.com/slippStudy/slipp_tbd_todo/pull/18)를 스프링 context를 불러올떄 테스트환경에서만 동작하도록 config를 설정한 부분을 고치도록 [코드리뷰](https://github.com/slippStudy/slipp_tbd_todo/pull/18/commits/598a45b440ed20a012df1cd24f7ea0ccca593be1) 받았었음.
- 통합테스트를 위한 구성
```
    @RunWith(SpringJUnit4ClassRunner.class)
@SpringApplicationConfiguration(classes = ReadingListApplication.class)
public class AddressServiceTest {
    @Autowired
    private AddressService addressService;
    //...
}
    ```

    + 스프링에서는 application context를 가져오기 위해 `@ContextConfigutation`사용하지만, 
    스프링부트의 기능을 사용하기 위해 `@SpringApplicationConfiguration`사용 
    + `@Autowired`하여 애플리케이션 컨텍스트에서 테스트로 빈을 주입함. 테스트대상인 빈을 테스트에 autowired(자동연결)함

- [ ] 이하 내용 정리 중
- Mock이란? 
    + controller 처럼 동작하도록 해줌
- 웹 어플리케이션 테스트가 POJO 메소드와 다른 이유
    + 두가지 방법 
    + 1. 스프링 MVC mock사용
    + 2. 웹 서블릿 엔진 사용한 테스트
- 두번째 코드 분석 
  - 추가 태그 알기 : autowiring / controller
  - DI 좀 이해해보자 나도 쫌!
  - repository 가 뭔거지...
- 정적임포트 사용해서 코드 간결하게 만들기 - static하지 않으면 사용할 수 없음. static해서 메모리에 올리는게 비효율적으로 자원관리하는 것인가?



## 해보기 
- springboot cli 설치 : [참고 - 공식문서 10. Installing Spring Boot](https://docs.spring.io/spring-boot/docs/current/reference/html/getting-started-installing-spring-boot.html)
  - 먼저 `brew tap pivotal/tap` 해야함. 해당 리포지토리(pivotal/tap)를 가져와서 관련 fomulae가 있는 tab을 가져와야함. `brew install springboot`
      + 정말 생맥주 tab따듯이 tap 이라는 명령어를 쓰는구나! 재미지다.
