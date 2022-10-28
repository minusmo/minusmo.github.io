---
title: About ListView and More
category: flutter
tags: flutter widget ListView
toc: true
toc_label: "Contents"
---

# ListView

기본적으로 `ListView`는 적은 수의 아이템을 나열하기 위해 사용됩니다.
왜냐하면, 리스트 뷰는 한번에 모든 아이템을 렌더링하는데, 아이템의 수가 많으면 많을 수록 실제로 화면에는 보이지 않지만 렌더링은 되어야하는, *불필요한* 렌더링이 많아지게 되는 것이죠.

ListView는 무한대의 높이를 가지기를 원하기 때문에, 이를 `Column`과 같은 위젯에서 사용하기를 원한다면, `Expanded`나 `Flexible` 위젯으로 감싸야합니다.

# ListView.builder

ListView.builder는 *lazy-loading*을 통해 위의 문제를 해결합니다. 화면을 스크롤해서 위젯이 화면안으로 들어왔을 때 렌더링을하고, 그렇지 않으면 렌더링을하지 않는 방법으로 더 효율적인 렌더링 방식을 제공합니다.

`ListView.builder` 위젯은 `itemBuilder` 프로퍼티로 함수를 받습니다. 이 함수는 다음과 같습니다.

```dart
itemBuilder: (listViewContext, index) {
	return widgetForEachItem;
}
```

그리고 `itemCount` 라는 프로퍼티도 받습니다.   
이 프로퍼티는 아이템을 리스트에 몇개나 렌더링할지를 정해줍니다. 
이 값이 정해지지 않았다면, 리스트는 무한대의 아이템을 렌더링합니다.

그런데 `ListView.builder`는 각각의 아이템을 렌더링할 위젯을 반환하는 함수를 ItemBuilder에서 받을 뿐이지, 이값이 다른 외부값에 종속적이지는 않습니다. 따라서 서로 다른 아이템을 이 방법으로 렌더링하기 위해서는, 아이템들이 `index` 에 종속적이어야합니다.(인덱스에 따라 변한다는 말입니다.)

결국 `ListView.builder`로 빌드하는 아이템은 다음의 두 경우라는 말입니다.

- index에 순수하게 종속되어서 변하는 위젯의 경우
- index로 접근가능한 외부의 데이터 컬렉션의 index 위치의 아이템에 종속적인 위젯의 경우

# 마치며

이번 시간에는 아이템들의 리스트를 렌더링하고 싶을 때 어떤 위젯을 어떻게 사용하면 되는지를 알아보았습니다.
이보다 유용할 수는 없겠죠? 결국 우리는 언젠가 어디선가는 무언가의 컬렉션을 렌더링해야할 수 밖에 없을테니 말입니다.

[Flutter - ListView & ListView.builder Explained (+ How To Use It)](https://www.youtube.com/watch?v=QH0AFxI0Ejg&ab_channel=FlutterMentor)

[ListView class - widgets library - Dart API](https://api.flutter.dev/flutter/widgets/ListView-class.html)