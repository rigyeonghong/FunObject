# 6. 메시지와 인터페이스

애플리케이션은 '클래스의 집합'으로 구동되는 걸까? -> 아니다. 클래스보다 객체들이 주고받는 메시지가 중요.

## 협력과 메시지

* 클라이언트-서버 모델 : 클라이언트가 메시지를 전송하면 서버가 받는다.
* 메서드 : 메시지를 수신 시 실제 실행되는 함수 또는 프로시저
* 퍼블릭 인터페이스 : 객체가 의사 소통을 위해 외부에 공개하는 메시지의 집합
* 오퍼레이션: 퍼블릭 인터페이스에 포함된 메시지

## 인터페이스의 설계 품질

* 디미터 법칙: 도트(.)를 이용해 메시지 전송을 표현하는 언어에서 오직 하나의 도트만 사용하라. 이를 통해 과도한 객체 구조의 결합을 방지한다.
* TDA(Tell, Don't Ask) : 객체에 메시지를 보내라는 말과 일맥상통
* 인터페이스에 의도를 드러내라

## 원칙의 함정

* 디미터 법칙은 반드시 하나의 도트를 강재하는 것은 아니다. 객체의 내부 구조를 외부로 노출시키는 것을 막는 게 주요 목적임을 상기하자.
* 가끔씩은 TDA를 포기하고 응집도를 높여야 더 효율적이다 (위임 메서드)

## 명령-쿼리 분리 원칙

* 명령: 객체의 상태를 변경, 반환값이 없음
* 쿼리: 객체의 정보를 반환, 상태 변경 불가

이 둘을 분리함으로써 객체의 캡슐화를 지키는 데 도움이 된다.