---
title: About ThemeData
category: flutter
tags: flutter theme
toc: true
toc_label: "Contents"
---


# Flutter - Theme을 잘 사용해 보자

지난번 해커톤에서 Theme을 모듈로 분리해서 사용해보려고 했지만, main.dart에서 다른 모듈로 분리하기만 했을 뿐 전혀 제대로 적용하지 못했다… 

다음에는 제대로 해보자!

# App Theme

어플리케이션에는 갖가지 색이 필요합니다.

당연히 그 색을 컬러 팔레트를 통해 앱 전체에 제공해야 통일감있는 좋은 앱 디자인이 되겠죠?

*flutter*의 *Material Design*은 이를 `ThemeData()`를 통해 가능하게 합니다.

앱의 루트 위젯 격인 *MaterialApp*의 생성자는 **`theme`**이란 **named parameter**를 받습니다. 이를 통해 루트 위젯에서 자손 위젯들로 테마 데이터를 전달할 수 있죠.

```dart
MaterialApp(
	title: "MyApp",
	theme: ThemeData(),
	home: Home(),
);
```

기본적으로 theme이 받는 인스턴스는 *light 모드*의 테마 데이터입니다.

시스템에서 light테마를 요구할 때 앱이 제공하는 테마 데이터이죠.

우리는 이것을 theme parameter에 `ThemeData.dark()`를 넘겨주고,

`darkTheme`이라는 **named parameter**에 테마 데이터를 넘겨주는 것으로 다크모드의 테마를 임의로 제공할 수 있습니다.

지금은 먼저 시스템이 light 를 요구한다고 생각하고 light 테마를 작성해봅시다.

## PrimaryColor

`primaryColor`는 앱이 가장 우선적으로 사용하는 색입니다. 이 색은 앱바에서 사용이 됩니다. 

`primayColor`가 지정되어 있으면, 앱바는 우선적으로 이 색을 사용합니다.

## PrimarySwatch

`primarySwatch`는 기준 색을 기본으로, 컬러 쉐이드를 만들어 흑백 단조 컬러 팔레트를 만들어줍니다.

`primarySwatch`가 지정되어 있으면, 앱에서 기본적으로 사용하는 색의 컬러 팔레트가 바뀌게 됩니다.

### PrimaryColor와 PrimarySwatch 동시에 사용하기

두 가지를 동시에 사용할 수도 있습니다.

그렇게되면, 앱바는 `PrimaryColor`를 사용하고, 나머지 위젯은 `PrimarySwatch`를 사용하게 됩니다.

### accentColor

`accentColor`는 강조색을 지정하는 것입니다. 이 값을 `ThemeData`에 넘겨주게 되면, `accentColor`가 지정이 되고, 이 색을 기본으로 사용하는 위젯(`floatingActionButton` etc)들은 기본 색이 바뀌게 됩니다.

## scaffoldBackgroundColor

`MaterialApp`에서 사용하는 `Scaffold` Widget의 배경색을 지정합니다. 

## textTheme

`textTheme`은 텍스트에 사용할 테마를 지정합니다. 

어떤 텍스트 종류에 어떤 `TextStyle`을 사용할지를 지정할 수 있습니다.

`textTheme`의 텍스트 컬러의 경우는 시스템 색이 dark로 설정이 되면 자동으로 반전을 시켜주니, 이를 고려하여 텍스트 색상을 지정할지 말지 결정해야합니다.

```dart
theme: ThemeData(
	primaryColor: Color(0xFF45D1FD),
	primarySwatch: Colors.green,
	accentColor: Colors.greenGrey,
	scaffoldBackgroundColor: Colors.black,
	textTheme: TextTheme(
		bodyText2: TextStyle(
			color: Colors.whte,
			),
		),
	)
```

## floatingActionButtonTheme, buttonTheme

플로팅 액션 버튼과 같은 특정한 위젯에서 사용하는 테마를 지정할 수도 있습니다. 

버튼 위젯에서 모두 사용하는 테마를 지정할 수도 있습니다.

# Theme

만약 자손 위젯을 `Theme` 위젯으로 감싸게 되면,  그 위젯에서만 사용하는 테마를 지정할 수 있습니다.

`Theme` 위젯은 `**data**` named parameter를 받는데, 여기에 `ThemeData`를 넘겨주면 됩니다. 그러면 그 위젯을 기준으로 하위 위젯 트리에서는 새로운 테마를 사용하게 됩니다.

## Theme.of(context)

자손 위젯에서 앱 테마 데이터를 사용하고 싶다면, `Theme.of(context)` method를 사용해서 `context`의 테마를 사용하면 됩니다.

# 마치며

이번에는 이렇게 매우 간단하지만, 앱 테마를 사용하는 기본을 알아보았습니다.

앱 테마를 사용하면 앱을 구성하는 위젯에서 사용하는 여러가지 색을 일일이 지정하지 않고 `ThemeData`에서 일괄적으로 적용할 수 있어, **더 이해하기 쉬운 코드**, **재사용하기 쉬운 코드**, **독립적으로 컴파일 가능한 코드**를 제공합니다.(모듈로 분리할 경우)

Reference  
[Everything About Flutter Themes in Less Than 10 minutes](https://www.youtube.com/watch?v=9iQiVUmLXyI&ab_channel=FlutterMentor)