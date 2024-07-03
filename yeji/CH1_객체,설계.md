[프로그래밍 패러다임]

패러다임 = 모델,패턴에서 한시대의 사회 전체가 공유하는 이론이나 방법,문제의식을 뜻하게 됨

과학혁명 = 과거의 패러다임이 새로운 패러다임에의해 붕괴되는 혁명적 과정으로 새로운 패더라임으로 대체되어 정상과학의 방향과 성격이 변함 (패러다임 전환)

이 책에서의 패러다음 전환은 절차형→ 객체지향형 패러다임으로의 변화

프로그래밍 패러다임은 개발자 공동체가 동일한 프로그래밍 스타일과 모델을 공유함으로서 불필요한 부분에 대한 의경 충돌을 방지 (프로그래밍에서 패러다임끼리는 공존가능하다기에 혁명적 관점이 아니라 발전적으로 보임)

[객체,설계]

실무를 관찰한 결과를 바탕으로 실용성을 입증하고서 이론을 입증, 소프트웨어 개발에서는 이렇게 실무가 이론보다 앞선 분야가 소프트웨어 설계와 유지보수< 이책은 이를 설명하는 책

[티켓 판매 어플리케이션 구현]

- 소프트웨어에서 모듈이 가져야하는 세가지 기능
    
    ( 모듈은 클래스,패키지, 라이브러리와 같이 프로그램을 구성하는 임의의 요소)
    
    - 실행중에 제대로 동작/ 변경 용이/ 코드로 의사소통
- 1차 객체 구현
    
    ```java
    //무료 초대장을 티켓으로 교환하여 입장하거나 
    //현금을 가지고 티켓을 구매하여 입장
    public class Bag{
    	private Long amount;
    	private Invitation invitation;
    	private Ticket ticket;
    	
    	//생성시점에 강제
    	//현금이나 초대장을 가지고있거나 티켓을 가지고 있는상태만 가능
    	public Bag(long amount){
    		this(null,amount)
    	}
    	public Bag(Invitation in,long amount){
    		this.in = in;
    		this.amount =amount;
    	}
    }
    
    //관람객은 가방을 가질 수 있다
    public class Audience{
    private Bag bag;
    }
    
    //매표소에는 판매할 티켓과 판매금액이 존재
    public class TicketOffice{
    	private Long amount;
    	private List<Ticket> tickets = new ArrayList<>();
    	
    	publkic TicketOffice(Long amount, Ticket ..tickets){
    		this.tickets.addAll(Arrays.asList(tickets))
    		}
    	
    	public Ticket getTicket(){
    		return tickets.remove(0);
    		}
    	public void minusAmount(Ling amount){
    		this.amount --amount;
    		}
    }
    
    //판매원은 매표소에서 초대장교환,판매를 맡고 일하는 매표소를알아야함
    public class TicketSeller{
    	private TicketOffice ticketoffice;
    	public getTicketOffice();
    }
    ```
    


```java
//가방안의 초대장을 확인하고 티켓을 가방에 주고
//없으면 판매하여 매표소의 금액을 증가시키고 가방에줌
public class Theater{
	private TickerSeller ticketSeller;
	
	public void enter(Audience audience){
		if(audience.getBag().hasInvitation()){
			Ticket ticket = ticketSeller.getTicketOffice().getTicket();
			audiemce.getBag().setTicket(ticket );
		}else{
			Ticket ticket = ticketSeller.getTicketOffice().getTicket();
			audiemce.getBag().minusAmount(ticket.getFee());
			ticketSeller.getTicketOffice().plusAmount(ticket.getFee());
			audiemce.getBag().setTicket(ticket );
		}
	}	
}

위 코드는 변경이 힘들고 의사소통이 어렵다.
1. **의사소통이 어려움** : 관람객 입장에서는 제 3자가 가방에 접근하고, 판매원의 입장에서는 소극장이 접근하는 문제 발생
전제조건을 모두 알아야 이해 가능
2. **변경에 취약함** : 관람객과 판매원을 변경 할 경우 극장도 바꿔야함
객체사의의 의존성 제거 하여 최소한의 의존성만 유지
( 완전히 없앨 순 없고, 서로 존하면서 현렵하는 객체드르이 공동체 구축)
-> 의존성이 과한 경우를 **결합도**가 높다고 한다

[설계 개선(자율성 증가)]
코드를 이해하기 어려운 이유는 극장이 관람객의 가방과 판매원은 매표소에 직접 접근하기 때문
 → 자신의 일을 스스로 처리한다는 우리의 직관을 벗어남
직접접근 = 결합도가 높음
개선방안 : 관람객과 판매원을 자율적인 존재로 만듬
```

