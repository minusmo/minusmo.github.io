---
title: About Higher Order Components
category: React
tags: frontend React Patterns
toc: true
toc_label: "Contents"
---

이 글은 React docs의 Higher Order Components를 직접 번역, 요약한 글입니다.

# React

에서 고차 컴포넌트란, 
컴포넌트가 비슷한 로직을 공유하고 있을 때, 컴포넌트를 재사용하고, 중복을 제거하기 위해서 사용하는 소프트웨어 구성 패턴입니다.

비슷한 로직을 공유하는 컴포넌트들은, 
애플리케이션의 크기가 커질 수록 많아집니다. 

우리는 추상화를 통해서 공통된 로직을 하나의 공간에 분리하고, 여러개의 컴포넌트에서 공유합니다. 고차 컴포넌트가 하는 일이죠.

고차 컴포넌트는 입력받은 컴포넌트를 변경하지 않습니다. 상속을 사용하지도 않습니다.
고차 컴포넌트는 원래 컴포넌트를 컨테이너 컴포넌트로 감싸서 구성합니다.
`side-effect`가 전혀 없는 순수함수입니다.

감싸진(원래 컴포넌트)는 컨테이너 컴포넌트의 모든 `props`를 받고(데이터와 함께), 이 데이터를 이용해 출력을 렌더링합니다. 고차 컴포넌트는 데이터가 어떻게, 왜 쓰이는지는 고려하지 않습니다. 그리고 어디에서 왔는지도 고려하지 않습니다.

고차 컴포넌트는 평범한 함수이기 때문에, 원하는 만큼 인수를 추가할 수 있고, 원하는 만큼 `props`와 컴포넌트 생명주기 설정을 변경할 수 있습니다.

감싸는 컴포넌트와 감싸진 컴포넌트의 계약 관계는 철저히 **props-based**이기 때문에, 감싸진 컴포넌트에 같은 props를 전달하는 한, 쉽게 다른 컴포넌트로 교환이 가능합니다. 이러한 행위는 데이터 요청 라이브러리를 바꾸는 등의 상황에 유용합니다.

```jsx
// This function takes a component...
function withSubscription(WrappedComponent, selectData) {
  // ...and returns another component...
  return class extends React.Component {
    constructor(props) {
      super(props);
      this.handleChange = this.handleChange.bind(this);
      this.state = {
        data: selectData(DataSource, props)
      };
    }

    componentDidMount() {
      // ... that takes care of the subscription...
      DataSource.addChangeListener(this.handleChange);
    }

    componentWillUnmount() {
      DataSource.removeChangeListener(this.handleChange);
    }

    handleChange() {
      this.setState({
        data: selectData(DataSource, this.props)
      });
    }

    render() {
      // ... and renders the wrapped component with the fresh data!
      // Notice that we pass through any additional props
      return <WrappedComponent data={this.state.data} {...this.props} />;
    }
  };
}
```

# 원래 컴포넌트를 변경하지 말 것

원래 컴포넌트를 변경하는 고차 컴포넌트는 원래 컴포넌트를 다른 컴포넌트에서 재사용할 수 없게 만들 수 있습니다. 

특히나 ***프로토타입*** 을 변경해서는 안됩니다. 변경하는 고차 컴포넌트는 *결함이 생기기 쉬운 추상화* 입니다. 
어떻게 변경이 일어났는지 모른다면, 다른 고차 컴포넌트와 충돌이 발생할 수 있습니다.

컴포넌트를 변경하는 대신에, 컴포넌트를 감싸는 방식으로 새로운 기능을 추가하세요.

```jsx
function logProps(WrappedComponent) {
  return class extends React.Component {
    componentDidUpdate(prevProps) {
      console.log('Current props: ', this.props);
      console.log('Previous props: ', prevProps);
    }
    render() {
      // Wraps the input component in a container, without mutating it. Good!
      return <WrappedComponent {...this.props} />;
    }
  }
}
```

## 고차 컴포넌트와 컨테이너 컴포넌트

둘은 비슷하게 보입니다. 

**컨테이너 컴포넌트**는 고 수준과 저 수준 관심사 사이의 책임을 분리하는 전략입니다.
컨테이너들은 

- 구독과 상태와 같은 것들을 관리하고,
- UI를 렌더링하는 것과 같은 컴포넌트로 props를 전달합니다.

