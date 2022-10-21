---
title: About State less or ful
category: flutter
tags: flutter state
toc: true
toc_label: "Contents"
---

# State: less Or ful

State가 less 하냐 ful 하냐는 다음과 같은 컨셉트로 간단하게 설명할 수 있습니다.

- **Stateless: static**
- **Stateful: dynamic**

이 컨셉트는 이미 익숙하지만, 그만큼 중요하기도 합니다.
이런 생각을 해볼 수 있습니다.

*“Stateful 위젯이 dynamic하다면, 매번 Stateless 위젯에 다른 값을 주어 새로 렌더링하면 되는 것이 아닌가?”*

맞습니다. 두 위젯은 같은 것을 다른 방법으로 구현 할 수 있죠.

이에 대한 정답은 *“가능하면 Stateless 위젯을 사용하라”* 입니다.

*Stateful* 위젯은 위젯이 가지는 변수의 값이 변하면, 변한 후의 값이 변하기전의 값과 같은지 비교하고, 다르면 새로운 위젯을 빌드합니다.

*Stateless* 위젯은 주어진 파라미터를 받아 그냥 렌더링할 뿐입니다.

간단한 앱이라면, 몇개의 Stateful 위젯으로 해결될 수 있을지 모르지만, 비즈니스 로직이 복잡해지면 질수록 상태관리의 복잡도가 증가합니다. 

따라서 앱의 성능을 최적화하기 위해서는, 위젯 트리에서 꼭 필요한 부분만 *Stateful* 위젯으로 구성하고 나머지는 *Stateless* 위젯을 구성하는 것이 좋습니다.

그렇다면 꼭 *Stateful* 위젯이 필요한 경우는 어떤 경우일까요?
다음과 같은 경우가 있습니다.

- 위젯이 보여주는 것(사실은 위젯이 가지고 있는 state: temporary data)이 사용자의 입력에 따라 즉각 변화하고, 이 상태가 즉각 global state에 반영되지 않는 경우
- 위젯이 스스로 state를 변화시키며 사용자에게 다른 것을 보여주어야하고, 이 상태가 즉각 global state에 반영되지 않는 경우

일단 저는 이정도가 생각납니다.

더 많은 경우들이 있을 수 있지만, 일단은 위와 같은 상황을 잘 피해서 *Stateless* 위젯을 사용해 보도록 합시다.

# StatefulBuilder

만약 어떤 위젯 하위에 크기가 큰 Stateless 위젯과 크기가 작은 Stateful 위젯이 형제 사이로 있다고 생각해봅시다.
상태가 변해서 새로 빌드해야하는 것은 Stateful 위젯 뿐인데, state의 변화로 멤버 변수가 변화해서 빌드 코스트가 큰 Stateless 위젯까지 *build 함수*에서 새로 빌드해야하는 것은 비효율적입니다.

이 때, Stateful 위젯을 ***StatefulBuilder*** 위젯으로 감싸게 되면, *StatefulBuilder*의 builder 프로퍼티 함수가 가지는 **별도의 setState 파라미터 함수**를 Stateful 위젯에서 호출하는 것으로, 전체 위젯에서 Stateful한 부분만 새로 빌드되도록 최적화할 수 있습니다.

```dart
await showDialog<void>(
  context: context,
  builder: (BuildContext context) {
    int? selectedRadio = 0;
    return AlertDialog(
      content: StatefulBuilder(
        builder: (BuildContext context, StateSetter setState) {
          return Column(
            mainAxisSize: MainAxisSize.min,
            children: List<Widget>.generate(4, (int index) {
              return Radio<int>(
                value: index,
                groupValue: selectedRadio,
                onChanged: (int? value) {
                  setState(() => selectedRadio = value);
                },
              );
            }),
          );
        },
      ),
    );
  },
);
```

# 마치며

이번 시간에는 플러터의 중요한, Stateless, Stateful 위젯에 대해 알아보았습니다.
플러터는 모두 위젯으로 구성되어 있는 만큼, 언제나 어떤 위젯을 사용하는 것이 바른지를 생각하며 UI를 빌드해야겠습니다.