# 컴포넌트
SOLID 원칙이 벽과 방에 벽돌을 배치하는 방법을 알려준다면, 컴포넌트 원칙은 빌딩에 방을 배치하는 방법을 설명해준다.
큰 빌딩과 마찬가지로 대규모 소프트웨어 시스템은 작은 컴포넌트들로 만들어진다.

컴포넌트는 배포 단위이다. 자바의 경우 jar 파일, 루비에서는 gem 파일, 닷넷에서는 DLL 이다.
컴파일형 언어에서 컴포넌트는 바이너리 파일의 결합체다. 인터프리터형 언어의 경우는 소스 파일의 결합체다.
모든 언어에서 컴포넌트는 배포할 수 있는 단위 입자이다.

여러 컴포넌트를 서로 링크하여 실행 가능한 단일 파일로 생성할 수 있다.
또는 여러 컴포넌트를 서로 묶어서 .war 파일과 같은 단일 아카이브로 만들 수도 있다.
또는 컴포넌트 각각을 .jar 나 .ddl  같이 동적으로 로드할 수 있는 플러그인이나 .exe 파일로 만들어서 독립적으로 배포할 수도 있다.
컴포넌트가 마지막에 어떤 형태로 배포되든, 잘 설계된 컴포넌트라면 반드시 독립적으로 배포 가능한, 따라서 독립적으로 개발 가능한 능력을 갖춰야 한다.

## 컴포넌트 응집도
어떤 클래스를 어떤 컴포넌트에 포함시켜야 할지 결정하는 것은 중요하다.
안타깝게도 우리는 수년 동안 거의 순전히 상황에 따라 임시방편적으로 결정을 내려왔다.
이 결정을 위한 컴포넌트 응집도와 관련된 소프트웨어 엔지니어링 원칙을 소개하겠다.

### REP: 재사용/릴리스 등가 원칙 Reuse/Release Equivalence Principle
> 재사용 단위는 릴리스 단위와 같다.

우리는 소프트웨어 재사용의 시대에 살고 있다.

단일 컴포넌트는 응집성 높은 클래스와 모듈들로 구성되어야 한다.
단순히 뒤죽박죽 임의로 선택된 클래스아 모듈로 구성되어서는 안 되며, 
컴포넌트를 구성하는 모든 모듈은 서로 공유하는 중요한 테마나 목적이 있어야 한다.
즉, 하나의 컴포넌트로 묶인 클래스와 모듈은 반드시 함께 릴리스할 수 있어야 한다.

### CCP: 공통 폐쇄 원칙 Common Closure Principle

> 동일한 시점에 동일한 이유로 변경되는 것들을 한데 묶어라. 서로 다른 시점에 다른 이유로 변경되는 것들은 서로 분리하라.

조금 더 구체적으로 말하면, 아래와 같다.
> 동일한 이유로 동일한 시점에 변경되는 클래스를 같은 컴포넌트로 무껑라. 서로 다른 시점에 다른 이유로 변경되는 클래스는 다른 컴포넌트로 분리하라.

이 원칙은 단일 책임 원칙(SRP)을 컴포넌트 관점에서 다시 쓴 것이다.
SRP 에서 단일 클래스는 변경의 이유가 여러 개 있어서는 안 된다고 말하듯이, CCP 에서도 마찬가지로 단일 컴포넌트는 변경의 이유가 여러 개 있어서는 안 된다고 말한다.

애플리케이션에서 코드가 반드시 변경되어야 한다면, 이러한 변경이 여러 컴포넌트 도처에 분산되어 발생하기보다는, 차라리 변경 모두가 단일 컴포넌트에서 발생하는 편이 낫다.
만약 변경을 단일 컴포넌트로 제한할 수 있다면, 해당 컴포넌트만 재배포하면 된다. 변경된 컴포넌트에 의존하지 않는 다른 컴포넌트는 다시 검증하거나 배포할 필요가 없다.

CCP 는 같은 이유로 변경될 가능성이 있는 클래스는 모두 한곳으로 묶을 것을 권한다.
이를 통해 소프트웨어를 릴리스, 재검증, 배포하는 일과 관련된 작업량을 최소화할 수 있다.

