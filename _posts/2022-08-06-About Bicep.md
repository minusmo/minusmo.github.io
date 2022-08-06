---
title: About Bicep
category: DSL
tags: Azure ARM IaaS
toc: true
toc_label: "Contents"
---

이 블로그 포스트의 내용은 2022 Open Source Contributon Challenges 기간 워크샵 내용을
정리한 것입니다.

# 2022 OSSC 3rd meetup note

# Today’s Topic: Bicep

# Resource란?

**Resouce:** (remote machine의 자원들을 총칭하는 것)
ex) network, cpu, hdd, ram …

# Bicep을 사용하는 이유?

**ARM(**Azure Resource Manager**) template**을 사용해서 resource를 선언적으로 정의할 수 있다!

**Bicep → ARM을 쉽게 하기위한 DSL(Domain Specific Language)!**

## 실습 단계

**Resource를 만들고 거기다가 Azure function을 배포할 것!**

우리 프로젝트에서는 **API Management**에서 **BFF**를 구성해서 사용할 것이다!

1. **bicep** cli install
2. **bicep** extension install
3. **az** login *azure platform*에 잘 로그인 되었는지 확인하고, 자신의 *구독정보*를 확인한다!
4. **mkdir infra, cd infra** infra는 bicep 파일을 만들 디렉토리 이름!
5. **touch** main.bicep bicep 파일 생성!
6. **az bicep build** -f main.bicep

## What should you Know!

- **param**: cli를 통해 받을 외부 입력값 정의합니다.
- **var**: bicep 파일 내부에서 사용될 변수를 정의합니다.
- **resource**: Azure cloud 서비스에서 사용할 자원을 선언합니다.
- **output**: bicep 파일을 모듈화 하기 위해 사용합니다. 다른 bicep 파일에서 참조 가능한 값을 정의합니다.

### In practice,

**bicep template**을 **microsoft docs**에서 받아서 사용!

- `az deployment group create -n 배포 이름 -g 리소스 그룹 이름 -f bicep 엔트리 파일 이름 -p 파라미터 이름 = 파라미터 값`
    
    내가 원하는 리소스 그룹에서 배포하기 위한 커맨드
    

**Azure platform console** 에서 **azure function ap**p 을 실행하기 위해서는

- App service plan: 요금제를 정의!
- Storage account: 이름은 반드시 영문 소문자 24자 이내로 작성!!

가 반드시 필요하다.

## HW

bicep으로 생성해야할 리소스

- API management: 애저 API 관리자
- storage account: 애저 저장소 어카운트
- app service plan: 애저 앱 서비스 플랜
- azure function: 애저 펑션
- application insight: 애저 애플리케이션 인사이트
- azure log analytics: 애저 로그 아날리틱스 워크스페이스

*bicep azure tutorial* 참고하는 것도 좋다!.(초,중,고급 과정)

bicep file을 github repository에 업로드하고 챗룸에 링크 남기기!

# 배포 명령

`az deployment group create --resource-group "리소스 그룹 이름" --template-file 템플릿 파일 경로 --parameters 파라미터이름=파라미터값`

만약 구독이 여러개라면, 어느 구독에 배포할 것인지 컨텍스트를 설정해 주어야 한다.

`az account set --subscription "구독 이름”`

리소스 그룹을 먼저 생성할 수도 있다.

`az group create --location 지역이름 --name "리소스 그룹 이름”`

# 참고

[Create Azure Application Insights with Bicep](https://oulasvirta.github.io/2020/09/22/create-app-insights-bicep.html)

[배포 기록 - Azure Resource Manager](https://docs.microsoft.com/ko-kr/azure/azure-resource-manager/templates/deployment-history?tabs=azure-portal)

[Create your function app resources in Azure using Bicep](https://docs.microsoft.com/en-us/azure/azure-functions/functions-create-first-function-bicep?tabs=CLI)

[가격 책정 - Azure Monitor | Microsoft Azure](https://azure.microsoft.com/ko-kr/pricing/details/monitor/)

[Migrate an Application Insights classic resource to a workspace-based resource - Azure Monitor - Azure Monitor](https://docs.microsoft.com/en-us/azure/azure-monitor/app/convert-classic-resource)