- 설계 개선
    1. 판매원에게 판매 로직 이동
        
        get메서드가 없애면서 객체 내부의 세부사항을 감추는 **캡슐화** 되었음
        
        극장이 판매원 내부의 매표소에 접근하지 않고 내부 로직을 모름 → 판매원의 **인터페이스에** 의존, 내부에 매표소 인스턴스를 포함한다는 사실은 구현영역에 **속함**
        
        결합도를 낮추고 변경하기 쉬운코드를 작성하는 원칙 중 하나  : 객체를 인터페이스와 구현으로 나누고 인터페이스만 공개한다
        
        ```java
        public class TicketSeller{
        	private TicketOffice ticketoffice;
        	
        	public void sellTo(Audience audience){
        		if(audience.getBag().hasInvitation()){
        			Ticket ticket = ticketOffice().getTicket();
        			audiemce.getBag().setTicket(ticket );
        		}else{
        			Ticket ticket = ticketOffice().getTicket();
        			audiemce.getBag().minusAmount(ticket.getFee());
        			ticketOffice().plusAmount(ticket.getFee());
        			audiemce.getBag().setTicket(ticket );
        		}
        	}
        }
        
        public class Theater{
        	private TickerSeller ticketSeller;
        	
        	public void enter(Audience audience){
        		ticketSeller.sellTo(audience)
        	}	
        }
        
        ```
        
    2. 관객 캡슐화 및 인터페이스만 공개 = 자율전인 존재
        
        ```java
        public class Audience{
        	private Bag bag;
        	
        	public Long buy(Ticktet){
        		if(bag.hasInvitation()){
        			bag.setTicket(ticket);
        			return 0L;
        		}else{
        			bag.setTicket(ticket);
        			bag.minusAmount(ticket.getFee());
        			return (ticket.getFee());			
        		}
        	}
        }
        
        public class TicketSeller{
        	private TicketOffice ticketoffice;
        	
        	public void sellTo(Audience audience){
        		ticketOffice().plusAmount(audience.buy(ticketoffice.getTicket()));
        	}
        }
        
        ```
        


관람객과 판매원을 변경 할 경우에도 극장변경필요 X

객체 내부의 상태를 캡슐화하고 객체간에 오직 메세지를 통해서만 상호작용

**응집도**= 밀접하게 연관된 작업만 수행하고 연관성없는 작업은 다른 객체에게 위윔

스스로 자신의 데이터를 처리하여 응집도를 높이고 결합도를 낮출수 있다

[객체지향과 절차지향]

- 처음 개발한 극장안에서 티켓을 사고파는 코드는 절차지향.
    - 극장의 입장 메서드가 **프로세스**이고, 관람객 판매원은 **데이터**가 된다.
    - 프로세스와 데이터를 볈도의  모듈에 위치시키는 방식을 **절차지향적 프로극래밍** (의존성 구조를 가짐, 모든처리가 하나의 클래스안에 위치하고 나머지클래스는 데이터의 역할만 수행하기 때문)
    - 우리의 직관을 위배하여 의사소통이 어렵고 데이터 변경으로 인한 영향을 지역적으로 고립시키기 어려워서 변경하기 어려움
