---
title: About Device Orientation
category: flutter
tags: flutter widget orientation device
toc: true
toc_label: "Contents"
---

모바일 디바이스는 가로, 세로로 변합니다. 오늘은, 이 디바이스의 방향을 다루는 법을 알아봅시다.

의외로 간단합니다.

애플리케이션의 메인함수에서, `runApp(MyApp)` 을 호출하기 전에, 시스템을 설정하는 함수를 호출하면됩니다.

두 가지의 함수를 말입니다.

1. `WidgetsFlutterBinding.ensureInitialized()`
2. `SystemChrome.setPreferredOrientations()`

# WidgetsFlutterBinding.ensureInitialized

이 메소드를 호출하면 되는데… 뭘까요 이건??

먼저 `BindngBase` Class 를 알아봅시다.

이 클래스는 **Flutter foundation doc**에서 찾아볼 수 있습니다. 
우리가 보통 위젯을 생성할 때 사용하는 API는 굉장히 높은 레벨의 API입니다. 시스템과 밀접하지 않다는 말입니다. 그런데 기기의 방향과 같은 시스템 센서 정보는 상대적을 훨씬 낮은 레벨의 API로 제어됩니다. 이를 해결하기 위해 `BindingBase` 클래스가 있습니다. 
공식 문서에는 다음과 같이 설명되어 있습니다.

***“싱글턴 서비스들을 제공하는 [믹스인](https://en.wikipedia.org/wiki/Mixin)들을 위한 베이스 클래스”***

- **믹스인이란?**
    
    여러가지 클래스에서 *공통으로 사용하고 싶은 인터페이스*가 있을 때, 이것을 직접 상속하지 않고 믹스인이라는 클래스에 가두어, 여러 클래스와 **섞어서**, 공통된 인터페이스를 사용할 수 있게하는 프로그래밍 방법입니다.
    
    일종의 ***약한 인터페이스***, 혹은 ***폴리모피즘*** 의 형태라고 볼 수도 있습니다.
    
    믹스인에대한 자세한 예시는 [다음글](https://javascript.info/mixins)을 참고하면 좋습니다.
    

꽤 중요하고 어려운 말들의 집합이지만, 다시 말하면 다음과 같습니다.

앱에서 필요한 *싱글턴 서비스*들이 있겠죠? 그 서비스들을 사용하기위해 인터페이스를 노출시켜야하는데, 이 인터페이스가 **믹스인 클래스** 에 캡슐화 되어 있습니다.(여러 싱글턴 서비스들에 공통된 인터페이스가 좀 있는가 봅니다.)  
바로 이 믹스인 클래스도 여러 형태가 있을텐데, 이 믹스인 클래스가 상속받는 클래스가 바로이 `BindingBase` 클래스인 겁니다.

다시 플러터로 좀 돌아가면, *플러터 엔진(dart:ui)은* 몇몇 low-level 서비스들을 노출하는데, 이것들은 보통 플러터 프로그래머가 직접 사용하기에 적합하지 않습니다. 

`Binding`들은 이런 저수준 API들과 고수준 프레임워크 API들이 잘 메시지를 주고받게끔 붙여주는 역할을 합니다.

`WidgetsFlutterBinding`은 그래서 `BindingBase` 클래스를 상속받는 일종의 바인딩 클래스인 것이고, 이 클래스의 **ensureInitialized** 인터페이스를 호출하면 플러터 위젯 프레임워크와 저수준 시스템 API가 잘 통신하게 됩니다.

돌고돌아 `WidgetsFlutterBinding.ensureInitialized()`가 결국 무엇이냐 하면, 방금 위에서 말한 low-level API와 high-level API가 잘 묶이도록 보장해주는 함수라고 이해할 수 있겠습니다.

# SystemChrome.setPreferredOrientations

`SystemChrome` 클래스는 운영체제의 그래픽 인터페이스의 모양,방향과 그것이 어떻게 어플리케이션과 상호작용하는지를 제어합니다.

이 클래스의 `setPreferredOrientations`라는정적 메소드를 호출하게됩니다.

이 메소드는 `List<DeviceOrientation>` 를 파라미터로 받는데요, 이 리스트에 우리가 선호하는 디바이스의 방향을 아이템으로 넣어주면 됩니다. 다음과 같이요.

```dart
SystemChrome.setPreferredOrientaitons([
	DeviceOrientation.portraitUp,
	DeviceOrientation.portraitDown,
]);
```

이게 다 입니다!! 😊

# 마치며

이번 글에서는 디바이스의 방향을 어떻게 제어하는지를 알아보았습니다.

사실 제어 설정 자체는 어렵지 않은데, 설정할 때 호출하는 함수는 어떤 함수인지, 왜 호출해야하는지, 무엇을 위한 클래스인지를 아는 과정이 더 어려웠습니다. 하지만, 절대 피해가면 안되는 과정이라고 생각합니다.

[Flutter - Control Device Orientation (Disable Landscape Mode)](https://www.youtube.com/watch?v=qQhvdmNhBfE&t=110s&ab_channel=FlutterMentor)

[WidgetsFlutterBinding class - widgets library - Dart API](https://api.flutter.dev/flutter/widgets/WidgetsFlutterBinding-class.html)