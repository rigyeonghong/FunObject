- 클래스 상속 지연바인딩은 구현측면에서 중요
- 객체지향 패러다임의 본질에서 중요한것은 역할,책임,협력
- 객체지향의 본질은 협력하는 객체들의 공동체를 창조하는 것

[협력]

- **협력**: 객체의 기능을 구현하기 위해 수행하는 **상호작용**
- **책임**: 객체가 협력에 참여하기 위해 수행하는 **로직**
- **역할**: 협력안에서 수행하는 **책임이 모여** 객체가 수행하는 역할을 구성
- **메세지전송** : 객체사이의 협력을 위해 사용하는 유일한 **커뮤니케이션 수단** (요청을 전달)
    - 메세지를 수신한 객체는 **메서드를** 실행해 요청에 응답 ( 스스로 처리방법 선택=자율적인존재=자신의 상태를 직접관리하고 스스로의 결정에따라 행동하는 객체< 내부구현 캡슐화를 통해 자율적인객체를 만듬)
- **객체** : 상태와 행동을 함께 캡슐화하는 실행단위
    - 객체의 **행동**을 결정하는것은 객체가 참여하고있는 협력 (협력내에서 객체가 처리할 메세지)
        - 예매를 위한 협력에 참여하고있기 때문에 Movie객체가 상영이아닌 요금계산 등의 행동을함
    - 객체의 **상태**를 결정하는 것은 행동
        - 행동을 수행하는데 필요한 정보에 의해
- 협력은 객체를 설계하는데 필요한 **문맥을** 제공한다
    - 협력이 행동과 상태를 결정하기 떄문

[책임]

- **책임**: 객체가 협력에 참여하기 위해 수행하는 **로직(행동)**
    - 객체에 의해 정의 되는 응집도 있는 행위의 집합
    - 객체가 유지해야하는 정보와 수행할수 있는 행동에대해 서술한 문장
- 책임을 **아는것/하는것** 으로 세분화
    - 하는것 : 객체생성이나 계산등 스스로하는것/ 다른객체의 행동을 시작시키기/ 다른객체의 홀동을 제어하고 조절
    - 아는것 : 사적인 정보를 아는것/ 관련된객체에대해 아는것/ 자신이 유도하거나 계산할수있느넋을 아는덧
    - 영화 예매에서의 책임
        - 상영- 영화예매(doing),영화알기(knowing) /영화- 요금계산(doing),가격과정책알기(knowing)
    - 책임과 메세지의 크기는 다르고, 책5임이 나뉘거나 커지기도함
    - **책임이 객체지향설계의 핵심**
        - 적절한 협력이 적절한 책임을 제공하고 , 적절한책임을 적절한 객체에 할당해야 단순하고 유연한 설계가 가능
    - CRC카드 : 후보/책임/협졀자
    

[책임할당]

- **정보전문가패턴**: information expert, 책임을 수행하는데 필요한 정보를 가장 잘 알고있는 전문가에게 그 책임을 할당, 자율적인객체를 만들수있음
- 책임을 할당하기 위해 먼저 협력이라는 문맥을 정의
    - 기능을 시스템이 담당할 하나의 책임으로 바라보고
    - 스시템의 책임을 완료하는데 ㅍ필요한 더 작은 책임을 찾아내어 객체에 할당하는것을 반복
- **책임주도설계** (Responsibility DD ,RDD): 책임을 찾고 책임을 수행할 적절한 객체를 찾아 할당하는 방식으로 협력을 설계하는 방법
- **메세지가 객체를 결정**
    - 책임 할당시 필요한 메세지 식별 후 ,메세지를 처리할 객체를 나중에 선택했음, 이유는
    - 객체가 최소한의 인터페이스를 가질수 있게되고
        - 메세지가 식별될때까지 퍼블릭인터페이스에 어떤것도 추가되지않고 필요한 인터페이스만 갖고됨
    - 객체가 충분히 추상적인 인터페이스르 ㄹ가질수 있게됨
        - 어떻게 수행하는지를 노출하지않고 무엇을 수행할지에 초점을 맞추는 인터페이스를 얻을 수 있음

[행동이 상태를 결정]

- 객체의 존재이유는 협력에 참여하기 위해.
- 행동이 협력에 참여할 수 있는 유일한 방법
- 객체의 내부구현에 초첨을 맞춘 설계법이 **데이터 주도설계**(DDD)
- 중요한것은 객체의 상태가 아니라 행동임. 행동을 결정하고 나서 상태를 결정하고, 행동이바로 객체의 책임이됨

[역할]

- 객체의 목적은 협력안에서 객체가 맡은 **책임의 집합** =역할
- 역할을 통해 유연하고 재사용가능한 협력을 얻을 수 있음
    - 다른것으로 교체할 수 있는 책임의 집합
    - 역할이 두 종류의 구체적인 객체를 포괄하는 **추상화**
    - 동일한 책임을 수행하는 역할을 기반으로 두개의 협력을 통합하여 코드중복 제거 가능
    - **추상클래스와 인터페이스**를 통해 역할 구현 가능
        - 추상클래스는 책임의 일부를 구현
        - 인터페이스는 구혀넚이 책임의 집합만을 나열
    - 다양한 객체가 참여하는게 확실하다면 면 역할로, 아니라면 협력으로 시작
- 역할은 객체가 참여할 수 있는 일종의 슬롯
    - 동일한 종류의 객체가 하나의 역할을 수행한다면 둘은 동일
    - 하나이상의 객체가 동일한 책임을 수행한다면 역할은 서로 다른 방법으로 실행할 수 있는 집함이 됨        
    - 역할을 설계의 중심개념으로 보는 역할 모델링개념도 젱ㄴ되었음
        - UML에 영향
- 추상화의 장점은 중요한 정책을 상위수준에서 단순화가능, 설계가 유연해지는것. 역할은 공통의 책임을 바탕으로 객체의 종류를 수기기때문에 추상화로 볼 수 있음. 위의장점이 협력의 관점에서 역할에게 적용됨
- 역할은 객체가 협력에 참여하는 잠시동안에만 존재하느 ㄴ일시적인존재(연극안에서 **배역을** 연기하는배우처럼)
    - 객체는 다양한 역할을 가질 수 있다
    - 협혁의 관점에서 동일한 역할을 수행하는 객체들은 대체 가능하다
    - 역할은 특정항 객체의 종류를 캡슐화 하기 때문에 참여하는 객체들은 다형적이다
