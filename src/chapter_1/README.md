# 소개

프로그램이 동작하도록 만드는 데 엄청난 수준의 지식과 기술이 필요하지는 않다.
어떻게 해서든 '동작'은 한다.
하지만 프로그램을 제대로 만드는 일은 전혀 다르다.
적정 수준의 지식과 기술을 겸비해야 한다. 사고력과 통찰력을 갖춰야 한다.
정말 어려운 일이다.

하지만 소프트웨어를 제대로 만들게 되면 마법과도 같은 일이 벌어진다.
소수의 프로그래머만으로 프로그램이 지속적으로 동작하도록 만들 수 있따.
새로운 기능을 추가하거나 유지보수 할 수 있고, 변경은 단순해지며 빠르게 반영할 수 있다.
결함은 적어지고 잦아든다.

최소한의 노력으로 기능과 유연성을 최대화할 수 있다.

## 설계(Design)와 아키텍처(Architecture)
설계와 아키텍처 사이에는 아무런 차이가 없다. 이들은 모든 고수준의 결정사항을 지탱하는 모든 세부사항을 자세하게 나타낸다.
저수준의 세부사항과 고수준의 결정사항은 전체 설계의 구성요소가 된다. 다만 주로 아키텍처는 고수준의 무언가를 가리키고, 설계는 저수준의 무언가를 가리킬 때가 많다.
우리는 따로 분리하지 않는다. 애초에 분리될 수 없는 것들이다.

### 좋은 소프트웨어 설계, 아키텍처의 목표

> 소프트웨어 아키텍처의 목표는 필요한 시스템을 만들고 유지보수하는 데 투입되는 인력을 최소화하는 데 있다.

설계 품질을 재는 척도는 고객의 요구를 만족시키는 데 드는 비용을 재는 척도와 다름없다. 
이 비용이 낮을 뿐만 아니라 시스템의 수명이 다할 때까지 낮게 유지할 수 있다면 좋은 설계라고 말할 수 있다.
새로운 기능을 출시할 때마다 비용이 증가한다면 나쁜 설계다.

좋지 못한 설계는 개발자의 노력을 기능 개발보다는 엉망이 된 상황을 대처하는 데 사용하도록 한다.
작은 기능을 개발하는데, 엉망이 된 코드를 같이 수정하느라 부작업이 추가된다.
그럼 개발자를 더 많이 고용하게 되는데, 개발자의 생산성은 떨어지고 인건비만 지출하게 된다.

이렇게 된 원인은 뭘까?

> 코드는 나중에 정리하면 돼. 당장은 시장에 출시하는 게 먼저야!

한 번 쯤은 들어봤거나, 겪어봤을 것들이다. 여기에 넘어가면 겉잡을 수 없이 망가지게 된다. 나중에 정리하는 일 따위는 발생하지 않는다.
다음 기능이 생기고, 코드를 정리할 시간은 없고, 이것이 반복되면 후에는 코드를 정리할 수 없다.
결국 코드는 엉망진창이 되고 개발자의 생산성은 0을 향해 수렴하기 시작한다.

> 엉망으로 만들면 깔끔하게 유지할 때보다 항상 더 느리다. 빨리 가는 유일한 방법은 제대로 가는 것이다.

## 두 가지 가치에 대한 이야기
모든 소프트웨어 시스템은 이해관계자에게 서로 다른 두 가지 가치를 제공하는데, 행위(behavior)와 구조(structure)이다.
소프트웨어 개발자는 두 가치를 모두 반드시 높게 유지해야 하는 책임을 진다.

### 행위 Behavior
프로그래머를 고용하는 이유는 이해관계자를 위해 기계가 수익을 창출하거나 비용을 절약하도록 만들기 위해서다.
이를 위해 프로그래머는 이해관계자가 기능명세서나 요구사항 문서를 구체화할 수 있도록 돕느다.
그리고 이해관계자의 기계가 이러한 요구사항을 만족하도록 코드를 작성한다.
기계가 이러한 요구사항을 위반하면 프로그래머는 디버거를 열고 문제를 고친다.

요구사항을 기계에 구현하고 버그를 수정하는 일이 그들의 행위이다.

