---
title: About Adapter Pattern
category: designPattern
tags: OOP
toc: true
toc_label: "Contents"
---

## 어댑터는

**구조적** 디자인 패턴으로, **wrapper** 로도 알려져 있다. 가장 흔하고 유용한 디자인 패턴으로 알려져있다.

_Gang of Four_ 에 따르면 이 패턴의 디자인 의도는 다음과 같다.

_한 클래스의 인터페이스를 클라이언트가 기대하는 또 다른 인터페이스로 변환한다. 어댑터는 호환되지 않는 인터페이스를 가진 클래스들이 함께 작동하게 한다._

예를 들어 서드파티 api를 사용할 때, 어댑터 클래스는 외부 api와 나의 코드 사이에 위치하여 외부 인터페이스를 노출하지 않고 호환되게 한다.

![adapter pattern diagram1](/assets/images/adapter0.png)

### 객체 어댑터와 클래스 어댑터

어댑터 패턴에는 객체 어댑터와 클래스 어댑터가 있다. 두 어댑터는 다른 구조를 가지고 있지만, 같은 아이디어를 공유한다.

- _Target 또는 ITarget_ 은 클라이언트가 사용하는 _domain-specific_ 한 인터페이스를 정의한다.
- 클라이언트는 _Target_ 인터페이스를 따르는 객체들과 상호작용한다.
- **_Adaptee는 adapting이 필요한 기존 인터페이스를 정의한다. ex) third-party library_**
- **_Adapter는 Adaptee의 인터페이스를 Target 인터페이스에 적응시킨다.(Adapting)
  이것이 이 패턴의 주요 목적이며, 호환되지 않는 두 코드를 호환시킨다._**

**객체 어댑터는**

객체(Adaptee)의 구성요소에 의존하여 Target 인터페이스 구현한다. 다시 말해, 어댑터는 Target 인터페이스 기능을 Adaptee 클래스의 자세히 구현된 기능을 호출하는 것으로 작동하게 된다.

**클래스 어댑터는**

Adaptee 클래스를 상속하여 Target 인터페이스를 구현한다.

**_둘 중 어느것을 사용해야 할까? 답을 위해 몇가지를 따져보자._**

1. 클래스 어댑터를 사용하기 위해서는 **다중 상속** 이 필요하다.따라서 다중 상속을 지원하지 않는 언어에서는 사용하기 어렵다.
2. 클래스 어댑터의 장점은 Adaptee 클래스를 상속받아 쉽게 상위 클래스의 동작을 오버라이드하여 사용할 수 있다. 그러나, 객체 어댑터 방식이 **더욱 유연하다.** Client and Adaptee 가 느슨하게-결합(loosely-coupled)되기 때문이다. 이는 *run-time*에서 Adaptee 클래스에 기능을 위임하기 때문이며, **단일 어댑터를 생성하여 인터페이스가 일치하는 다수의 다른 adaptee들 사용할 수 있다는 것이다.**
3. 객체 어댑터를 사용하면 런타임 환경에서 쉽게 Adapter 클래스 내에서 Adaptee 의 구현을 교환하여 사용할 수 있다. 그러나 이는 **_Liskov substitution principle_** 을 고려하여 사용할 필요가 있다.

## 언제 적용하는가?

- 어댑터 디자인 패턴은 서드 파티 라이브러리 혹은 외부 코드가 현재 당신이 개발하는 어플리케이션의 인터페이스와 호환되지 않을 때 사용한다.
- 외부 데이터 소스를 호출하거나 외부 API를 사용할 때, 데이터를 변환하거나 감싸서 당신의 프로그램의 _비즈니스 로직_ 과 분리하고 싶을 때 사용한다.
- 비슷한 기능을 가지는 서로 다른 API를 사용하고 싶을 때 유용하다. 이런 경우에, _도메인 레이어 코드_ 는 어댑터의 똑같은 인터페이스를 계속 사용하는 채로 모든 _부수적인 작업들_ 을 어댑터 클래스 안에서 해결할 수 있다.

⇒ 이러한 코드 추상화는 _도메인 레이어 코드_ 의 _단위 테스트_ 를 더 쉽게 만들 수 있다.

## 적용 사례

두개의 서로다른 외부 소스로 부터 각각 JSON, XML 데이터를 받아 하나의 주소록 인터페이스를 제공하도록 하는 경우.

![adapter pattern diagram2](/assets/images/adapter1.png)
