---
title: About MediaQuery
category: flutter
tags: adaptiveDesign flutter layout
toc: true
toc_label: "Contents"
---

# MediaQuery

**MediaQuery**는 여러가지 디바이스의 뷰포트 크기에 대한 쿼리입니다.

이것을 활용해서, 다양한 기기의 뷰포트에 대응하도록 위젯의 크기를 설정할 수 있습니다.

# MediaQuery.of(context)

를 이용해서 해당 컨텍스트의 미디어쿼리를 참조하고, 이 미디어 쿼리의 *높이, 너비* 프로퍼티를 이용해서 위젯이 렌더링되는 컨텍스트의 뷰포트 크기에 대한 정보를 얻을 수 있습니다.

*MediaQuery.of(context)* 가 반환하는 값은 *MediaQueryData* 객체입니다. 

```dart
final MediaQueryData mediaQueryData = MediaQuery.of(context); 
```

이 *MediaQueryData* 객체는 3가지의 중요한 속성을 갖고 있습니다.

바로 ***viewInsets, padding, viewPadding*** 입니다. 하나씩 어떤 것인지 알아봅시다.

## viewInsets

공식 문서에는 다음과 같이 적혀있습니다.
*”시스템 UI가 차지해 버리는 디스플레이의 부분들은, 주로 기기의 키보드가 차지한다”*

다시말해 viewInsets 가 가지는 값은, 시스템 UI가 완전히 차지하는 공간의 크기이고, 
이것은 키보드가 차지하는 공간의 크기와 같습니다.

## padding

패딩에 대해서는 다음과 같이 적혀있죠.

*“시스템 UI가 차지해 버리는 디스플레이의 부분들은, 주로 하드웨어 디스플레이 노치 이거나, 시스템 상태 바 입니다.”*

## viewPadding

*“시스템 UI가 차지해 버리는 디스플레이의 부분들은, 주로 하드웨어 디스플레이 노치 이거나, 시스템 상태 바 입니다.”*

패딩과 설명이 똑같네요? 그렇다면 패딩과 뷰 패딩은 어떤 차이가 있을까요??

이 차이는 바로 **“키보드”** 와 **“시스템”** 에 있습니다.

패딩은 기본적으로 시스템이 유용한 목적이 아닌, 꼭 필요해서 어쩔 수 없이 차지하는 부분을 말합니다.
그래서 바로 **“노치”** 와 **“상태바”** 혹은 ios의 경우에는 **“하단 제어 바”** 가 이런 부분에 해당합니다. 시스템적으로 꼭 필요하지만, 사용자에게는 그다지 의미가 없죠. 메인 컨텐츠가 보여지는 부분이 아니니까요.

하지만 **“키보드”** 가 나타난다면 어떻게 될까요?

키보드는 사용자와 메인 인터랙션을 하는 중요 시스템 UI입니다. 그래서 키보드가 나타나면, 기존에 차지했던 유용하지 못한 공간의 패딩값은 0이 되고,(padding.bottom)

**viewInset.bottom** 값이 키보드의 크기만큼 증가합니다.

그래서 만약에 패딩(아래)의 값만을 가지고 레이아웃을 조정했다면, 키보드가 나타나는 순간 모든 레이아웃이 조금 아래로 내려가게 됩니다. **padding.bottom == 0** 가 되기 때문이죠.

바로 여기서, 패딩과 뷰패딩의 차이가 나타납니다.

키보드가 나타나도, 뷰패딩은 키보드가 없던 때의 패딩값을 기억합니다.

키보드가 있을 때, **(padding.bottom == 0 && viewPadding ≠ 0) == true** 라는 것이죠. 🙂 

# SafeArea

로 위젯을 감싸게 되면, 패딩, 뷰패딩, 뷰인셋의 값이 모두 0가 됩니다.(키보드가 없을 때)

하지만 키보드가 나타나면, 역시 뷰패딩과 뷰인셋의 값은 0이 아니게 됩니다.

# 마치며

이번 시간에는 미디어 쿼리란 무엇인지, 어떻게 사용하는지, 그리고 자주 마주치는 “키보드”에 어떻게 대처하는지에 대한 내용을 알아보았습니다. 이제는 “키보드”에 당황하지 말고, 의연하게 대처해야겠습니다.

## References

[https://www.youtube.com/watch?v=ceCo8U0XHqw&ab_channel=Flutter](https://www.youtube.com/watch?v=ceCo8U0XHqw&ab_channel=Flutter)

[MediaQueryData class - widgets library - Dart API](https://api.flutter.dev/flutter/widgets/MediaQueryData-class.html)