- 데이터와 프로세스가 동일한 모듈 내부에 위치하도록 한것이 **객체지향** 프로그래밍
    - 캡슐화를 이용해 의존성을 관리하여 객체사이의 결합도를 낮추는것이 설계 핵심
- **책임의 이동**이 두 방식간 근본적인 차이를 반든다
    - 절차지향은 **책임이 집중**되어있음 ( 작업 흐름이 극장에 의해 제어됨)
        
        극장에 몰려있던 책임이 개별 객체로 이동 = **책임이 이동**됨
        
    - 객체지향은 책임이 분산됨 ( 하나의 기능을 완성하는데 필요한 책임이 분산, 제어흐름이 각 객체에 분산됨)
        
        자신을 스스로 책임짐
        
        객체지향의 핵심은 하나의 객체안에 모으기 + 적절한 객체에 적절한 책임 할당 (어떤 데이터를 가질지 보단 책임 할당에 초점을 맞추기)
        
        
- 한번 더 개선?
    
    ```java
    //가방이 관객에게 끌려다니는 수동적인 존재.이기에 개선하여 캡슐화
    public class Bag{
    	private Long amount;
    	private Invitation invitation;
    	private Ticket ticket;
    	
    	public Long hold(Ticket){
    			if(hasInvitation()){
    			setTicket(ticket);
    		}else{
    			setTicket(ticket );
    			minusAmount(ticket.getFee());
    			return ticket.getFee()
    		}
    	}	
    }
    
    //로직제거
    public class Audience{
    	private Bag bag;
    	
    	public Long buy(Ticktet){
    		return baf.hold(ticket);
    }
    
    // 판매원이 판매소의 자율권 침해중이기에 수정
    public class TicketSeller{
    	private TicketOffice ticketoffice;
    	
    	public void sellTo(Audience audience){
    		ticketOffice.plusAmount(audience.buy(ticketoffice.getTicket()));
    	}
    }
    
    // 판매원이 인터페이스에만 의존함
    //but 관객과 부스간 의존성이 ㅅ생성됨
    // 판매소이 자율성은 높아졌지만 전체적인 결합도가 상승함
    public class TicketOffice{
    	private Long amount;
    	private List<Ticket> tickets = new ArrayList<>();
    	
    	publkic TicketOffice(Long amount, Ticket ..tickets){
    		this.tickets.addAll(Arrays.asList(tickets))
    	}
    	public void sellTicketTo(Audience){
    		plusAmount(audience.buy( getTicket()))
    		}
    	
    	private Ticket getTicket(){
    		return tickets.remove(0);
    	}
    	public void minusAmount(Ling amount){
    		this.amount --amount;
    	}
    }
    ```
    

판매원이 인터페이스에만 의존하면서 but 관객과 부스간 의존성이 ㅅ생성됨
판매소의 자율성은 높아졌지만 전체적인 결합도가 상승하는 문제가 발생하여 트렝드 오프 핗요

→ 기능 설계에 대한 방싣이 여러개 있을수 있다 + 각 방법(설계는)은 트레이드오프의 산물이다

의인화 : 현실에서는 수동적인 존재더라도 객체지향에서는 능동적이고 자율적인 존재가 됨

[셀계가 왜 필요한가]

설계 =코드를 배치하는 것

설계는 코드작성의 일부이며 매수간 어떻게 배치하는것도 포함

좋은 설계 = 기능이 구현 + ㅜ변경 용이

요구사항이 항상 병견되기때무네 변경 될수있는 설계가 중요, + 코드 수정은 버그가 추가될 가능성이 높기 때문

[객체지향 설계]

객체지향 프로그래밍은 의존성을 적절하게 관리하여 요구사항에 수월하게 대응할 수있는 가능성을 높임.

변경이 쉽다는것은 이해하기 쉽다는 뜻

객체지향 패러다음은 세상을 바라 보는 방식대로 코드를 작성하게 돕는다

데이터와 프로세스를 모으고, 객체들각 의존성을 적절하게 조절하는것이 훌륭한 ㄱㄱ체지향 설계
