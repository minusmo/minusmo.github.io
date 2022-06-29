---
title: About Association, Composition, Aggregation
category: OOP
tags: designPattern
toc: true
toc_label: "Contents"
---

# Relation

연관은 객체를 통해 설정되는 두 개의 개별 클래스 간의 관계이다. 연관은 _일대일_, _일대다_, _다대일, 다대다_ 일 수 있습니다. 객체지향 프로그래밍에서 객체는 다른 객체와 통신하여 해당 객체가 제공하는 기능과 서비스를 사용합니다. **구성(Composition)** 과 **집계(Aggregation)** 은 연결의 두 가지 형태입니다.

포함관계는 다음과 같습니다.

Associtation > Aggregation > Composition

예를 들면,

```python
class Bank:
	# Bank stuff

class Employee:
	# Employee stuff

{
	bank: new Bank,
	employees: [Employee1, Employee2, ...],
}
```

위 예시에서, 은행과 직원은 직접적인 구현이나 사용 관계는 아니지만, 객체를 통해 두 클래스가 연결되는 관계를 가집니다. 하나의 은행에는 다수의 직원이 있을 수 있으므로, 이는 **일대다** 관계입니다.

연관은 **방향성**이 있습니다. 그리고 **독립적** 입니다. 위와 같이 은행에 직원은 속할 수 있지만, 직원에 은행이 속하는 것은 불가능합니다. 이를 **_Has-A_** 관계라고도 합니다.

또한 **집계** 에서, 두 클래스 모두 개별적으로 살아남을 수 있습니다. 하나의 엔터티가 종료되어도 다른 엔터티가 종속적으로 사라지지 않습니다.

# 집계 와 구성

## 1. 종속성(Dependency)

**_집계_** 는 **\***자식* 이 *부모\* 와 독립적으로 존재할 수 있는 관계를 의미합니다. 예를 들어 **Bank** 와 **Employee** 는 Bank를 삭제해도 Employee는 여전히 존재합니다. 반면에

**_구성_** 은 자식이 부모와 독립적으로 존재할 수 없는 관계를 의미합니다. 예를 들어, _인간_ 과 _심장_ 의 관계에서, 심장은 인간과 별개로 존재하지 않습니다.

## 2. 관계 유형

집계 관계는 **”has-a”** 관계이고,

구성 관계는 **”part-of”** 관계입니다.

## 3. 연관 유형

집계는 **강한** 연관이고,

구성은 **약한** 연관입니다.
