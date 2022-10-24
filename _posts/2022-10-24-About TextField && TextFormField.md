---
title: About TextField && TextFormField
category: flutter
tags: flutter widget form
toc: true
toc_label: "Contents"
---

# Text(Form)Field

플러터에는 텍스트를 위한 입력 필드가 두 가지 있습니다.

- **TextField**
- **TextFormField**

입니다. 
두 가지는 아주 약간의 차이가 있는데요,
*TextField*는 아주 일반적인 목적의 텍스트(문자열)을 입력받는 필드이고,
*TextFormField*는 폼에 입력을 받아 어딘가로 전송을 하거나, 정보를 저장하기 위해 *Validation*을 해야하는 경우에 사용합니다.

이 입력 필드에는 여러가지 장식을 해줄 수 있습니다.
바로, *Decoration* 입니다.

# Decoration

*Decoration*은, 위젯을 어떻게 꾸미는가를 지정하는 객체로, 입력을 장식하기 위한 위젯은 
*InputDecoration*이 있습니다.  

*InputDecoration*은 다음과 같은 프로퍼티를 가집니다.

- filled
- fillColor
- icon
- border
- hintText
- hintStyle
- etc…

# Getting value

텍스트 필드 위젯을 빌드했다면, 이 위젯을 통해 사용자가 입력하는 값을 가져올 수 있어야겠죠??  
이를 위해서 *onChanged* 콜백이 있습니다. **value**를 파라미터로 받는 이 콜백을 *onChanged* 프로퍼티에 넘겨주면, 텍스트필드의 값을 가지고 우리가 원하는 작업을 처리할 수 있습니다.

```dart
onchanged: (value) {
	currentValue = value;
}
```

# Refactoring Decoration

Decoration을 여러 위젯에 적용하고 싶다면, 일일이 지정해 줄 수도 있습니다만, 비슷한 Decoration을 비슷한 위젯에 적용하는데 위젯마다 일일이 비슷한 프로퍼티를 가지는 새로운 객체를 생성해 넣어주는 것은 극히 비효율적입니다.  
**이는 Decoration 객체를 하나 생성하고, copyWith 인터페이스를 통해 변경하고 싶은 부분만 변경하여 새로운 객체를 생성하는 패턴**으로 극복할 수 있습니다. 이는 마치 앱에 공통된 **ThemeData**를 사용하고, 이를 변주하여 위젯마다 다르게 테마를 부여하는 것과 비슷한 맥락입니다.

```dart
decoration: textFieldDecoration.copyWith(
	hintText: "write your name here",
	icon: Icon(Icons.person),
),
```

# 마치며

이번에는 텍스트의 입력이 필요할 때, 텍스트 필드와 텍스트 폼 필드를 어떻게 사용하는지, 그리고 어떻게 장식하는지를 알아보았습니다. 사용자의 입력을 적절한 위젯으로, 적절한 UI로 받아봅시다.

[Flutter - Applying Same Decoration To Multiple Widgets (.copyWith)](https://www.youtube.com/watch?v=r1imQrumtuo&ab_channel=FlutterMentor)

[Flutter - TextField and TextFormField (Text Input Widgets) - Part 1/2: Decoration and Styling](https://www.youtube.com/watch?v=_u72QgwsSq0)