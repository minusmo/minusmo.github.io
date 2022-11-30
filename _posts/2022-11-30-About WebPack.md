---
title: About Webpack
category: modularization
tags: frontend bundler 
toc: true
toc_label: "Contents"
---

웹팩을 이제야 공부하다니… html 태그랑 CSS 만지기는 정말 싫어해서 웹앱은 가능하면 다 JS로 만들고싶어하는 주제에… 네. JS 코더 실격입니다. 사실 한참 전부터 모듈 번들러(웹팩, 걸프, 파셀 등등)를 공부해서 잘 써먹어야지 했지만 결국 하지 못했습니다. 하지만!!! 지금이라도 알아봅시다. 

# 웹팩의 개념

“웹 팩은 모던 JS 어플리케이션을 위한 정적 모듈 번들러입니다” 라고 공식 문서에 쓰여있습니다.
웹팩이 js 애플리케이션을 처리할 때, 내부적으로는 프로젝트에 필요한 모든 모듈을 맵핑하고, 하나 이상의 번들을 생성하는 [의존성 그래프](https://webpack.kr/concepts/dependency-graph/)를 만듭니다. 라고 또 써 있습니다.

- 의존성
    
    웹팩에서 말하는 의존성은 [모듈화](https://webpack.kr/concepts/modules)된 파일간의 종속성입니다. 한 파일에서 다른 파일을 로드하여 사용해야한다면, 의존성이 생기는 것이죠. 웹팩은 이 의존성을 엔트리 포인트 파일(main.js)로 부터 만들어나 갑니다.
    

웹팩의 장점은, 번들링하기 위한 작업이 간편하다는 것입니다. 사용자의 요구에 따라 유연하게 설정을 변경할 수 있습니다.

## 핵심 개념

웹팩의 핵심 개념은 다음과 같습니다.

- 엔트리
- 출력
- 로더
- 플러그인
- 모드
- 브라우저 호환성

## [엔트리](https://webpack.kr/concepts/entry-points)

엔트리 포인트는 웹팩이 의존성 그래프를 그려나가기 시작하는 입구입니다. 웹팩은 엔트리로부터 모듈들의 직간접적 의존성을 찾아냅니다. 

엔트리 포인트의 기본 경로는 ./src/index.js 이지만, 웹팩 설정에서 손쉽게 다른 경로로 설정할 수 있습니다.

```jsx
module.exports = {
  entry: './path/to/my/entry/file.js',
};
```

그러니까 엔트리 포인트는, 말하자면 내가 작성한 소스코드의 최상위 모듈이 됩니다.

## [출력](https://webpack.kr/concepts/output)

출력 속성은 생성될 번들을 내보낼 위치와 이 파일의 이름을 지정하는 방법을 웹팩에 알려주는 역할을 합니다.
기본 출력 파일은 ./dist/main.js로 설정이 되어있고, 생성된 다른 파일들은 ./dist 폴더 안에 있습니다.

```jsx
const path = require('path');

module.exports = {
  entry: './path/to/my/entry/file.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'my-first-webpack.bundle.js',
  },
};
```

여기서는 output.filename 과 output.path 속성을 사용해서 웹팩이 내보낼 번들 이름과 경로를 지정해주었습니다. 첫줄에서 가져오는 path 모듈은 파일 경로를 지정하기 위해 사용되는 core Node.js 모듈입니다.

## [로더](https://webpack.kr/concepts/loaders)

웹팩은 기본적으로는 JS,JSON 파일만 이해합니다. 로더를 사용하면, 웹팩이 다른 유형의 파일을 처리하거나, 그들을 유효한 모듈로 변환하여 애플리케이션에 사용하거나 의존성 그래프에 추가됩니다.

상위 수준에서 로더는 웹팩 설정에 두 가지 속성을 가집니다.

- 변환이 필요한 파일들을 식별하는 test 속성
- 변환을 수행하는데 사용되는 로더를 가리키는 use 속성

```jsx
const path = require('path');

module.exports = {
  output: {
    filename: 'my-first-webpack.bundle.js',
  },
  module: {
		// test 할 파일을 지정할 때 정규식과 문자열을 잘 구분하세요.
		// 정규식은 ',"를 사용하지 않습니다.
    rules: [{ test: /\.txt$/, use: 'raw-loader' }],
  },
};
```

여기서는 로더 설정을 하기 위해 module.rules 속성을 지정해줍니다. 이 속성에는 언급한 test, use 속성이 정의됩니다. 이 설정은 자연어로 말하면 다음과 같습니다.

> *"이봐 webpack 컴파일러, `require ()`/`import` 문 내에서 '.txt' 파일로 확인되는 경로를 발견하면 번들에 추가하기 전에 `raw-loader`를 **사용하여** 변환해."*
> 

## [플러그인](https://webpack.kr/concepts/plugins)

로더는 특정 유형의 모듈을 변환하는데 사용되지만, 플러그인을 활요하여 번들을 최적화하거나, 에셋을 관리하고, 환경변수 주입과 같은 더 많은 작업을 수행할 수 있습니다.

플러그인을 사용하기 위해서는 require()를 통해 플러그인을 요청하고, plugins 배열에 추가해야합니다. 대부분의 플러그인은 옵션을 통해 사용자가 지정할 수 있습니다. 다른 목적으로 플러그인을 여러번 사용하도록 설정할 수 있으므로, new 연산자로 호출하여 플러그인의 인스턴스를 만들어야합니다.

```jsx
const HtmlWebpackPlugin = require('html-webpack-plugin');
const webpack = require('webpack'); // 내장 plugin에 접근하는 데 사용

module.exports = {
  module: {
    rules: [{ test: /\.txt$/, use: 'raw-loader' }],
  },
  plugins: [new HtmlWebpackPlugin({ template: './src/index.html' })],
};
```

여기의 html-webpack-plugin은, 생성된 모든 번들을 자동으로 삽입하여 애플리케이션용 html 파일을 생성합니다.

웹펙은 [설치없이 사용가능한 플러그인들](https://webpack.kr/plugins)을 제공합니다.

## [모드](https://webpack.kr/configuration/mode)

모드 파라미터를 development, production, none 으로 설정하면, 웹팩에 내장된 환경별 최적화를 활성화할 수 있습니다. 기본값은 production입니다.

## 브라우저 호환성

웹팩은 ES5가 호환되는 모든 브라우저를 지원합니다(IE8 이하는 제외). 웹팩은 import() 및 require.ensure()을 위한 Promise를 요구합니다. 구형 브라우저를 지원하려면, 이러한 표현식을 사용하기전에 [폴리필을 로드](https://webpack.kr/guides/shimming/)해야합니다.

## 웹팩 사용환경

웹팩 5는 Node.js 10.13.0 이상에서 실행됩니다.

## 마치며

이번글에서는 웹팩이라는 것을 왜 사용하는 것인지, 사용하면 무엇이 해결되는 것인지, 어떻게 사용하는 것인지를 간략하게 알아보았습니다. 앞으로 점점 더 알아가면서, 요긴하게 사용될 것 같습니다.