### 아키텍처 Architecture, 설계 Design, 구조 Structure
소프트웨어라는 단어는 `부드러운 Soft`과 `제품 Ware`이라는 단어의 합성어이다.
`부드러운 Soft`이라는 단어에 두 번째 가치가 존재한다.

소프트웨어는 부드러움을 지니도록 만들어졌다. 소프트웨어를 만든 이유는 기계의 행위를 쉽게 변경할 수 있도록 하기 위해서이다.
알다싶이 하드웨어는 기계의 행위를 바꾸기 어렵게 만들어졌다.

소프트웨어가 가진 본연의 목적을 추구하려면 소프트웨어는 반드시 부드러워야 한다. 즉, 변경하기가 쉬워야 한다.
변경사항을 적용하는 데 드는 어려움은 변경되는 범위(scope)에 비례해야하며, 변경사항의 형태(shape)와는 관련이 없어야 한다.

소프트웨어 개발 비용의 증가를 결정짓는 주된 요인은 바로 이 변경사항의 범위와 형태의 차이에 있다.
바로 이 때문에 개발 비용은 요청된 변경사항의 크기에 비례한다.

대부분이 느꼈겠지만, 새로운 요청사항이 발생할 때마다 바로 이전의 변경사항을 적용하는 것보다 조금 더 힘들어지게 된다. 
이유는 시스템의 형태와 요구사항의 형태가 서로 맞지 않기 때문이다.

문제는 시스템의 아키텍처다. 아키텍처가 특정 형태를 다른 형태보다 선호하면 할수록, 새로운 기능을 이 구조에 맞추는 게 더 힘들어진다.

따라서 아키텍처는 형태에 독립적이어야 하고, 그럴수록 더 실용적이다.

### 더 높은 가치
* 기능 vs 아키텍처.
* 동작하도록 만드는 것 vs 시스템을 더 쉽게 변경할 수 있도록 하는 것.

완벽하게 동작하지만 수정이 아예 불가능한 프로그램은, 요구사항이 변경됨에 따라 폐기될 것이다.
반면 동작은 하지 않지만 변경이 쉬운 프로그램은, 동작하도록 변경해서 사용하면 된다. 변경사항에도 대처할 수 있다.

### 아이젠하워(Dwight D. Eisenhower) 매트릭스
드와이트 D. 아이젠하워 미국 대통령이 고안한 중요성과 긴급성에 관한 아이젠하워 매트릭스이다.

> 내겐 두 가지 유형의 문제가 있습니다. 하나는 긴급하며, 다른 하나는 중요합니다. 긴급한 문제는 중요하지 않으며, 중요한 문제는 절대 긴급하지 않습니다.

이 격언을 바탕으로 소프트웨어의 두 가치를 살펴보자.

첫 번째 가치인 행위는 긴급하지만 매번 높은 중요돌르 가지는 것은 아니다. 두 번째 가치인 아키텍처는 중요하지만 즉각적인 긴급성을 필요로 하는 경우는 절대 없다.

* 중요함, 긴급함
* 중요합, 긴급하지 않음
* 중요하지 않음, 긴급함
* 중요하지 않음, 긴급하지 않음.

우리는 위 순서대로 우선순위를 매겨야 한다. 중요한 일인 아키텍처는 상위 우선순위를 차지하는 반면, 행위는 하위 우선순위를 차지한다.
다만 이에 대한 우선순위를 무시하거나 제대로 구분 짓지 못하는 실수로 인해 시스템에서 중요도가 높은 아키텍처를 무시한 채 중요도가 떨어지는 기능을 선택하게 되는 경우가 발생한다.


### 아키텍처를 위해 투쟁하라

업무 관리자는 보통 아키텍처의 중요성을 평가할 만한 능력을 겸비하지 못한다. 이로 인해 개발자는 딜레마에 빠진다.
하지만 소프트웨어 개발자를 고용하는 이유는 바로 이 딜레마를 해결하기 위해서이다.

효율적인 소프트웨어 개발팀은 소프트웨어 아키텍처를 중요한 가치라고 믿고, 이를 위해 투쟁해야 한다.
그것이 당신이 고용된 이유다.





