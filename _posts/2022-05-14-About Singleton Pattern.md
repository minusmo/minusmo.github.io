---
layout: posts
title: About Singleton Pattern
category: designPattern
tags: OOP
---

## 싱글톤은

생성적 디자인 패턴으로, 하나의 클래스는 하나의 인스턴스만을 가져야 한다는 패턴이다.

그리고 프로그램 전체에서 단 하나의 접근 지점을 가져야한다.

이 패턴의 주요 아이디어는, 하나의 클래스가 하나의 인스턴스만을 책임지게 하는 것이다.

싱글톤은 매우 단순한 디자인 패턴이지만, 조심하지 않으면 실수하기도 쉽다.

## 기본 구조

싱글톤 클래스는 **static** property _instance_ 를 가진다. 이 property는 이 클래스의 단 하나의 인스턴스를 참조한다.

이 인스턴스는 반드시 **static method** _getInstance()_ 를 통해서만 접근 가능하다.

클래스 생성자는 **private** 하고, 이로 인해 클래스 밖으로 부터 _instantiated_ 되는 것을 막아야한다.

![singleton pattern diagram](/assets/images/singleton.png)

### 방법론적인 이해

새로운 인스턴스를 생성하지 않고, 클래스 안에 _캐싱된_ 멤버 변수를 지속적으로 참조해 멤버 함수를 호출하는 것으로 기능을 수행하는 것으로 이해할 수 있다.

## 언제 사용하는가

싱글톤은 인스턴스를 생성하는 것이 코스트를 많이 유발할 때 사용될 수 있다. _예) 인스턴스를 생성하는 것이 외부로 부터 많은 데이터를 로드하는 것을 필요로 할때_

또한 프로그램에서 같은 object를 계속해서 참조해야 할 때 유용하다.

특정 캐싱 레이어가 필요할 때도 싱글톤 패턴을 사용할 수 있다. 싱글톤 클래스는 인스턴스 요청에 대한 캐시를 _check and manage_ 할 수 있다.

## 주의할 점

- 싱글톤 디자인을 적용할 때는, 반드시 _lazy construction_ 이 고려되어야 한다.
  클래스 인스턴스는 반드시 그것이 처음으로 필요할 때만 성성되어야 한다.
- 보통, 싱글톤 클래스는 생성자의 _parameter 를 받지 않는다.
  만약 받는다면 싱글톤 패턴의 아이디어에 위배되지 않는가?를 고려할 필요가 잇다._
- 스레드 안전성: _멀티 스레드_ 어플리케이션에서의 싱글톤 패턴은 주의할 필요가 있다.
  만약 싱글톤에서 _mutable data 를 가지고 있다면, 스레드-안전성을 위협할 수 있다._
- 몇몇 경우에서는 싱글톤 패턴이 _anti-pattern_ 으로 여겨지기도 한다. 이는 싱글톤 패턴이 **_SOLID_** 원칙(단일 책임 원칙)을 위배하기 때문이기 때문이다. 싱글톤을 다룰 때는, 인스턴스의 수명을 별도로 관리해야 한다. 또한 싱글톤은 _단위 테스트 를 어렵게한다._ 싱글톤처럼 작동하는 인터페이스를 제공하는 _mockup_ 을 만들 수 없기 때문이다.