**고차 컴포넌트**는 컨테이너 컴포넌트를 구현의 일부로 사용합니다. 
고차 컴포넌트는 마치 파라미터가 잇는 컨테이너 컴포넌트 정의라고 생각할 수 있습니다.

# 기능의 확장과 제어

고차 컴포넌트는 원래 컴포넌트의 기능을 확장할 뿐만 아니라, 원래 컴포넌트에서 필요없는 기능을 제한하기도합니다. 예를 들면, 전달된 `props` 중에서 원하는 `prop`만 추출해서 전달할 수도 있고, 다른 로직이나 데이터와 결합한 새로운 `prop`을 만들어 전달할 수도 있습니다.

# 출력되는 이름

디버깅하기 쉽게 만들기 위해 컴포넌트에 `displayName`을 설정하세요.
리액트 개발자 도구에서는 `displayName`이 보입니다.

# 경고

고차 컴포넌트를 사용할 때 지켜야할 것들이 몇가지 있습니다.

## 고차 컴포넌트를 render 함수 안에서 사용하지 마세요.

리액트의 `Reconcillation` 은 컴포넌트 아이덴티티를 사용해 컴포넌트 하위 트리를 렌더링해야할지 말지, 아예 소멸시키고 새로운 컴포넌트를 마운트 할지 결정하기 위해 사용됩니다. 만약 `render` 함수가 반환하는 컴포넌트가 이전 것과 같다면, 리액트를 재귀적으로 하위 트리를 새로운 것과 비교하면서 업데이트 합니다. 만약 그들이 같지 않다면, 이전 컴포넌트를 완전히 소멸시킵니다.

만약 다음과 같이 고차 컴포넌트를 렌더 함수안에서 생성하면, 성능의 문제 뿐만 아니라 컴포넌트가 새로 생성됨으로써 해당 컴포넌트 트리의 모든 상태가 소실됩니다.

```jsx
render() {
  // A new version of EnhancedComponent is created on every render
  // EnhancedComponent1 !== EnhancedComponent2
  const EnhancedComponent = enhance(MyComponent);
  // That causes the entire subtree to unmount/remount each time!
  return <EnhancedComponent />;
}
```

대신에, 고차 컴포넌트를 컴포넌트 정의 밖에서 생성해서 고차 컴포넌트가 단 한 번만 생성되도록 하세요.

만약 아주 가끔 항상 고차 컴포넌트를 새로 생성해야 한다면, 컴포넌트 생명 주기나 생성자 안에서 하도록 하세요.

## 정적 메소드는 반드시 계속 복사되어야만 합니다.

종종 **정적 메소드**를 리액트 컴포넌트에 정의하는게 유용할 때가 있습니다. 
예를 들면, `Relay` 컨테이너는 정적 메소드 `getFragment`를 노출해서 `GraphQL fragment`의 구성을 촉진합니다.

고차 컴포넌트를 생성할 때는 기능이 확장되기는 하나, 원래 컴포넌트가 갖고 있던 정적 메소드까지 자동으로 확장되지는 않습니다. 따라서 감싸진 컴포넌트를 반환하기 전에 항상 정적 메소드를 복사하도록 하세요. 

하지만 항상 어떤 정적 메소드가 있는지 일일이 확인하고 복사하기는 어렵습니다. 그래서,
`hoist-non-react-statics`를 사용해서 모든 non-React 정적 메소드를 복사하세요.

```jsx
import hoistNonReactStatic from 'hoist-non-react-statics';
function enhance(WrappedComponent) {
  class Enhance extends React.Component {/*...*/}
  hoistNonReactStatic(Enhance, WrappedComponent);
  return Enhance;
}
```

또다른 방법은 **정적 메소드**를 컴포넌트 자체로부터 추출하는 방법입니다.

```jsx
// Instead of...
MyComponent.someFunction = someFunction;
export default MyComponent;

// ...export the method separately...
export { someFunction };

// ...and in the consuming module, import both
import MyComponent, { someFunction } from './MyComponent.js';
```

## 참조는 전달되지 않습니다.

고차 컴포넌트들의 규칙이 `props`를 감싸진 컴포넌트들로 전달하는 것이지만, 참조는 그렇지 않습니다.
고차 컴포넌트의 `ref`는 감싸진 컴포넌트의 `ref`와 같지 않습니다.

이것은 `.forwardRef` 로 해결할 수 있습니다.

[Higher-Order Components - React](https://reactjs.org/docs/higher-order-components.html)