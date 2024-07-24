객체지향 설계란 올바른 객체에게 올바른 책임을 할당하면서 낮은 결합도와 높은 응집도를 가진 구조를 창조하는 활동이다.

→ 해당 정의에 속한 두가지 관점

1) 객체지향 설계의 핵심은 책임이다.

2) 책임을 할당하는 작업은 응집도와 결합도 같은 설계 품질과 깊이 연관되어 있다.

설계는 변경을 위해 존재하고 변경에는 어떤식으로든 비용이 발생한다.

훌륭한 설계란 합리적인 비용안에서 변경을 수용할 수 있는 구조를 만드는 것이다.

결합도와 응집도를 합리적인 수준으로 유지할 수 있는 중요한 원칙

→ 객체의 상태가 아닌 객체의 행동에 초점을 맞추는 것.

### 01 데이터 중심의 영화 예매 시스템

객체의 상태 = 객체가 저장해야하는 데이터

훌륭한 객체지향 설계는 객체의 상태가 아닌 책임에 초점을 맞춰야한다.

이유는 객체의 상태는 구현에 해당된다. 구현은 불안정하기 때문에 변하기 쉽다. 따라서 변경에 취약하다.

### 02 설계 트레이드오프

여기서부터는  **데이터 중심 설계**와 **책임 중심 설계**의 장단점을 비교하기 위해 **캡슐화, 응집도, 결합도**를 사용하겠다.

- 캡슐화 - 외부에서 알 필요가 없는 부분을 감춤으로써 대상을 단순화하는 추상화의 한 종류, 변경 가능성이 높은 부분을 객체 내부로 숨기는 추상화 기법.
- 응집도 - 모듈에 포함된 내부 요소들이 연관돼 있는 정도
- 결합도 - 의존성 정도를 나타내며 다른 모듈에 대해 얼마나 많은 지식을 갖고 있는지 나타내는 척도

일반적으로 좋은 설계란 높은 응집도와 낮은 결합도를 가진 모듈로 구성된 설계이다.

변경 관점에서 응집도란 변경이 발생할 때 모듈 내부에서 발생하는 변경의 정도이다.

변경 관점에서 결합도는 한 모듈이 변경되기 위해 다른 모듈의 변경 정도이다.

캡슐화를 지키면 응집도는 높고 결합도는 낮아진다. 따라서 응집도 결합도를 고려하기 전에 캡슐화를 향상시키기 위해 노력하라.

### 03 데이터 중심의 영화 예매 시스템의 문제점

기능적인 측면에서는 데이터 중심의 설계와 동일하다.

데이터 중심 영화 예매 시스템의 문제점

- 캡슐화 위반
- 높은 결합도
- 낮은 응집도

**캡슐화 위반**

Movie는 getFee(), setFee()는 Money 타입의 fee라는 변수가 존재한다는 것을 퍼블릭 인터페이스로 나타내고 있다.

- 캡슐화를 어기게 된 근본적인 원인은 객체가 수행할 책임이 아니라 저장할 내부 데이터에 초점을 맞췄기 때문이다.
- 앨런 홀럽은 과도하게 접근자와 제어자에 의존하는 설계 방식을 **추측에 의한 설계**라고 부른다.

**높은 결합도**

ReservationAgency의 reserve()를 보면 한 명의 요금을 계산하기 위해 Movie의 getFee()를 호출하여 사용하고 있다. 이는 Money타입이 아닌 다른 타입으로 변경되었을 때 ReservationAgency 코드도 수정되어야한다.

- 이처럼 데이터 중심 설계는 캡슐화를 약화시키기 때문에 클라이언트가 객체의 구현에 강하게 결합된다.

또 다른 단점은 하나의 제어 객체가 다수의 객체에 강하게 결합된다는 것이다.

데이터 중심의 설계는 전체 시스템을 하나의 거대한 의존성 덩어리로 만들기 때문에 어떤 변경이라도 일단 발생하고 나면 시스템 전체가 요동칠 수 밖에 없다.

**낮은 응집도**

아래 수정사항이 발생한다면 ReservationAgency를 수정해야할 것이다.

- 할인 정책이 추가될 경우
- 할인 정책별로 할인 요금을 계산하는 방법이 변경될 경우
- 할인 조건이 추가되는 경우
- 할인 조건별로 할인 여부를 판단하는 방법이 변경될 경우
- 예매 요금을 계산하는 방법이 변경될 경우

