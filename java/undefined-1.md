# 객체 지향 프로그래밍

#### <mark style="background-color:orange;">객체 지향과 비용</mark>

* 캡슐화 + 다형성(추상화) -> 비용을 낮추는 데 유리



### <mark style="background-color:blue;">객체</mark>&#x20;

#### <mark style="background-color:orange;">객체 지향</mark>

* 객체에 데이터와 프로시저를 캡슐화함
* 객체는 프로시저를 이용해서 서로 연결



#### <mark style="background-color:orange;">객체란?</mark>

* &#x20;객체의 핵심 -> <mark style="color:red;">**기능 제공**</mark>&#x20;
* 객체는 제공하는 기능으로 정의 내부적으로 가진 필드(데이터)로 정의하지 않음
* ex) 회원 객체 암호 변경하기 기능 차단 여부 확인 하기 기능
* ex) 소리 제어기 소리 크기 증가하기 기능 소리 크기 감소하기 기능



#### <mark style="background-color:orange;">기능 명세</mark>

* 메서드(오퍼레이션)를 이용해서 기능 명세 이름, 파라미터, 결과로 구성



#### <mark style="background-color:orange;">객체와 객체</mark>&#x20;

* 객체와 객체는 기능을 사용해서 연결&#x20;
* 기능 사용 = 메서드 호출&#x20;

```
VolumnController volCont = new VolumnController();
volCont.increase(4);
volCont.decrease(3);
int currentVol = volCont.volume();
```



#### <mark style="background-color:orange;">용어 : 메시지</mark>&#x20;

* 객체와 객체 상호 작용 : 메시지를 주고 받는다고 표현&#x20;
* 메서드를 호하는 메시지, 리턴하는 메시지, 익셉션 메시지



### <mark style="background-color:blue;">캡슐화(Encapsulation)</mark>

* 데이터 + 관련 기능 묶기
* 객체가 기능을 어떻게 구현했는지 외부 감추는 것
* 구현에 사용된 데이터의 상세 내용을 외부에 감춤
* 정보 은닉(Information Hiding) 의미 포함
* 외부에 영향 없이 객체 내부 구현 변경 가능
* 연쇄적인 변경 전파를 최소화
* 캡슐화된 기능을 사용하는 코드 영향 최소화



#### <mark style="background-color:orange;">캡슐화와 기능</mark>

* 캡슐화 시도 -> 기능에 대한 (의도) 이해를 높임



#### <mark style="background-color:orange;">캡슐화를 위한 2가지 규칙</mark>

* Tell, Don't Ask
  * 데이터를 달라 하지 말고 해달라고 하기
* Demeter's Law
  * 메서드에서 생성한 객체의 메서드만 호출
  * 파라미터로 받은 객체의 메서드만 호출
  * 필드로 참조하는 객체의 메서드만 호출



#### <mark style="background-color:orange;">캡슐화 정리</mark>

* 캡슐화 : 기능의 구현을 외부에 감춤
* 캡슐화를 통해 기능을 사용하는 코드에 영향을 주지 않고 (또는 최소화) 내부 구현을 변경할 수 있는 유연함
* 수정에 있어 비용을 최소화



### <mark style="background-color:blue;">다형성(Polymorphism)</mark>

* 여러(poly) 모습(morph)을 갖는 것
* 객체 지향에서는 한 객체가 여러 타입을 갖는 것
  * 즉, 한 객체가 여러 타입의 기능을 제공
  * 타입 상속으로 다형성 구현
    * 하위 타입은 상위 타입도 됨



### <mark style="background-color:blue;">추상화(Abstraction)</mark>

* 데이터나 프로세스 등을 의미가 비슷한 개념이나 의미 있는 표현으로 정의하는 과정
* 두 가지 방식의 추상화
  * 특정한 성질, 공통 성질(일반화)
* 간단한 예
  * DB의 USER 테이블 : 아이디, 이름, 이메일
  * Money 클래스 : 통화, 금액
  * 프린터 : HP MXXX, 삼성 SL-M2XXX
  * GPU : 지포스, 라데온
* 추상 타입 사용에 따른 이점 : 유연함
*   추상화 결과 : 사용 대상 변경 유연함



#### <mark style="background-color:orange;">타입 추상화</mark>

* 여러 구현 클래스를 대표하는 상위 타입 도출
* 흔히 인터페이스 타입으로 추상화
* 추상화 타입과 구현은 타입 상속으로 연결



#### <mark style="background-color:orange;">추상 타입 사용</mark>

* 추상 타입을 이용한 프로그래밍
* 추상 타입은 구현을 감춤
  * 기능의 구현이 아닌 의도를 더 잘 드러냄



#### <mark style="background-color:orange;">추상화는 의존 대상이 변경하는 시점에</mark>

* 추상화 -> 추상 타입 증가 -> 복잡도 증가
  * 아직 존재하지 않는 기능에 대한 이른 추상화는 주의
    * 잘못된 추상화 가능성, 복잡도만 증가
  * 실제 변경 및 확장이 발생할 때 추상화 시도



### <mark style="background-color:blue;">상속 보다는 조립</mark>

#### <mark style="background-color:orange;">상속과 재사용</mark>

* 상위 클래스의 기능을 재사용, 확장하는 방법으로 활용



#### <mark style="background-color:orange;">상속을 통한 기능 재사용 시 발생할 수 있는 단점</mark>

* 상위 클래스 변경 어려움
  * 변경의 여파가 계층도를 따라 전파됨
* 클래스 증가
* 상속 오용



#### <mark style="background-color:orange;">상속의 단점 해결 방법 -> 조립</mark>

