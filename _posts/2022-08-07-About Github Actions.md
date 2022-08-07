---
title: About Github Actions
category: devOps
tags: github CD CI
toc: true
toc_label: "Contents"
---

이 블로그 포스트의 내용은 2022 Open Source Contributon Challenges 기간 워크샵 내용을
정리한 것입니다.

# 2022 OSSC 4th meetup note

# Today’s Topic: Github Actions

[terraform](https://www.terraform.io/), [pulumi](https://www.pulumi.com/) 등 다른 **CI/CD** 를 위한 **IaaS** 를 위한 도구들도 있다.

## Continuous Deployment

[Continuous Deployment](https://en.wikipedia.org/wiki/Continuous_deployment)(지속적 배포): 소프트웨어의 기능이 **자동화된 배포**를 통해 자주 제공되는 것을 말한다. 이것은 **수동 릴리스**를 통해 언제든지 배포할 수 있는 소프트웨어를 제공하는 기능이다. 이는 자동화된 배포를 사용하는 **연속적전달**과는 대조된다. *Martin Fowler* 에 따르면, **지속적인 배포**에는 **지속적 전달**이 필요하다.

## Continuous Delivery

[Continuous Delivery](https://docs.microsoft.com/en-us/devops/deliver/what-is-continuous-delivery)(지속적 전달): 소프트웨어를 릴리스 할 때, 수동으로 수행하지 않고도 언제든지 안정적으로 릴리스 할 수 있도록 한다. **더 빠른 속도와 빈도로 소프트웨어를 빌드, 테스트 및 릴리스하는 것**을 목표로한다. 이는 프로덕션 환경의 애플리케이션에 대한 더 많은 증분 업데이트를 허용하여, 변경 사항을 제공하는 데 드는 비용, 시간 및 위협을 줄이는데 도움이 된다. 지속적 배포를 위해서는 **간단하고 반복 가능한 배포 프로세스**가 중요하다.

## Continuous Integration

**[Continuous Integretion](https://en.wikipedia.org/wiki/Continuous_integration)(지속적 통합)**

모든 개발자의 작업 복사본을 하루에 여러 번 공유 메인라인에 병합하는 방식입니다. 변경을 시작할 때, 개발자는 작업할 현재 코드 기반의 복사본을 가져옵니다. 다른 개발자가 변경된 코드를 소스 코드 리포지토리에 제출하면, 이 복사본이 리포지토리 코드를 반영하지 않게 됩니다. 기존 코드 기반이 변경될 수 있을 뿐만 아니라, 종속성 및 잠재적 충돌을 생성하는 새 라이브러리 및 기타 리소스 뿐만 아니라 새 코드가 추가될 수 있습니다. 

따라서 코드를 제출하기 전에, 먼저 기존 리포지토리의 변경사항을 반영하도록 코드를 업데이트해야합니다. 

### Workflow of CI

- 로컬에서 테스트 실행
- CI에서 코드 컴파일
- CI에서 테스트 실행
- CI에서 아티팩트 배포

### **CI 와 CD를 구분**하는 것이 중요하다

깃허브 액션은 CI, CD 를 구분할 수 있는 도구이다.

이벤트 기반으로 액션이 발생하며, **issue, PR** 등 다양한 이벤트에 대해 동작을 실행할 수 있다.

**수동**으로도 워크플로우를 실행할 수 있다!

# 개발환경 설정하기

다음의 두 vscode 확장 프로그램을 설치합니다.

[YAML - Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-yaml)

[GitHub Actions - Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=cschleiden.vscode-github-actions)

### 기본 워크 플로우 파일 생성 방법

1. `mkdir .github/` 
2. `mkdir .github/workflows`
3. `touch main.yaml`

***워크플로우를 정의하는것*** 을 깃허브 액션이라고도한다.

액션에서 **job**이 생성되면,

**job**은 github 클라우드의 큐에 들어가고, 랜덤하게 가상머신을 잡아서 실행된다.

가상머신의 성능도 모두 제각각이라, 어떤 작업이 먼저 끝날지도 알 수 없다.

시간 종속성을 설정해 줄 수도 있다. 예를 들어, *빌드* 가 반드시 끝난 후에 *릴리스* 를 해야하는 경우가 있을 수 있다.

# 워크플로우 파일 작성하기

## 기본 문법

```yaml
name: 'My First GitHub Actions' # 워크플로우 이름을 지정

on: push # 어떤 이벤트에서 액션이 트리거 될지를 지정. 여러개의 이벤트를 지정할 수도 있다.

env: # 환경 변수를 지정. 각 환경 변수는 선언된 블록에서 스코프를 가진다. 상위 스코프에서 선언된 환경 변수는 하위 스코프로 전달된다.
  WORKFLOW_LEVEL: "This value comes from the WORKFLOW level"

jobs: # 어떤 일을 수행할지를 지정. 여러개의 일을 수행할 수도 있다.
  first-job: # 일을 정의
    name: 'First Job' # 일의 이름

    runs-on: ubuntu-latest # 어떤 운영체제에서 실행될지를 지정. # 여러개의 운영체제를 지정할 수도 있다.

    steps: # 일의 실행 단계를 지정.
    - name: Say Hello World 1 # 단계의 이름을 지정
      shell: bash # 단계의 명령 실행 환경을 지정
      run: | # 단계에서 실행할 명령을 지정. 여러개의 명령을 실행할 수도 있다.
        echo "Hello World from step 1"

    - name: Say Hello World 2
      shell: pwsh
      run: |
        echo "Hello World from step 2"
```

## 런타임에서 환경 변수 선언

```yaml
name: 'My First GitHub Actions'

on: push

env:
  PRESET_VALUE: "This is the preset value"

jobs:
  first-job:
    name: 'First Job'

    runs-on: ubuntu-latest

    steps:
    - name: Set environment variable 1
      shell: bash
      run: | # github 환경변수를 런타임에 추가한다.
        echo "STEPSET_VALUE_1='This is the value 1 set in the step'" >> $GITHUB_ENV

		- name: Check environment variables
      shell: bash
      run: | # github 문법을 사용해 환경변수를 사용할 수 있다.
        echo "preset value: ${{ env.PRESET_VALUE }}"
        echo "stepset value 1: ${{ env.STEPSET_VALUE_1 }}"
```

## 참조가능한 값 내보내기

```yaml
name: 'My First GitHub Actions'

on: push

jobs:
  first-job:
    name: 'First Job'

    runs-on: ubuntu-latest

    steps:
    - name: Set output value
      id: first # 참조 가능하도록 id를 지정해준다.
      shell: bash
      run: | # 내보낼 값을 설정한다.
        first_value="This is the value for the first output"

        echo "::set-output name=first_value::$first_value"

    - name: Check output value
      shell: bash
      run: | # id를 통해 내보내진 값을 참조할 수 있다.
        echo "first value: ${{ steps.first.outputs.first_value }}"
```

`echo "::add-mask::$first_value"` 을 값을 내보내기 전에 추가하면, 

중요 정보가 안보이게 마스킹을 할 수도 있다. → job이 실행중일 때는 참조 가능하나, 외부로 노출될 때(로그에 찍힐 때 등)에는 ***로 가려진다.

## Github Secrets 사용하기

Github의 리포지토리 세팅에서, **secrets** 에 값을 추가하고, 이를 참조하는 것으로 비밀 정보를 사용할 수 있다.

```yaml
name: 'My First GitHub Actions'

on: push

jobs:
  first-job:
    name: 'First Job'

    runs-on: ubuntu-latest

    steps:
    - name: Show secret
      shell: bash
      run: | # github secrets의 값을 참조한다.
        echo ${{ secrets.HELLO }}

    - name: Check secret
      shell: pwsh # 파워쉘을 사용한다.
      run: | # 이와 같이 조건문을 추가할 수도 있다. 
        if ("${{ secrets.HELLO }}" -eq "World") {
            echo "YES!"
        } else {
            echo "NO!"
        }
```

## Matrix 사용하기

Matrix를 사용하여, 같은 작업을 코드를 중복하지 않고 여러버전의 언어, 혹은 여러 운영체제의 가상머신에서 실행할 수 있다. 다음의 job에서는 3개의 운영체제와 2개의 nodejs 런타임 버전에서 총 6번 실행된다.

```yaml
name: 'My First GitHub Actions'

on: push

jobs:
  first-job:
    name: 'First Job'

    strategy: # 매트릭스 전략을 선언한다.
      matrix: # 매트릭스를 정의한다. 하나 이상의 원소를 갖는 배열을 정의한다.
        os: [ 'windows-latest', 'macos-latest', 'ubuntu-latest' ]
				nodejs: [ '14.x', '16.x' ]

    runs-on: ${{ matrix.os }} # 매트릭스에서 정의된 운영체제의 값을 참조한다.

    steps:
    - name: Setup node.js
      uses: actions/setup-node@v3
      with:
        node-version: ${{ matrix.nodejs }}

    - name: Check node.js version from ${{ matrix.os }}
      shell: bash
      run: |
        echo $(node --version) # 설치된 nodejs의 버전을 확인한다.
```

## 작업에 조건문 달기

원하는 조건에서만 작업을 실행하도록 조건을 설정할 수 있다.

```yaml
name: 'My First GitHub Actions'

on: [ 'push', 'pull_request' ] # 2개의 이벤트에서 작업이 실행되도록 설정한다.

jobs:
  first-job:
    name: 'First Job'
    if: github.event_name == 'push' # 이벤트가 push일 때만 작업을 실행한다.

    strategy:
      matrix:
        os: [ 'windows-latest', 'macos-latest', 'ubuntu-latest' ]

    runs-on: ${{ matrix.os }}

    steps:
    - name: Say Hello World from ${{ matrix.os }}
      shell: bash
      run: |
        echo "Hello World on ${{ matrix.os }}"

  second-job:
    name: 'Second Job'
    if: github.event_name == 'pull_request' # 이벤트가 pull_request일 때만 작업을 실행한다.

    strategy:
      matrix:
        os: [ 'windows-latest', 'macos-latest', 'ubuntu-latest' ]

    runs-on: ${{ matrix.os }}

    steps:
    - name: Say Hello World from ${{ matrix.os }}
      shell: bash
      run: |
        echo "Hello World on ${{ matrix.os }}"
```

## 스텝에 조건문 달기

원하는 조건에서만 스텝을 실행하도록 조건을 설정할 수 있다.

```yaml
name: 'My First GitHub Actions'

on: push

jobs:
  first-job:
    name: 'First Job'

    strategy:
      matrix:
        os: [ 'windows-latest', 'macos-latest', 'ubuntu-latest' ]

    runs-on: ${{ matrix.os }}

    steps:
    - name: Say Hello World from ${{ matrix.os }} 1
      shell: bash
      run: |
        echo "Hello World on ${{ matrix.os }} 1"

    - name: Say Hello World from ${{ matrix.os }} 2
      if: matrix.os == 'ubuntu-latest' # os가 ubuntu-latest일 때만 스텝을 실행한다.
      shell: bash
      run: |
        echo "Hello World on ${{ matrix.os }} 2"
```

## 작업 체이닝

작업이 특정 순서로 실행되도록 설정해줄 수 있다.

```yaml
name: 'My First GitHub Actions'

on:
  push:
    branches:
    - main

jobs:
  first-job:
    name: 'First Job'

    runs-on: ubuntu-latest

    steps:
    - name: Say Hello World from first job
      shell: bash
      run: |
        echo "Hello World from first job"

  second-job:
    name: 'Second Job'
    needs: first-job # second-job은 반드시 first-job이 실행된 후에만 실행된다.

    runs-on: ubuntu-latest

    steps:
    - name: Say Hello World from second job
      shell: bash
      run: |
        echo "Hello World from second job"
```

## 이벤트 추가하기

```yaml
name: 'My First GitHub Actions'

on: # push이고, branch가 main일때, push이고, v로 시작하는 태그일때, pull_request이고, branch가 main일때 실행된다.
  push:
    branches:
    - main
    tags:
    - 'v*'
  pull_request:
    branches:
    - main

jobs:
  build:
    name: Build Apps

    runs-on: ubuntu-latest

    steps:
    - name: Checkout the repo
      uses: actions/checkout@v2 # 재사용 가능한 오픈소스 워크플로우를 사용한다.

    - name: Setup .NET SDK
      uses: actions/setup-dotnet@v1
      with: # 재사용 가능한 워크플로우에 필요한 값을 넘겨준다.
        dotnet-version: '6.x'

    - name: Restore NuGet packages
      shell: bash
      run: |
        dotnet restore ./api

    - name: Build solution
      shell: bash
      run: |
        dotnet build ./api -c Release

    - name: Create FunctionApp artifact
      shell: bash
      run: |
        dotnet publish ./api -c Release -o ./api/bin/published

    - name: Upload FunctionApp artifact
      uses: actions/upload-artifact@v2
      with:
        name: apiapp
        path: api/bin/published

  release:
    name: Release Apps
    needs: build

    runs-on: ubuntu-latest

    steps:
    - name: Download FunctionApp artifact
      uses: actions/download-artifact@v2
      with:
        name: apiapp
        path: artifacts/api

    - name: Zip FunctionApp artifact
      shell: bash
      run: |
        pushd artifacts/api
        zip -qq -r apiapp.zip .
        popd

        mv artifacts/api/apiapp.zip artifacts/apiapp.zip

    - name: Release FunctionApp artifact to GitHub
      uses: "marvinpinto/action-automatic-releases@latest"
      with:
        repo_token: "${{ secrets.GITHUB_TOKEN }}"
        prerelease: false
        files: |
          artifacts/apiapp.zip
```

## 수동으로 워크플로우 실행하기

수동으로 워크플로우를 입력과 함께 실행할 수 있다.

```yaml
name: 'Manual Release'

on:
  workflow_dispatch: # 수동 워크플로우 실행을 정의한다.
    inputs: # 어떤 입력을 받을 것인지 정의한다.
      title:
        type: string
        required: true
        description: Enter the release title

jobs:
  build:
    name: Build Apps

    runs-on: ubuntu-latest

    steps:
    - name: Checkout the repo
      uses: actions/checkout@v2

    - name: Setup .NET SDK
      uses: actions/setup-dotnet@v1
      with:
        dotnet-version: '6.x'

    - name: Restore NuGet packages
      shell: bash
      run: |
        dotnet restore ./api

    - name: Build solution
      shell: bash
      run: |
        dotnet build ./api -c Release

    - name: Create FunctionApp artifact
      shell: bash
      run: |
        dotnet publish ./api -c Release -o ./api/bin/published

    - name: Upload FunctionApp artifact
      uses: actions/upload-artifact@v2
      with:
        name: apiapp
        path: api/bin/published

  release:
    name: Release Apps
    needs: build

    runs-on: ubuntu-latest

    steps:
    - name: Download FunctionApp artifact
      uses: actions/download-artifact@v2
      with:
        name: apiapp
        path: artifacts/api

    - name: Zip FunctionApp artifact
      shell: bash
      run: |
        pushd artifacts/api
        zip -qq -r apiapp.zip .
        popd

        mv artifacts/api/apiapp.zip artifacts/apiapp.zip

    - name: Release FunctionApp artifact to GitHub
      uses: "marvinpinto/action-automatic-releases@latest"
      with:
        repo_token: "${{ secrets.GITHUB_TOKEN }}"
        prerelease: false
        title: ${{ github.event.inputs.title }} # 워크플로우 실행시 입력받은 값을 참조한다.
        files: |
          artifacts/apiapp.zip
```

## 재사용 가능한 로컬 워크플로우 호출하기

재사용 가능한 워크플로우를 분리하고, 원할 때 호출하여 사용할 수 있다.

```yaml
name: 'My First GitHub Actions'

on:
  push:
    branches:
    - main
    tags:
    - 'v*'
  pull_request:
    branches:
    - main

jobs:
  call_build:
    uses: ./.github/workflows/ci.yaml # 로컬 워크플로우 호출
    with:
      artifact_name: apiapp

  call_release:
    uses: ./.github/worlfows/cd.yaml # 로컬 워크플로우 호출
    needs: call_build
    with:
      title: latest
      artifact_name: apiapp
    secrets: inherit # 호출하는 워크플로우의 secrets를 호출된 워크플로우로 상속한다.
```

## 다중 단계 배포

여러 단계를 거치는 배포 작업을 환경 변수를 구분하고, 워크플로우를 호출하는 것으로 구성할 수 있다.

```yaml
name: 'My First GitHub Actions'

on:
  push:
    branches:
    - main
    tags:
    - 'v*'
  pull_request:
    branches:
    - main

jobs:
  call_build:
    uses: ./.github/workflows/ci.yaml
    with:
      artifact_name: apiapp

  call_release_dev: # 개발 릴리스 워크플로우는 빌드 워크플로우가 먼저 호출된뒤에 호출된다.
    uses: ./.github/worlfows/cd.yaml
    needs: call_build
    with:
      title: latest
      artifact_name: apiapp
      env: DEV # 환경변수를 입력으로 받아 개발 단계와 제품 단계를 구분한다.
    secrets: inherit

  call_release_prod: # 제품 릴리스 워크플로우는 개발 릴리스 워크플로우가 먼저 호출된뒤에 호출된다.
    uses: ./.github/worlfows/cd.yaml
    needs: call_release_dev
    with:
      title: latest
      artifact_name: apiapp
      env: PROD
    secrets: inherit
```

# HW

멘토님 실습 리포지토리에서 step 4, 5 실습해보고 레포에 올리고 링크 남기기

[https://github.com/devkimchi/github-actions-from-scratch](https://github.com/devkimchi/github-actions-from-scratch)

# 참고

[Continuous delivery - Wikipedia](https://en.wikipedia.org/wiki/Continuous_delivery)

[Continuous integration - Wikipedia](https://en.wikipedia.org/wiki/Continuous_integration)

[Continuous deployment - Wikipedia](https://en.wikipedia.org/wiki/Continuous_deployment)