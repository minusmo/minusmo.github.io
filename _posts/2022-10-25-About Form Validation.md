---
title: About Form Validation
category: flutter
tags: flutter widget form validation
toc: true
toc_label: "Contents"
---

form을 만들었다면, 당연히 폼에 적절한 입력이 들어왔는지를 검증해야합니다.
오늘은 폼의 입력값을 어떻게 검증하는지 알아보겠습니다.

# Form

**Form** 위젯으로 우리가 원하는 일련의 **FormField**들을 감싸줍니다.
그리고 먼저, Form 위젯에 *글로벌 키* 를 프로퍼티로 넣어줍니다.

지난번에 우리가 알아보았듯이, 글로벌 키는 특정 위젯에 마치 글로벌 변수처럼 작용해서, 동일한 레벨의 위젯과 상태를 공유하지 않고 앱 어디서든 값을 참조할 수 있습니다.  
글로벌 키는 다음과 같은 방법으로 생성할 수 있습니다.

```dart
final GlobalKey<FormState> _formKey = GlobalKey<FormState>();
```

# Validator

**FormField**에서는 **validator** 프로퍼티를 가지게됩니다. 이 프로퍼티는 함수를 하나 받습니다.
이 함수는 유저가 입력한 값(value)를 받아서 적절하게 검증하기 위한 함수입니다.
validator의 리턴 값은 ***null || string*** 입니다. 

만약 입력값을 검증했는데 유효하다면 null을 반환하고, 

아니라면 적절한 에러 메시지(string)을 반환합니다.

이 에러 메시지는 만약 입력값이 유효하지 않을 경우, FormField의 하단에 나타나게 됩니다.

```dart
validator: (value) {
	if (formValidator.isValid(value)) {
		return null;
	}
	else {
		return "Something went Wrong!!!";
}
```

# FormState.validate()

우리는 처음에 생성했던 글로벌 키를 이용해서 폼의 상태에 접근한 후, **validate() 메소드**를 이용해서 폼이 유효한지를 검증할 수 있습니다.

validate 메소드가 호출되면, FormState는 **폼 안에 있는 각각의 필드에 대해 validator() 메소드를 호출**합니다.  
만약 **모든 필드가 유효하다면, validate 메소드는 true를 반환**하고, 아니면 false를 반환합니다. 그리고, **만약 어떠한 필드라도 유효하지 않으면, 폼을 다시 빌드하고, 에러 메시지를 보여줍니다.**

# 마치며

이번 시간에는 폼을 어떻게 검증하는 지를 알아보았습니다.
여기서 알아본 것은 매우 간단한 검증에 불과합니다. 더 나아가서, 입력값에 더 위험한 상황을 초래할 만한 우려는 없는지에 대한 검증과 보안 설계가 필요하겠습니다.

[Build a form with validation](https://docs.flutter.dev/cookbook/forms/validation)

[Flutter - How To Validate A Form (TextFormField Validation)](https://www.youtube.com/watch?v=NF7paH7toGk&t=69s&ab_channel=FlutterMentor)