또한 CCP 에서 말하는 폐쇄에는 OCP 에서의 폐쇄와 같은 의미이다.
동일한 유형의 변경에 대해 닫혀 있는 클래스들을 하나의 컴포넌트로 묶음으로써, 변경이 필요한 요구사항이 발생했을 때 그 변겨이 영향을 주는 컴포넌트들이 최소한으로 한정되게 한다.

### CRP: 공통 재사용 원칙 Common Reuse Principle

> 컴포넌트 사용자들을 필요하지 않는 것에 의존하게 강요하지 마라.

CRP 는 클래스와 모듈을 어느 컴포넌트에 위치시킬지 결정할 때 도움되는 원칙이다.
같이 재사용되는 경향이 있는 클래스와 모듈들을 같은 컴포넌트에 포함해야 한다.

예시로, 컨테이너(Container) 클래스와 해당 클래스의 이터레이더(Iterator) 클래스는 서로 강하게 결합되어 있다.
그리고 함께 재사용된다. 따라서 이들은 반드시 동일한 컴포넌트에 위치해야 한다.

또한 CRP 는 각 컴포넌트에 어떤 클래스들을 포함시켜야하는지 뿐 아니라, 묶어서는 안 되는 클래스가 무엇인지도 말해준다.
서로 의존하는 컴포넌트는, 한쪽의 변경만 발생해도 다른쪽을 함께 변경해야 할 가능성이 있다. 혹은 그렇지 않더라도 재컴파일, 재검증, 재배포의 가능성이 남아있다.
따라서 의존하는 컴포넌트가 있다면 해당 컴포넌트의 모든 클래스에 대해 의존함을 확실히 인지해야 한다.
즉, 의존하는 컴포넌트의 일부 클래스에만 의존하고 다른 클래스와는 독립적일 수 없다는 말이다.

CRP 는 어떤 클래스를 한데 묶어도 되는지보다는, 어떤 클래스를 한데 묶어서는 안 되는지에 대해 훨씬 더 많은 것을 이야기한다.
강하게 결합되지 않은 클래스들을 동일한 컴포넌트에 위치시켜서는 안 된다는 것이다.

CRP 는 ISP(인터페이스 분리 원칙)의 포괄적인 버전이다.
ISP 는 사용하지 않은 메서드가 있는 클래스에 의존하지 말라고 조언한다.
CRP 는 사용하지 않는 클래스를 가진 컴포넌트에 의존하지 말라고 조언한다.
이 두 조언은 한 문장으로 요약할 수 있다.

> 필요하지 않은 것에 의존하지 마라.

## 컴포넌트 결합
### ADP: 의존성 비순환 원치
> 컴포넌트 의존성 그래프에 순환(cycle)이 있어서는 안 된다.

하루 종일 일해서 무언가를 작동하게 만들어 놓고 퇴근했는데, 이튿날 출근해 보면 전혀 돌아가지 않는 경험을 해본 적이 있지 않은가?
누군가 당신보다 더 늦게, 당신이 의존하고 있던 무언가를 수정했기 때문이다.
저자는 이를 숙취 증후군이라고 부른다.

이에 대한 해결책으로는 '주 단위 빌드'와 '의존성 비순환 원칙'이 있다.

#### 주 단위 빌드
중간 규모의 프로젝트에서 흔히 사용되는 방식인데, 주 4일동안은 각자 편히 개발하고, 금요일에 병합을 하는 것이다.
4일 동안 개발자를 고립된 세계에서 살 수 있게 보장해 준다는 멋진 장점이 있지만, 금요일에 병합과 관련한 업보를 치러야 한다는 단점이 있다.
프로젝트 크기가 커지면 병합이 하루만에 되지 않을 수 있고, 병합 자체의 난이도가 커질 것이다.
통합에 드는 노력이 더 커지고, 이는 비효율적이다.