* 조립(Composition)
  * 여러 객체를 묶어서 더 복잡한 기능을 제공
  * 보통 필드로 다른 객체를 참조하는 방식으로 조립
  * 또는, 객체를 필요 시점에 생성/구함





### <mark style="background-color:blue;">기능과 책임 분리</mark>

#### <mark style="background-color:orange;">기능 분해</mark>

* 기능은 하위 기능으로 분해 가능



#### <mark style="background-color:orange;">기능을 누가 제공할 것인가?</mark>

* 기능은 곧 책임
* 분리한 각 기능을 알맞게 분배



#### <mark style="background-color:orange;">큰 클래스, 큰 메서드</mark>

* 클래스나 메서드가 커지면 절차 지향의 문제 발생
* 큰 클래스 -> 많은 필드를 많은 메서드가 공유
* 큰 메서드 -> 많은 변수를 많은 코드가 공유
* 여러 기능이 한 클래스/메서드에 섞여 있을 가능성
* 책임에 따라 알맞게 코드 분리 필요



#### <mark style="background-color:orange;">몇 가지 책임 분배/분리 방법</mark>

* 패턴 적용
* 계산 기능 분리
* 외부 연동 분리
* 조건별 분기는 추상화



**패턴 적용**

* 전형적인 역할 분리
* 간단한 웹
* 컨트롤러, 서비스, DAO
* 복잡한 도메인
* 엔티티, 밸류, 리포지토리, 도메인 서비스
* AOP
* Aspect(공통 기능)
* GoF
* 팩토리, 빌더, 전략, 템플릿 메서드, 프록시/데코레이터 등



**연동 분리**

* 네트워크, 메시징, 파일 등 연동 처리 코드 분리



**조건 분기는 추상화**

* 연속적인 if-else는 추상화 고민



#### <mark style="background-color:orange;">역할 분리와 테스트</mark>

* 역할 분리가 잘되면 테스트도 용이해짐



### <mark style="background-color:blue;">의존과 DI</mark>

<mark style="background-color:blue;"></mark>

#### <mark style="background-color:orange;">의존</mark>

* 기능 구현을 위해 다른 구성 요소를 사용하는 것
  * 의존의 예 : 객체 생성, 메서드 호출, 데이터 사용
* 의존은 변경이 전파될 가능성을 의미
  * 의존하는 대상이 바뀌면 바뀔 가능성이 높아짐
    * ex) 호출하는 메서드의 파라미터가 변경
    * ex) 호출하는 메서드가 발생할 수 있는 익셉션 타입이 추가



#### <mark style="background-color:orange;">순환 의존</mark>

* 순환 의존 -> 변경 연쇄 전파 가능성
  * 클래스, 패키지, 모듈 등 모든 수준에서 순환 의존 없도록 해야함함



#### <mark style="background-color:orange;">의존 대상 많을 때1 -> 기능 많은 경우</mark>

* 한 클래스에서 많은 기능을 제공하는 경우(한 클래스에 여러 메서드)
  * 각 기능마다 의존하는 대상이 다를 수 있음
  * 한 기능 변경이 다른 기능에 영향을 줄 수 있음
* 기능 별로 분리 고려 -> 클래스로 분리 -> 테스트에 용이



#### <mark style="background-color:orange;">의존 대상 많을 때 2 -> 묶어보기</mark>

* 몇 가지 의존 대상을 단일 기능으로 묶어서 생각해보면 의존 대상을 줄일 수 있음



#### <mark style="background-color:orange;">의존 대상 객체를 직접 생성하면?</mark>

* 생성 클래스가 바뀌면 의존하는 코드도 바뀜
  * 추상화에서 언급
* 의존 대상 객체를 직접 생성하지 않는 방법
  * 팩토리, 빌더
  * 의존 주입(Dependency Injection)
  * 서비스 로케이터(Service Locator)



#### <mark style="background-color:orange;">의존 주입(Dependency Injection)</mark>

* 외부에서 의존 객체를 주입
  * 생성자나 메서드를 이용해서 주입



#### <mark style="background-color:orange;">조립기(Assembler)</mark>

* 조립기가 객체 생성, 의존 주입을 처리
  * ex) 스프링 프레임워크



#### <mark style="background-color:orange;">DI 장점</mark>

* 상위 타입을 사용할 경우 의존 대상이 바뀌면 조립기(설정)만 변경하면 됨
* 의존하는 객체 없이 대역 객체를 사용해서 테스트 가능

## 정리



*   소프트웨어의 가치: 변화

    * 적은 비용으로 변화할 수 있는 방법 중 하나 -> 객체 지향


*   객체는 제공하는 기능으로 정의

    * ex) 회원 객체 -> 암호 변경하기 기능


*   메서드를 이용해서 기능 명세

    * 이름, 파라미터, 결과(리턴 타입)로 구성


*   캡슐화 : 내부 구현 감춤

    * 이는 내부 구현 변경에 따른 외부 영향을 최소화
    * 내부 구현 변경의 유연함


*   추상화 : 여러 구현의 공통점을 상위 타입으로 도출


*   상속 보단 조립

    * 상속의 단점을 조립하는 방식으로 해소


*   기능과 책임 분리

    * 4가지 분리 방법
      * 패턴 적용
      * 계산 기능 분리
      * 외부 연동 분리
      * 조건별 분기는 추상화


*   적절히 책임을 분리할수록 테스트 용이


*   의존과 DI

    * DI로 의존 객체 접근
    * 의존 객체 변경이 쉽고 테스트에서 대역 객체 사용 용이


* 개발자는 코드를 변경해야 하는 사람
  * 변경 비용을 낮추기 위한 노력 필요
