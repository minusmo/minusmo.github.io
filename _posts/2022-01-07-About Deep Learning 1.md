---
title: About Deep Learning 1
category: DeepLearning
tags: AI DeepLearning NeuralNetworks
toc: true
toc_label: "Contents"
---

# 딥러닝의 기본 개념 1  
[Neural Networks by 3Blue1Brown](https://youtube.com/playlist?list=PLZHQObOWTQDNU6R1_67000Dx_ZCJB-3pi)

## Neural Networks
**신경망** 이라는 단어의 유래는 인간의 뇌이다.  
인간의 뇌는 뉴런이라는 신경세포로 이루어져있다. 바로 이 뉴런을 통해 인간의 뇌는 새로운 
정보를 학습하고 사고한다. 이러한 개념을 컴퓨터 과학에 적용한 것이 바로 딥러닝의 골자가 되는 인공 신경망이다.  

**딥러닝** 이라는 추상적인 말을 사용하지만, 사실은 딥러닝도 결국에는 특정 입력을 받아서
특정 출력을 반환하는 함수일 뿐이다. 다만 우리가 얻고자 하는 결과와 함수의 출력 간의 오차를 어떻게 하면 줄일 수 있을까에 대한 많은 고찰의 결과라는 것이 차이인 것이다.  

가장 단순한 예를 살펴보자.  
**인공 신경망** 에 있어서의 ___Hello World___ 같은 이른바 **"숫자 판별 문제"** 이다.  
우리가 사람의 손으로 종이 위에 쓰여진 수천개의 숫자들의 사진이 있다고 해보자.  
만약 사람의 두뇌라면 어떻게 학습할까??  

시각으로 전해진 정보가 뉴런으로 전달 되고, 이 뉴런이 또 다른 뉴런을 자극(활성화)한다.
처음에는 단순히 서로 다른 정보의 집합일 뿐이었던 것이, 위의 과정을 수없이 거쳐 추상화와 정보의 정제를 통한 개체의 인식이 완성되는 것이다.  

![Neural Networks](/assets/images/NN.jpeg)

위 그림처럼 입력이 1차원 배열이라고 생각해보자.  
이는 사람의 뇌에서 처음 정보를 전달 받는 뉴런의 역할을 한다.  
이 뉴런들이 다음 n개의 뉴런을 활성화 시켜야한다.  
그런데 어떤 기준으로 어떻게 활성화 할것인가? 

**hidden layer 1** 의 뉴런들이 입력된 정보들 중 각각 일부를 담당하여 처리하는 뉴런들이라 생각해보자. 예를 들면, hidden layer 1의 첫 번째 뉴런은 하나의 숫자 전체를 
n개로 나누었을 때 첫번째, 마찬가지로 두 번째 뉴런은 그 n개 중의 두 번째, 이렇게 말이다.  

그렇다면 각 뉴런이 처리해야 하는 정보가 모두 다르므로, 같은 정보를 입력받았다고 해서
그 정보를 모두 같은 중요도로 처리해서는 안된다고 생각해 볼 수 있다.  

그래서 우리는 뉴런과 뉴런을 잇는 __*신경망*__ 을 정의한다. 위 그림과 같이, 각 층의 
뉴런들과 다음 층의 각 뉴런들은 모두 __*신경망*__ 으로 연결되어 있다. 이 신경망들은 입력층과 같은 크기와 모양의 __*가중치*__ 들의 집합인데, 한 층의 각 뉴런마다 __*가중치(중요도)*__ 가 달라야 하므로 입력층의 모든 뉴런들과 다음층의 하나의 뉴런을 잇는 가중치들의 집합은, 다음층의 뉴런들 마다 개별적으로 모두 다르다.  

이 가중치(weight)들과 입력층의 뉴런마다 가진 실수값들을 __*점곱(dot product)*__ 해서 다음층으로 전달하게 된다.  

그런데 이 때, 상황에 따라서 뉴런이 활성화되어야 하는 조건이 다르므로,  
이를 반영하기 위해 __*역치(Bias)*__ 를 도입한다.  

![Neural Networks calculation](/assets/images/NN2.png)

역치(bias)값이 중요한 이유는 바로 인공 신경망의 기본 이론에서 찾아볼 수 있다.  
뉴런이 다른 뉴런으로 부터 활성화 되는 것은 무조건적으로 이루어지지 않는다.  

다른 뉴런으로부터 전달받은 정보(자극)이 일정 수치가 넘어가야 뉴런이 활성화 되는 것이다.  
이를 도입한 것이 인공 신경망 초기의 __*Sigmoid*__ 함수이다.  
신경망으로부터 전달 받은 값들을 정규화하기 위해, 이 값들을 __*Sigmoid*__ 함수에 넣으면
뉴런이 활성화되는 정도를 0과 1사이의 수치로 얻을 수 있다.  

Sigmoid 함수에서는 0 주변에서 함수값(뉴런의 활성화 정도)가 급격하게 증가하는데,
이런 일반적인 상황에 대응하지 않는 뉴런도 있을 수 있다.  

그렇기 때문에 역치(bias)를 도입하게 된 것이다.  

최근에는 __*ReLU*__ 함수를 많이 사용하는데, 이는 뉴런의 학습 방법을 더 정확히 반영한 것이다. ReLU 함수는 Sigmoid 함수처럼 함수값이 부드럽게 증가하지 않는다.  

![ReLU function](/assets/images/NN4.jpeg)

특정값 이후부터 함수값이 일정한 기울기로 증가하게 되는데,  
이러한 모습이 실제 뉴런이 활성화 되는 방식과 유사하다고 한다.  

더 중요한 것은,  
#### 실제로 ReLU를 도입한 결과가 더 좋게 나타났다는 것이다.  
결과론적인 이야기이지만, 참 놀라운 결과가 아닐 수 없다.  

이러한 층과 층사이의 연결은, 뉴런의 개수가 늘어날 수록, 층의 개수가 늘어날 수록 
기하 급수적으로 증가하게 된다. 이런 과정을 거쳐 우리가 원하는 m개의 출력값을 최종적으로
얻게되는 것이다.  

하지만 딥러닝을 사용할 때, 우리는 이런 가중치와 역치 등의 값을 모두 일일이 
설정해주지 않는다. 그렇다고 처음 학습한 것 만으로 정확한 출력을 내는 것도 아닐 것이다.  

딥러닝 모델은 어떻게 입력 데이터를 주는 것만으로 정답에 가까운 결과를 내는 법을 
배우는 것일까?? 

#### 이는 다음에 함께 알아보도록 하자.  