#### 순환 의존성 제거하기
의존성 구조에 순환이 생기면 숙취 증후군을 피해 갈 수 없다.
책에 그림과 함께 잘 설명 되어있다.

컴포넌트는 시스템에서 가장 먼저 설계할 수 있는 대상은 아니다.
오히려 시스템이 성장하고 변경될 때 함께 진화한다.

### SDP: 안정된 의존성 원칙
> 안정성의 방향으로(더 안정된 쪽에) 의존하라.

설계는 결코 정적일 수 없다. 공통 폐쇄 원칙을 준수하면서, 컴포넌트가 다른 유형의 변경에는 영향 받지 않으면서도 특정 유형의 변경에만 민감하게 만들 수 있다.
이처럼 컴포넌트 중 일부는 변동성을 지니도록 설계되는데, 우리는 변동성을 지니도록 설계한 컴포넌트는 언젠가 변경되리라고 예상한다.

변경이 쉽지 않은 컴포넌트가 변동이 예상되는 컴포넌트에 의존하게 만들어서는 절대로 안 된다.

옆으로 세운 동전을 우리는 안정적이라고 보지 않는다.
가만히 세워두고 건드리지 않으면 계속 그 상태로 서있음에도 불구하고 우리는 안정적이라 부르지 않는다.
우리가 옆으로 세워둔 동전을 안정적이지 않다고 보는 이유는, 적은 힘으로 넘어뜨릴 수 있기 때문이다.

즉, 안정적인 것은 쉽게 움직이지 않는 것이다.
소프트웨어 관점에서, 소프트웨어 컴포넌트를 변경하기 어렵게 만드는 것은 무엇일까?
바로 수많은 컴포넌트가 해당 컴포넌트를 의존하게 만드는 것이다.
사소한 변경이라도 의존하는 모든 컴포넌트를 만족시키면서 변경하려면 상당한 노력이 들기 때문이다.

#### 안정성 지표
컴포넌트의 안정성은 컴포넌트로 들어오고 나가는 의존성의 개수를 세어보는 방법으로 측정할 수 있다.

* Fan-in: 안으로 들어오는 의존성. 컴포넌트 내부의 클래스에 의존하는 컴포넌트 외부의 클래스 개수를 나타냄.
* Fan-out: 바깥으로 나가는 의존성. 컴포넌트 외부의 클래스에 의존하는 컴포넌트 내부의 클래스 개수를 나타냄.
* I(불안정성): I = Fan-out / (Fan-in + Fan-Out). 나가는 의존성이 많을수록, 즉 외부에 의존할수록 안정적이다.

SDP 에서 컴포넌트의 I 지표는 그 컴포넌트가 의존하는 다른 컴포넌트들의 I 보다 커야 한다고 말한다.
의존성 화살표의 시작 부분의 컴포넌트가, 의존성 화살표의 끝 부분의 컴포넌트보다 불안정해야 한다는 것이다.

만약 위 규칙을 어기는 경우, 추상 컴포넌트와 DIP 를 활용하여 해결할 수 있다.
책 130 페이지에 자세하게 설명되어 있다.

### SAP: 안정된 추상화 원칙
> 컴포넌트는 안정된 정도만큼만 추상화되어야 한다.

SAP 는 안정성과 추상화 정도 사이의 관계를 정의한다.
안정된 컴포넌트는 추상 컴포넌트여야 하며, 이를 통해 안정성이 컴포넌트를 확장하는 일을 방해해서는 안 된다.
불안정한 컴포넌트는 반드시 구체 컴포넌트여야 한다. 컴포넌트가 불안정하므로 컴포넌트 내부의 구체적인 코드를 쉽게 변경할 수 있어야 하기 때문이다.

SAP 와 SDP 를 결합하면 컴포넌트에 대한 DIP 나 마찬가지가 된다.
SDP 에서는 의존성이 반드시 안정성의 방향으로 향해야 한다고 말하며,
SAP 에서는 안정성이 결국 추상화를 의미한다고 말하기 때문이다.
따라서 의존성은 추상화의 방향으로 향하게 된다.

이를 잘 나타내는 것이 130 페이지 그림이다.

