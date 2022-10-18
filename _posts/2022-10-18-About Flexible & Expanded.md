---
title: About Flexible and Expanded
category: flutter
tags: flutter layout
toc: true
toc_label: "Contents"
---

# Flexible & Expanded

위젯을 Container로 감싸게 되면 mainAxis(주축)를 차지하는 크기는 Container의 자식 위젯의 크기(컨텐츠의 크기)에 비례합니다.

한 레이아웃에 여러 위젯을 배치할 때, 특정한 위젯이 남은 공간을 전부 다 차지하도록 만들고 싶을 때가 있습니다.

이러한 배치는 두 가지의 위젯을 통해 가능합니다.

- Flexible
- Expanded

# Flexible

Flexible 위젯은 *fit* 이라는 값을 매개변수로 받습니다.
이 값은 Flexible의 자식 위젯이 어떻게 주축에서 공간을 차지해야하는지를 알려줍니다. 

fit은 두 가지의 값을 갖는데 다음과 같습니다.

- FlexFit.loose
    - 이 값은 자식 위젯이 최대의 크기를 가지도록 조정합니다.
    - 따라서 만약 자식 위젯의 크기 값이 정해져 있다면, 그 값을 넘어서지 않습니다.
- FlexFit.tight
    - 이 값은 자식 위젯이 남은 모든 공간을 채우도록 강제합니다.

## Flexible 위젯 간의 크기

같은 주축에서 Flexible 위젯이 여러 개 있다면, 각 위젯이 서로 주축의 남은 공간에서 얼마만큼의 크기를 차지해야하는지를 알려줄 수 있습니다.

*flex* 파라미터에 정수 값을 주면, 십분위, 백분위로 남은 공간에서 자식 위젯이 얼마만큼의 공간을 차지해야하는지를 알려주고, 다른 Flexible 위젯과 상대적으로 크기를 조정합니다.

이를 통해 주축 상의 남은 공간에서 위젯이 어느정도의 크기로 보여야하는지를 통제할 수 있습니다.

# Expanded

Expanded 위젯도 *flex* 라는 값을 매개변수로 받습니다.

그리고 Flexible 위젯과 똑같이 행동합니다.

Expaneded 위젯은 Flexible 위젯 보다 조금 더 단순하게 작동하도록 의도된 위젯입니다.
fit: FlexFit.tight 이 지정된 상태로 이해하는게 편할 것 같습니다.

# 마치며

이번 글에서 다뤄본 주제는 생각보다 단순하면서도, 레이아웃을 지정할 때 흔하게 마주하는 문제입니다.

몇 몇 위젯에게 가져야만하는 크기를 지정하고, 나머지 공간을 모두 채우거나,

여러 위젯이 남은 공간 안에서 각각 상대적으로 얼마만큼의 크기를 가진채로 보여져야하는지 등의 상황이죠.

[Flexible class - widgets library - Dart API](https://api.flutter.dev/flutter/widgets/Flexible-class.html)

[Expanded class - widgets library - Dart API](https://api.flutter.dev/flutter/widgets/Expanded-class.html)

[Flutter - Flexible And Expanded Widgets Simply Explained For Beginners](https://www.youtube.com/watch?v=GS1YJ2KP_CQ&list=PLp5vKkBQLOGwwNUxkZ4v8YAv3OdyfMKvM&index=7&ab_channel=FlutterMentor)