어떤 요구사항 변경을 수용하기 위해 하나 이상의 클래스를 수정해야 하는 것은 설계의 응집도가 낮다는 증거다.

**단일 책임의 원칙(Single Responsibility Principle, SRP)**

> 로버트 마틴은 모듈의 응집도가 변경과 연관이 있다는 사실을 강조하기 위해 단일 책임의 원칙이라는 설계 원칙을 제시했다. 요약하자면 클래스는 단 한 가지의 변경 이유만 가져야 한다는 것이다.
>

### 04 자율적인 객체를 향해

캡슐화는 설계의 제 1원리다.

Ractangle 예시(118P)의 문제점

- 코드 중복
- 변경에 취약함

→ 해결 방법은 캡슐화이다. 내부에 너비와 높이를 조절하는 로직을 캡슐화하면 두 가지 문제를 해결할 수 있다.

책임을 Ractangle 내부로 이동시키는 것 → 객체 자기 스스로를 책임진다.

우리가 상태와 행동을 하나의 객체에 묶는 이유는 객체 스스로 자신의 상태를 처리하게 하기 위함이다. 단순히 데이터를 제공하기 위함이 아니다.

객체를 설계할 때 “이 객체가 어떤 데이터를 포함해야 하는가?”라는 질문은 아래 두 개의 개별 질문으로 분리해야한다.

- 이 객체가 어떤 데이터를 포함해야 하는가?
  → DiscountCondition이 관리해야하는 데이터
- 이 객체가 어떤 데이터에 대해 수행해야 하는 오퍼레이션은 무엇인가?

  → isDiscountable 메서드 안에서 type의 값을 이용해 현재의 할인 조건에 맞는 적절한 메서드가 호출되었는지 판단한다.


두 번째 설계에서는 데이터를 처리하는 데 필요한 메서드를 데이터를 가지고 있는 객체 스스로 구현하고 있다. 따라서 이 객체들은 스스로를 책임진다고 말할 수 있다.

### 05 하지만 여전히 부족하다

첫번째 설계보다는 나아졌지만 아직도 첫번째 설계에서 발생하던 문제들이 여전히 발생한다.

**캡슐화 위반**

수정된 객체들은 자기 자신의 데이터를 스스로 처리한다. 예를 들어 DiscountCondition은 자신이 스스로 할인 여부를 판단한다.

하지만 기간 조건을 판단하는 메서드(isDiscountable)에서는 DayOfWeek라는 요일 정보와 시간 정보을 파라미터로 받고 있다. 이는 외부에 해당 변수 타입을 활용한다는 것을 노출하는 것이다.

Movie 또한 금액 할인 정책, 비율 할인 정책, 할인 미적용의 경우 호출 할 수 있는 세 가지 메서드를 구현하고 있다.

**캡슐화의 진정한 의미**

> 내부 속성을 외부로부터 감추는 것, 변할 수 있는 어떤 것이든 감추는 것
>

**높은 결합도**

DiscountCondition 내부 구현이 외부로 노출되었기 때문에 결합도는 높을 수 밖에 없다.

DiscountCondition에 대한 어떤 변경은 아래 영향이 생길 수 있다.

- DiscountCondition의 기간 할인 조건의 명칭이 period에서 다른 값으로 변경될 시 Movie를 수정해야한다.
- …(129P 참조 바람..)

인터페이스가 아닌 구현을 변경하는 경우에도 수정이 필요하다는 것은 결합도가 높다는 의미

이 모든 것은 캡슐화를 지키지 않아서 발생하는 문제이다. 캡슐화가 가장 중요하다.

**낮은 응집도**

하나의 변경을 수용하기 위해 코드의 여러곳이 수정되어야한다는 것은 응집도가 낮다는 것.

### 06 데이터 중심 설계의 문제점

**데이터 중심 설계가 취약한 이유**

- 데이터 중심의 설계는 본질적으로 너무 이른 시기에 데이터에 관해 결정하도록 강요한다.
- 데이터 중심의 설계에서는 협력이라는 문맥을 고려하지 않고 객체를 고립시킨 채 오퍼레이션을 결정한다.

데이터 중심 설계는 객체의 행동보다는 상태에 초점을 맞춘다.

너무 이른 시기에 데이터에 대해서 고민하기 때문에 캡슐화에 실패한다.

데이터 중심 설계는 객체를 고립시킨 채 오퍼레이션을 정의하도록 만든다.

중요한 것은 객체가 다른 객체와 협력하는 방법이다.