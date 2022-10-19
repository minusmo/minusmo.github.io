---
title: About Stack && Positioned
category: flutter
tags: design flutter layout
toc: true
toc_label: "Contents"
---

# Stack & Positioned

위젯을 항상 나란히 배치할 수는 없습니다.
때로는 겹쳐진 위젯을 보여주고 싶을 수도 있고,
때로는 정해진 위치에서 벗어나도록 의도해서 보여주고 싶을 수도 있습니다.

바로 그럴 때 어떻게 위젯을 위치시키는지, 알아봅시다.

# Stack

Stack 위젯으로 층층이 쌓고 싶은 여러 자식 위젯들을 감싸게 되면, 자식 위젯들은 인덱스 순서대로 맨아래에서 위로 차곡차곡 쌓이게 됩니다.

이 때 자식 위젯들은 기본적으로 *start(top left)* 위치에 포지셔닝됩니다.

이 위치 기준을 바꾸고 싶다면, *alignment* property에 ***AlignmentDirectional*** 값을 지정해주면 됩니다.

# Positioned

하지만 이것으로는 부족합니다.

우리는 자식 위젯들이 모두 같은 곳을 기준으로 정렬되어 있기를 항상 바라지는 않습니다.

때로는 그들 중 일부는 특별한 위치에 있으면 좋겠다고 생각할 때도 있습니다.

바로 이 때, 바로 그런 위젯을 Positioned 위젯으로 감싸주면 됩니다. 그리고 위젯의 위치(상하좌우)와 크기(가로세로)를 지정해주면 그 위젯을 원하는 곳에 원하는 크기로 위치시킬 수 있습니다.

하지만 이 위치 지정 방법은, 마치 *CSS의 position: absolute*와 같아서, Stack 위젯을 Positioned 위젯이 벗어나기도 합니다. 이럴 때는,

## overflow

값을 Stack 위젯에 지정해주면, Positioned 위젯이 Stack을 벗어날 때, *접혀보일 것인지(clipped)*, *그대로 보일 것인지(visible)*를 지정할 수 있습니다.

Stack 위젯의 자식들은 모두 각자의 크기와 위치가 있습니다.
그리고 Positioned 되지 않은 위젯들은 모두 최대 Stack 위젯의 높이와, 너비를 넘어서지 못합니다. 바로 이 높이와 너비는 Stack 위젯의 부모 위젯으로부터 상속받는 것이죠.

# StackFit

Stack의 자식 위젯들 중에 Positioned되지 않은 것들로 Stack 위젯을 꽉 채우고 싶을 때가 있습니다. 이럴 때는 StackFit 속성을 Stack에 지정해주면, Positioned되지 않은 위젯들이 Stack 위젯을 전부 채우게 됩니다. 이 때 Positioned되지 않은 위젯에는 Positioned 위젯으로 감싸져 있지만, 위치, 크기가 지정되지 않은 위젯도 포함됩니다.

# Standalone Stack

단독으로 사용되는 Stack 위젯은, 부모 위젯의 교차축을 전부 차지하는 크기를 가지게됩니다. 그리고 주축으로는 자식 위젯들 중 가장 큰 위젯의 주축 방향 크기를 가지게 됩니다. 말이 좀 어렵지만, 다음과 같은 경우에,

```
body: Container (
	height: ...,
	width: ...,
	child: Center(
		child: Stack(
			...
		),
	),
)
```

다음과 같은 모습을 가지게 된다는 말입니다.

![Standalone Stack](/assets/images/stack_and_positioned.png)


# 마치며

오늘은 위젯을 어떻게 층층이 쌓는지, 또 어떻게 자유롭게 원하는 위치에 보여지게 하는지를 알아보았습니다.

창의적인 UI/UX를 고민하다 보면, 기존의 방식에서 조금은 탈피하고 싶을 때가 있습니다. 그럴 때 이러한 방법을 통해 좁은 공간을 좀 더 유연하게 사용하는 방법을 택하는 것도 좋아보입니다.

[Reference](https://www.youtube.com/watch?v=81jLSAqQIY0&ab_channel=FlutterMentor)