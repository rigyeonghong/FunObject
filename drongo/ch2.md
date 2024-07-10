# 2. 객체지향 프로그래밍

## 이번 장의 예제: 온라인 영화 예매 시스템

* 할인 조건 - 가격의 할인 여부를 결정하며 순서 조건과 기간 조간으로 나뉨
  * 순서 조건의 경우 매일 n번째 상영 영화, 기간 조건은 기간 내에 상영하는 영화
* 할인 정책 - 얼마나 할인할 것인지
  * 금액 할인 정책 - 정해진 금액만큼 할인
  * 비율 할인 정책 - 정해진 비율만큼 할인

* 영화라는 개념을 Movie 클래스로, 상영이라는 개념을 Screening 클래스로 구분할 수 있다.
* 이외에도 할인 정책을 DiscountPolicy, 금액할인을 AmountDiscountPolicy, 비율할인을 PercentDiscountPolicy, 할인조건을 DiscountCondition 등...
* 클래스 안에 인스턴스 변수, 로직을 구현하고 가시성 (`private`, `public` 등) 을 알맞게 설정한다.
  * 클래스의 내부와 외부를 구분하여 경계를 명확하게 하고 객체의 자율성을 보장
* 객체의 자율성이란?
  * 객체는 상태와 행동을 가지고 자율적인 존재로서 활동하여야 한다.
  * 이를 위하여 객체 내 변수에 대한 접근을 통제하여야 한다. 이를 캡슐화라고 한다.
* 협력하는 객체들의 공동체: 프로그램이 작동하려면 객체들끼리 협력하여야 함
* 상속과 다형성
  * 상속을 통하여 DiscountPolicy 밑에 AmountDiscountPolicy, PercentDiscountPolicy를 둘 수 있음
  * 각 클래스는 getDiscountAmount라는 동일한 메서드를 가지고 있으나 작동하는 방식은 다름 
* 추상화와 유연성
  * 추상 클래스를 둠으로써 추후 기능 변경에 열려 있게 설계 가능