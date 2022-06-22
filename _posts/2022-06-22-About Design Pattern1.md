---
title: About Adapter Pattern
category: designPattern
tags: OOP 
toc: true
toc_label: "Contents"
---

# Introduction

# 디자인 패턴이란

디자인 패턴은 충분히 테스트된, 검증된 개발/디자인 패러다임을 제공함으로써, 개발 프로세스의 효율을 높이는 데 있다. 이것은, 디자인 패턴은 하나의 아이디어를 말하는 것이지, 특정한 구현방법을 말하는 것이 아니라는 것이다. 이러한 디자인 패턴을 적용함으로써, 더욱 *유연하고, 재사용가능하며, 유지가능한* 코드를 작성할 수 있다. 

디자인 패턴을 적용하는 것은 의무가 아니다. 디자인 패턴은 프로젝트 개발만을 위한 것이 아니다. 디자인 패턴은 **common problem solving** 을 위한 것이다. 적재적소에 필요한 패턴을 적용하는 것이 목적이다. 

어떤 상황에 어떤 패턴이 적절한지는 *직접 적용해 보는 것* 만을 통해 이해할 수 있다.

예를 들어, 많은 상황에서 우리는 *단 하나*의  인스턴스 만을 생성하기를 원할 수 있다.

이러한 상황에서는 **싱글톤 패턴** 을 적용가능하다. 다양한 객체에서 동일한 **DB connection** 을 원할 수 있다. 하지만 여러개의 객체에 대하여 각각의 DB connection을 생성하는 것은 비용이 많이든다. 
비슷하게, 어플리케이션에서 다수의 제어객체를 생성하기 보다는 단 하나의 설정 객체 혹은 에러 제어 객체를 생성하므로써 모든 문제 상황을 제어하는 상황도 있다. 

# 디자인 패턴의 큰 분류

디자인 패턴에는 크게 **3가지의 분류** 가 있다.

## 1. 생성적 패턴

이 패턴은 *class instanciating* 이나 *object creation* 에 관한 것이다. 이 패턴은 나아가 **클래스 생성 패턴** 그리고 **객체 생성 패턴** 으로 세분화 될 수 있다. 클래스 생성 패턴은 인스턴시에이팅 과정에서 *상속* 을  효과적으로 사용하는 반면, 객체 생성 패턴은 *위임* 을 효과적으로 사용하여 상황을 해결한다. 

생성적 패턴에는

- Factory Method
- Abstract Factory
- Builder
- Singleton
- Object Pool
- Prototype

이 있다.

만약 비슷한 종류의 인스턴스를 여러개 생성하고 싶고, *loose coupling* 을 달성하고 싶다면, *Factory pattern* 을 적용할 수 있다. 팩토리 패턴은 여러개의 클래스 사이의 *다리* 같은 역할을 한다. 

다양한 데이터베이스 서버를 사용하는 경우를 생각해보자.(SQL server나 Oracle같은) 만약 SQL 서버를 백엔드로 사용하는 어플리케이션을 개발하고 있다고 하자. 그러나 미래에 데이터베이스를 오라클로 바꿔야 하는 상황이 발생한다. 이런 상황에서, 기존의 코드를 모두 변경해야 할 것이다. 이 때, 팩토리 메소드 패턴을 이용하여 비슷한 종류의 객체를 생성하여 *느슨한 결합* 을 달성할 수 있다. 

## 2. 구조적 패턴

이 패턴은 서로 다른 클래스들과 객체들을 조직화하여 더 큰 구조를 형성하고 새로운 기능을 제공하는 데 사용된다. 

구조적 패턴에는 

- Adapter
- Bridge
- Composite
- Decorator
- Facade
- Flyweight
- Private Class Data
- Proxy

이 잇다. 

2개의 인터페이스가 서로 호환이 되지 않고, 이 둘 사이에 새로운 관계를 정립하고 싶을 때 *어댑터 패턴* 을 사용할  수 있다. *어댑터 패턴* 은 클래스의 하나의 인터페이스를 다른 하나의 인터페이스나 클래스로(client가 요구하는) 변환한다. 

## 3. 행동적 패턴

이 패턴은 객체들간의 *공통적 상호작용 패턴을 식별하고, 그 패턴을 실체화하는 데 사용된다.*

행동적 패턴에는,

- Chain of responsibility
- Command
- Interpreter
- Iterator
- Mediator
- Memento
- Null Object
- Observer
- State
- Strategy
- Template method
- Visitor

***템플릿 패턴*** 은 수행단계에서 몇개의 단계를 *하위 클래스들* 로 미룸으로써, 알고리즘의 뼈대를 정의한다.

템플릿 메소드는 하위 클래스들이 알고리즘의 특정 단계들을 알고리즘의 구조 변경 없이 **재정의** 할 수 있게 한다.

예를 들어, 프로젝트에서, 모듈이 확장가능하여 해당 모듈이 새롭고 다른 방법으로(어플리케이션이 요구하는 방향으로) 행동하기를 바랄 수 있다. 하지만 소스코드의 변경이 허용되지 않을 때(변경은 허용되지 않으나, 추가는 허용되는 경우) 템플릿 메소드를 적용할 수 있다. 

[Design pattern Introduction on Geeks for Geeks]([https://www.geeksforgeeks.org/design-patterns-set-1-introduction/](https://www.geeksforgeeks.org/design-patterns-set-1-introduction/))