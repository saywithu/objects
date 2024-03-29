# 코드로 이해하는 객체지향 설계 스터디

## 7. 객체분해

1. 추상화 매커니즘
    1. 프로시저 추상화
        - 기능분해(알고리즘 분해)
    2. 데이터 추상화
        - 타입 추상화 : 추상 데이터 타입
        - 프로시저 추상화 : 객체지향

2. 프로시저 추상화와 기능분해
    1. 하향식 기능 분해 방식
        - 최상위의 추상적인 함수 정의에서 출발해서 단계적인 정체 절차를 따라 시스템을 구축한다.
        - 메인 함수를 루트로 하는 트리로 표현할 수 있다.
      
      ```
      예)
      직원의 급여를 계산한다.
        사용자로부터 소득세율을 입력받는다.
          "세율을 입력하세요: "라는 문장을 화면에 출력한다.
          키보드를 통해 세율을 입력받는다.
        직원의 급여를 계산한다.
          전역 변수에 저장된 직원의 기본급 정보를 얻는다.
          급여를 계산한다.
        양식에 맞게 결과를 출력한다.
          "이름: {직원명}, 급여: {계산된 금액}" 형식에 따라 출력 문자열을 생성한다.
      ```
    2. 하향식 기능 분해의 문제점
        * 시스템은 하나의 메인 함수로 구성돼 있지 않다.
        * 기능 추가나 요구사항 변경으로 인해 메인 함수를 빈번하게 수정해야 한다.
        * 비즈니스 로직이 사용자 인터페이스와 강하게 결합된다.<br>
          *비즈니스 로직을 설계하는 초기 단계부터 입력 방법과 출력 양식을 함께 고민하도록 강요한다.*
        * 하향식 분해는 너무 이른 시기에 함수들의 실행 순서를 고정시키기 때문에 유연성과 재사용성이 저하된다.<br>
          *설계를 시작하는 시점부터 시스템이 무엇을 해야 하는지가 아니라 어떻게 동작해야 하는지에 집중하도록 만든다.*
        * 데이터 형식이 변경될 경우 파급효과를 예측할 수 없다.

    3. 하향식 분해가 유용한 경우
        + **설계가 어느 정도 안정화 된 후에는 설계의 다양한 측면을 논리적으로 설명하고 문서화하기에 용이**

3. 모듈
    1. 장점
        + 모듈 내부의 변수가 변경되더라도 모듈 내부에만 영향을 미친다.
        + 비즈니스 로직과 사용자 인터페이스에 대한 관심사를 분리한다.
        + 전역 변수와 전역 함수를 제거함으로써 네임스페이스 오염을 방지한다.
    2. 단점
        + 인스턴스의 개념을 제공하지 않는다.
        
4. 데이터 추상화와 추상 데이터 타입<br>
    - 리스코프 치환 원칙(LSP)<br>
    *상속관계에 있는 두 객체에 있어서 부모 클래스의 인스턴스가 사용된 자리에 자식 클래스의 인스턴스를 집어 넣어도 코드의 맥락이 변하지 않아야 한다.*
```
이해를 돕기위해 도형을 예시를 들어보자. 도형 클래스와 사각형 클래스가 있고, 사각형 클래스는 도형 클래스의 상속을 받는다고 가정하자.
(1) 도형은 둘레를 가지고 있다.
(2) 도형은 넓이를 가지고 있다.
(3) 도형은 각을 가지고 있다.
일반화 관계(일관성인지 확인하는 방법은 단어를 교체해 보면 알 수 있다.  (1) ~ (3)의 도형이란 단어 대신 사각형을 넣어보자.
(1) 사각형은 둘레를 가지고 있다.
(2) 사각형은 넓이를 가지고 있다.
(3) 사각형은 각을 가지고 있다.
(1) ~ (3) 모두 딱히 이상한 부분이 보이지 않는다. 따라서 도형과 사각형 사이에는 일관성이 있다고 할 수 있다.
여기서 원(Circle) 이라는 도형에 대해 생각해보자. 원 클래스 역시 도형 클래스의 상속을 받는다고 가정하자. 앞에서 언급한 (1) ~ (3)의 도형 단어 대신 원을 대입해보자.
(1) 원은 둘레를 가지고 있다.
(2) 원은 넓이를 가지고 있다.
(3) 원은 각을 가지고 있다.
문장을 읽어보면 (3)번 문장이 어색하다는 것을 알 수 있다. 따라서 도형 클래스는 LSP을 만족하지 않은 설계라 할 수 있다. 따라서 (3)문장에 대해서는 일반화 관계가 성립하도록 수정되어야 한다.
```

