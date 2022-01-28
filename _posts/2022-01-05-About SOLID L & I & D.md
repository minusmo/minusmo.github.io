---
layout: posts
title: About SOLID L & I & D
category: programming
tags: programmingPhilosophy OOP
---

## SOLID: 객체 지향 설계의 다섯 가지 원칙

### S: SRP(Single Responsibility Principle)
#### 한 클래스는 하나의 책임만 가져야 한다.

### O: OCP(Open/Closed Principle)
#### 소프트웨어 요소는 확장에는 열려있으나 변경에는 닫혀있어야한다.  

### L: LSP(Liskov Substitution Principle)
#### 프로그램의 객체는 프로그램의 정확성을 깨뜨리지 않으면서 하위 타입의 인스턴스로 바꿀 수 있어야 한다.(계약에 의한 설계)

### I: ISP(Interface Segregation Principle)
#### "특정 클라이언트를 위한 인터페이스 여러 개가 범용 인터페이스 하나보다 낫다."  

### D: DIP(Dependency Inversion Principle)
#### 프로그래머는 추상화에 의존해야지, 구체화에 의존하면 안된다. 의존성 주입은 이 원칙을 따르는 방법 중 하나다. 

[SOLID in Wikipedia](https://ko.wikipedia.org/wiki/SOLID_(%EA%B0%9D%EC%B2%B4_%EC%A7%80%ED%96%A5_%EC%84%A4%EA%B3%84))


### LSP  
치환성(substitutablility)은 객체 지향 프로그래밍의 원칙 중 하나이다.  
컴퓨터 프로그램에서 자료형 S가 자료형 T의 하위형이라면, 필요한 프로그램의 속성(정확성, 수행하는 업무 등)의 변경 없이 자료형 T의 객체를 자료형 S의 객체로 교체(치환)할 수 있어야 한다는 원칙이다. 리스코프 치환 원칙(Liskov substitution principle, LSP)은 바바라 리스코프가 __*자료 추상화와 계층(Data abstraction and hierarchy)*__ 이라는 제목으로 기조연설을 한 1987년 컨퍼런스에서 처음 소개한 내용으로, 이 원칙을 엄밀한 용어로 말하자면 __*(강한)행동적 하위형화*__ 라 부르는 하위형화 관계의 특정한 사례이다.  

리스코프의 __*행동적 하위형*__ 이라는 개념은 __*가변 객체*__ 의 치환성 이라는 개념을 정의한다. 즉 자료형 S가 자료형 T의 하위형이라면, 프로그램에서 자료형 T의 객체는 프로그램의 속성을 변경하지 않고 자료형 S의 객체로 교체할 수 있다.(예 [정확성](https://en.wikipedia.org/wiki/Correctness_(computer_science)))  

#### 전형적인 위반  
LSP를 위반하는 전형적인 예로, 너비와 높이의 조회(getter) 및 할당(setter) 메서드를 가진 직사각형 클래스로부터, 정사각형 클래스를 파생하는 경우를 들 수 있다. 정사각형 클래스는 항상 너비와 높이가 같다고 간주할 수 있다. 정사각형 객체가 직사각형을 다루는 문맥에서 사용되는 경우, 정사각형의 크기는 독립적으로 변경할 수 없기 때문에(혹은 그래서는 안되기 때문에) 예기치 못한 행동을 하게 된다. 이 문제는 고치기 쉽지 않다. 정사각형 클래스의 할당 메서드를 수정하여 정사각형의 불변 조건(즉, 너비와 높이가 같음)을 유지하면, 이 메서드는 크기를 독립적으로 변경할 수 있다고 설명한 직사각형의 할당자의 사후 조건을 무력화(위반)한다. 이러한 LSP 위반은 실전에서는 LSP를 위반한 클래스를 사용하는 코드가 실제로 기대하는 사후조건이나 불변 조건에 따라 문제가 될 수도 있고 아닐 수도 있다.  
여기서 중요한 사안은 가변성이다. 정사각형과 직사각형이 조회 메서드만 가진다면(즉, 이들이 불변 객체라면), LSP 위반을 발생하지 않는다.  

[LSP in Wikipedia](https://ko.wikipedia.org/wiki/%EB%A6%AC%EC%8A%A4%EC%BD%94%ED%94%84_%EC%B9%98%ED%99%98_%EC%9B%90%EC%B9%99)

### ISP  
인터페이스 분리 원칙은 클라이언트가 자신이 이용하지 않는 메서드에 의존하지 않아야 한다는 원칙이다. 인터페이스 분리 원칙은 큰 덩어리의 인터페이스들을 구체적이고 작은 단위들로 분리시킴으로써 클라이언트들이 꼭 필요한 메서드들만 이용할 수 있게 한다. 이와 같은 작은 단위들로 분리시킴으로써 클라이언트들이 꼭 필요한 메서드들만 이요할 수 있게한다. 이와 같은 작은 단위들을 역할 인터페이스라고도 부른다. 인터페이스 분리 원칙을 통해 시스템의 내부 의존성을 약화시켜 리팩토링, 수정, 재배포를 쉽게 할 수 있다.  
인터페이스 분리원칙은 SOLID 5원칙의 하나이며, GRASP의 밀착 원칙과 비슷하다.  

[ISP in Wikipedia](https://ko.wikipedia.org/wiki/%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4_%EB%B6%84%EB%A6%AC_%EC%9B%90%EC%B9%99)

### DIP  
객체 지향 프로그래밍에서 의존관계 역전 원칙은 소프트웨어 모듈들을 분리하는 특정 형식을 지칭한다. 이 원칙을 따르면, __*상위 계층(정책 결정)이 하위 계층(세부 사항)에 의존하는 전통적인 의존관계를 반전(역전)시킴으로써 상위 계층이 하위 계층의 구현으로부터 독립*__ 되게 할 수 있다. 이 원칙은 다음과 같은 내용을 담고 있다.  

**첫째,** 상위 모듈은 하위 모듈에 의존해서는 안된다.  
상위 모듈과 하위 모듈은 모두 추상화에 의존해야 한다.  

**둘째,** 추상화는 세부 사항에 의존해서는 안된다.  
세부사항이 추상화에 의존해야 한다.  

이 원칙은 __*상위와 하위 객체 모두가 동일한 추상화에 의존해야 한다.*__ 는  
객체 지향적 설계의 대원칙을 제공한다.  

[DIP in Wikipedia](https://ko.wikipedia.org/wiki/%EC%9D%98%EC%A1%B4%EA%B4%80%EA%B3%84_%EC%97%AD%EC%A0%84_%EC%9B%90%EC%B9%99)