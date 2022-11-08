---
title: About Compile && Runtime Constant
category: compilation
tags: programmingLanguage variable
toc: true
toc_label: "Contents"
---

컴파일 언어에는 크게 두가지 상태가 있습니다.
컴파일 타임과 런 타임이죠. 
컴파일 타임은 말 그대로 코드를 컴파일 하는 시간을 말하는 것이고,
런 타임은 그 코드가 실제 실행되는 시간을 말하는 것이죠.

우리는 흔히 **“변수”** 를 사용합니다. 이 변수는 말 그대로, **“변하는”** 값입니다. 그런데, 프로그램을 보다 예측 가능하고, 안정적으로 만들기 위해서는 이 변수를 잘 통제할 필요가 있습니다. 그러기 위해서 우리는 종종 이 “변수”를 **“상수”** 로 선언하기도 합니다. 그런데 이 “상수”에도 종류가 여러가지 있습니다. 프로그래밍 언어마다 다르기는 하지만요. 😄

오늘은 딱 2가지 분류로 이 “상수”를 알아보겠습니다.

# 런타임 상수

이 상수는, 그 값이 소**스 코드를 실행하는 도중에만 알 수 있거나, 계산되는** 상수를 말합니다. 
런타임 상수는 컴파일 타임 상수보다 조금 느립니다. 하지만 컴파일 상수보다 조금 더 유연합니다. 그러나 역시 한번 초기화되면, 그 값은 변하지 않습니다. 런타임 상수의 사용 예는 다음과 같습니다.

```cpp
int main()
{
    // Input a variable
    double electonmass;
    cin >> electonmass;
  
    // Define a constant
    // and initialize it at
    // run-time
    const double electon_mass{ electonmass };
  
    // Known to the compiler
    // at the run-time
    cout << electon_mass << endl;
  
    return 0;
}
```

# 컴파일 타임 상수

이 상수는, **그 값이 컴파일 타임에 알 수 있거나, 계산되는** 상수를 말합니다. 컴파일 타임 상수는 런타임 상수보다 빠르지만, 덜 유연합니다. 컴파일 타임 상수의 사용 예시는 다음과 같습니다.

```cpp
int main()
{
    // Declare and initialize
    // compile time constant
    const double electron_q{ 1.6e-19 };
  
    // Value known to compiler
    // at compile-time
    cout << electron_q << endl;
  
    return 0;
}
```

# 런타임 상수와 컴파일 타임 상수의 비교

| 런타임 상수 | 컴파일 타임 상수 |
| --- | --- |
| 런타임에만 값이 계산되거나, 알 수 있습니다. | 컴파일 타임에 값이 계산됩니다. |
| 런타임 상수는 소스코드가 실행될 때마다 다른 값을 가질 수 있습니다. | 컴파일 타임 상수는 소스코드가 실핼될 때마다 항상 같은 값을 가집니다. |
| 런타임 상수가 열거형을 초기화하는데 사용되면, 컴파일 에러를 발생 시킵니다. | 컴파일 타임 상수로 열거형을 초기화하면, 컴파일 에러를 발생시키지 않습니다. |

# 마치며

이번 글에서는 런타임 상수와 컴파일 타임 상수의 차이를 알아보았습니다. 사실, 이름에서도 어느정도 어떤 차이가 있는지 추측할 수 있지만, 그보다 명시적으로 어떤 차이가 있는 변수들인지 한번 알아두면, 나중에 헷갈릴일이 없겠죠?? 😄

[Runtime and Compile-time constants in C++ - GeeksforGeeks](https://www.geeksforgeeks.org/runtime-and-compile-time-constants-in-c/)