5. 클래스
    1. 클래스는 추상 데이터 타입인가?<br>
        - 클래스와 추상 데이터 타입 모두 데이터 추상화를 기반으로 시스템을 분해하기 때문에 꼭 틀린 것만은 아니다.
        - 클래스는 상속과 다형성을 지원하는 데 비해 추상 데이터 타입은 지원하지 못한다.
        - 추상 데이터 타입은 타입을 추상화 한 것
        - 클래스는 절차를 추상화 한 것

## 8. 의존성 관리하기
1. 런타임 의존성과 컴파일타임 의존성
    - 런타임 의존성 : 애플리케이션 실행 시점에 생기는 의존성
    - 컴파일 타임 의존성 : 컴파일 언어 - 컴파일 시점, 스크립트 언어 - 코드 작성시
2. 의존성 해결하기
    - 객체를 생성하는 시점에 생성자를 통해 의존성 해결
    - 객체 생성 후 Setter 메서드를 통해 의존성 해결
    - 메서드 실행 시 인자를 이용해 의존성 해결

예상되는 실제 개발 소스
``` java
public class Movie {
    private String title;
    private Duration runningTime;
    private Money fee;
    private DiscountPolicy discountPolicy;

    public Movie(String title, Duration runningTime, Money fee, DiscountPolicy discountPolicy) {
        this.title = title;
        this.runningTime = runningTime;
        this.fee = fee;
        this.discountPolicy = discountPolicy;
    }

    public Money getFee() {
        return fee;
    }

    public Money calculateMovieFee(Screening screening) {
        return fee.minus(discountPolicy.calculateDiscountAmount(screening));
    }
    
    public Money getDiscountAmount(Screening Screening){
        DiscountType discountType = movieService.getDiscountType(movieId);
        if(discountType == DiscountType.AMOUNT){
          ...
          return fee;
        } else if (discountType == DiscountType.PERCENT) {
          ...
          return fee;       
        } else {
          ...
          return fee;        
        }
    }
}
```
책 원본 소스

``` java
public class Movie {
    private String title;
    private Duration runningTime;
    private Money fee;
    private DiscountPolicy discountPolicy;

    public Movie(String title, Duration runningTime, Money fee, DiscountPolicy discountPolicy) {
        this.title = title;
        this.runningTime = runningTime;
        this.fee = fee;
        this.discountPolicy = discountPolicy;
    }

    public Money getFee() {
        return fee;
    }

    public Money calculateMovieFee(Screening screening) {
        return fee.minus(discountPolicy.calculateDiscountAmount(screening));
    }
}
```
``` java
public abstract class DiscountPolicy {
    private List<DiscountCondition> conditions = new ArrayList<>();

    public DiscountPolicy(DiscountCondition ... conditions) {
        this.conditions = Arrays.asList(conditions);
    }

    public Money calculateDiscountAmount(Screening screening) {
        for(DiscountCondition each : conditions) {
            if (each.isSatisfiedBy(screening)) {
                return getDiscountAmount(screening);
            }
        }

        return Money.ZERO;
    }

    abstract protected Money getDiscountAmount(Screening Screening);
}
```

## 9. 유연한 설계
1. 개방-폐쇄 원칙(OCP)
    - 확장에 대해 열려있고 수정에 닫혀 있어야 한다.
    - 컴파일 타임 의존성을 고정시키고 런타임 의존성을 변경하라.
    - OCP의 핵심은 추상화에 의존하는 것이다.
2. 생성 사용 분리
    - 같은 구체 클래스에서 인스턴스를 생성해서는 안 된다.
    - 팩토리 메서드 패턴을 이용해서 생성을 책임진다.
3. 의존성 주입
    - 생성자 주입
    - Setter 주입
    - 메서드 주입
4. 추상화와 의존성 역전
    - 수준의모듈은 하위수준의모듈에 의존해서는 안된다. 둘 모두 추상화에 의존해야 한다.
    - 추상화는 구체적인 사항에 의존해서는 안된다. 구체적인 사항은 추상화에 의존해야 한다.
5. 유연성에 대한 조언
    - 변경하기 쉽고 확장하기 쉬운 구조를 만들기 위해서는 단순함과 명확암의 미덕을 버리게 될 가능성이 높다.
    - 유연한 설계라는 말의 이면에는 복잡한 설계라는 의미가 숨어 있다.
    - 유연함은 단순성과 명확성의 희생 위에서 자라난다.
