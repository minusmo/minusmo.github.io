---
title: About Azure Function
category: backend
tags: Azure microservice
toc: true
toc_label: "Contents"
---

이 블로그 포스트의 내용은 2022 Open Source Contributon Challenges 기간 워크샵 내용을
정리한 것입니다.

# 2022 OSSC 2nd meetup note

# 로컬 환경에서 Azure function 빌드해보기

_(개발 환경 설정이 모두 되어있다는 전제하에 진행합니다!)
(개발 환경이 설정되지 않았다면 다음을 참고해주세요!)_

- 기본 개발 환경 설정하기
  - .NET 6 SDK: [dot.net](http://dot.net/)
  - Visual Studio: [visualstudio.com](http://visualstudio.com/)
  - Visual Studio Code: [visualstudio.com](http://visualstudio.com/)
  - Azure CLI: [docs.microsoft.com/cli](http://docs.microsoft.com/cli)
  - PowerShell: [docs.microsoft.com/powershell](http://docs.microsoft.com/powershell)
  - M365 개발자 계정: [https://study.fusiondev.kr/m365/m365-dev-setup](https://study.fusiondev.kr/m365/m365-dev-setup)
  - 파워 플랫폼 개발자 계정: [https://study.fusiondev.kr/pp/pp-dev-setup](https://study.fusiondev.kr/pp/pp-dev-setup)
  - NHN 클라우드 계정 생성: [https://toast.com/](https://toast.com/)

# 추가적인 개발 환경 설정하기

### Azure-function-core-tools 설치하기

다음의 주소를 참고하여 Azure function 개발을 위한 CLI tool을 설치합니다.

_azure-functions-core-tools@4_ 로 설치해야합니다!!(코어 툴즈 버전 4)

[GitHub - Azure/azure-functions-core-tools: Command line tools for Azure Functions](https://github.com/Azure/azure-functions-core-tools#readme)

다음과 같이 **.Net SDK와 azure-functions-core-tools** 의 설치와 버전을 확인합니다.(터미널에서)

```powershell

dotnet --version
6.0.301

func --version
4.0.4629

which func
/usr/local/bin/func

which dotnet
/usr/local/share/dotnet/dotnet
```

# 프로젝트 생성하기

## 디렉토리 생성하기

1. 루트 디렉토리에 _새로운 디렉토리를 생성합니다._
2. **VS Code** 를 이용해 새로운 디렉토리를 열어줍니다.
3. **VS Code 터미널**을 엽니다.

_이제부터 VS Code 터미널로 진행합니다._

## Azure function 생성하기(CLI)

### func init

후에 터미널에 나오는 옵션 설정에서,

1. _dotnet_ 선택 → 1 입력
2. _C#_ 선택 → 1 입력

### func new

후에 터미널에 나오는 옵션 설정에서,

1. _HttpTrigger_ 선택 → 1 입력
2. 함수 이름 설정 → 원하는 함수이름(실습에서는 _PingHttpTrigger_ 로 설정)

이제 디렉토리를 확인해보면 새로 파일들이 생성되었습니다.

_.csproj_ 파일을 열어 **<TargetFramework>**, **<AzureFunctionsVersion>** 태그 안의 값을 확인합니다.

- **<TargetFramework> ⇒ net6.0**
- **<AzureFunctionsVersion> ⇒ v4**

## 네임스페이스 수정

다음과 같은 태그를 .csproj 파일에 추가합니다.
_(<AzureFunctionsVersion> 태그 뒤에 추가하면 됩니다.)_

```xml
<AssemblyName>OCAProject</AssemblyName>
<RootNamespace>OCAProject</RootNamespace>
```

이제 .cs 파일(PingHttpTrigger.cs) 파일을 열어 소스코드 _최상단_ 의 _namespace_ 를 다음과 같이 수정합니다.

```csharp
namespace OCAProject
```

터미널에 _dotnet build ._ 을 입력해 Azure function을 한번 빌드해주면 오류 표시줄이 모두 사라집니다.

## 클래스 수정하기

**PingHttpTrigger** 클래스를 다음과 같이 수정해줍니다.

```csharp
[FunctionName(nameof(PingHttpTrigger))]
public static IActionResult Run(
[HttpTrigger(AuthorizationLevel.Function, "get", Route = "ping")] HttpRequest req,
ILogger log)
```

그리고 다음의 코드를 삭제해줍니다.

```csharp
string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
dynamic data = JsonConvert.DeserializeObject(requestBody);
name = name ?? data?.name;
```

이제 **dotnet build .** 을 통해 다시 한번 빌드하고,

**func start** 를 통해 어플리케이션을 실행하면, **[localhost](http://localhost)** 환경에서 _responseMessage_ 변수의 값이 출력되는 것을 확인할 수 있습니다.

[localhost](http://localhost) 주소 뒤에 _query string_ ex)?name=johnDoe 을 추가하여 요청을 보내면, 쿼리 스트링 값이 포함된 문자열 응답을 확인할 수 있습니다.

## 응답 객체 분리하기

_OCAProject namespace_ 안에 다음과 같은 클래스를 생성해줍니다.
_(PingHttpTrigger class 뒤에)_

```csharp
public class ResponseMessage {
    [JsonProperty("response_message")] // Json 응답 객체의 key 를 변경. 기본적으로는 파스칼 케이싱을 캐멀 케이싱으로 변환.
    public string Message { get; set; }
}
```

→ 기존의 문자열 _response_ 를 _JSON response_ 로 바꿔주기 위함입니다.

→ **[JsonProperty(string 응답 메세지의 key)] 를 통해 JSON 응답 메세지의 _key_ 값을 바꿀 수 있습니다.(속성 오버로딩)**

이제 다음과 같이 _Run_ method를 수정해주면, 전과 같은 응답을 볼 수 있습니다.

```csharp

var res = new ResponseMessage() { Message = responseMessage };

return new OkObjectResult(res);
```

## 업무규칙 분리하기

_OCAProject namespace_ 안에 다음과 같은 인터페이스와 클래스를 생성해줍니다.

```csharp
public interface IMyService {
        string GetMessage(string name);
}

public class MyService : IMyService {
    public string GetMessage(string name) {
        string responseMessage = string.IsNullOrEmpty(name)
            ? "This HTTP triggered function executed successfully. Pass a name in the query string or in the request body for a personalized response."
            : $"Hello, {name}. This HTTP triggered function executed successfully.";

        return responseMessage;
    }
}
```

→ 주요 업무규칙을 분리하여 *결합도*를 낮춥니다.

→ 업무규칙 클래스가 _인터페이스_ 에 의존하도록 하여 _의존관계를 역전_ 시키고 _느슨한 결합_ 을 만들기 위함입니다.

이제 다음과 같이 _Run_ method를 수정해줍니다.

```csharp
var service = new MyService();
var result = service.GetMessage(name);

var res = new ResponseMessage() { Message = result };
```

→ 이제 업무규칙이 다른 클래스로 분리되었습니다.

→ _Run_ method는 _http request_ 로 받은 값을 업무규칙에 넘겨주고 돌려받은 값을 반환할 뿐입니다.

## 결합도 낮추기

업무규칙을 분리했지만, **PingHttpTrigger** 클래스가 **MyService** 클래스에 _강하게 결합_ 되어 결합도가 높습니다.

결합도를 낮추어 _느슨한 결합_ 을 만들기 위해 _의존성 주입_ 을 합니다.

다음과 같은 _읽기 전용 멤버 변수_ 와 _생성자_ 를 **PingHttpTrigger** 클래스 최상위에 생성합니다.

```csharp
private readonly IMyService _service;

public PingHttpTrigger(IMyService service) {
    this._service = service ?? throw new ArgumentNullException(nameof(service));
}
```

→ 생성자는 _인터페이스_ 를 파라미터로 받아 멤버 변수에 할당하고,

→ _null safe_ 하도록 _service_ 가 _null_ 이면 _NullException_ 에러를 던지도록 합니다.

이제 코드를 다음과 같이 수정합니다.

```csharp
var result = this._service.GetMessage(name);

var res = new ResponseMessage() { Message = result };
```

→ _PingHttpTrigger_ 와 _MyService_ 는 이제 *인터페이스*를 통하여 더 _느슨한 결합_ 을 이루었습니다.

## 패키지 추가 설치하기

다음을 통해 터미널에서 추가 패키지를 설치합니다.

```csharp
dotnet add package Microsoft.Azure.Functions.Extensions
dotnet add package Microsoft.Extensions.Http
```

설치후 **<ItemGroup>** 태그를 .csproj 파일에서 확인하여 추가 패키지가 설치되었는지 확인합니다.

다음과 같은 _Startup.cs_ 이란 이름의 클래스 파일을 루트 디렉토리에 생성합니다.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using Microsoft.Azure.Functions.Extensions.DependencyInjection;
using Microsoft.Extensions.DependencyInjection;

[assembly: FunctionsStartup(typeof(OCAProject.Startup))]
namespace OCAProject
{
    public class Startup: FunctionsStartup {
        public override void Configure(IFunctionsHostBuilder builder)
        {
            builder.Services.AddScoped<IMyService, MyService>();
        }
    }
}
```

→ **의존성 주입**을 위해 생성한 클래스입니다.

→ _builder.Services.AddScoped<IMyService, MyService>();_ 를 통해 _의존성을 설정합니다._

### IoC Container

**IoC**: Inversion of Control(제어 역전)

**_제어 역전_** 이란, **_객체 지향 프로그래밍_** 에서, _소스코드 의존관계_ 를 역전시켜 제어흐름을 역전시키는 것을 말합니다.

IoC Container는 런타임에 자동으로 _종속성 개체_ 를 자동으로 생성해 주입합니다.

[Inversion of Control in C#](https://dotnettutorials.net/lesson/introduction-to-inversion-of-control/)

[Dependency injection in .NET](https://docs.microsoft.com/en-us/dotnet/core/extensions/dependency-injection)

만약 코드에서 _오류선_ 이 사라지지 않는다면, 다음의 두 _VS Code Extension_ 을 설치합니다.

![C# extension 1](./assets/images/c#extension1.png)

![C# extension 2](./assets/images/c#extension2.png)

그리고 오류선에 마우스 커서를 올리고(클릭)

- 윈도우라면 _ctrl + ._
- 맥이라면 _cmd + ._

키 조합을 통해 필요한 네임스페이스를 가져옵니다.

아니면 다음의 네임스페이스가 모두 소스 파일에 있는지 확인합니다.

```csharp
using System;
using System.IO;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.AspNetCore.Http;
using Microsoft.Extensions.Logging;
using Newtonsoft.Json;
```

## OpenApi 등록하기

다음을 통해 터미널에서 패키지를 추가합니다.

```powershell
dotnet add package Microsoft.Azure.WebJobs.Extensions.OpenApi
```

.csproj 파일에서 패키지가 잘 설치되었는지 확인합니다.

다음과 같이 _PingHttpTrigger_ 클래스를 수정합니다.

OpenApi에 등록하기위해 _attribute_ 를 추가해줍니다.

```csharp
[FunctionName(nameof(PingHttpTrigger))]

// OpenApi에 등록합니다.
[OpenApiOperation(operationId: "Ping", tags: new[] { "greeting" })]
// OpenApi credential을 설정합니다.
[OpenApiSecurity(schemeName: "function_key", schemeType: SecuritySchemeType.ApiKey, Name = "x-functions-key", In = OpenApiSecurityLocationType.Header)]
// OpenApi parameter를 설정합니다.
[OpenApiParameter(name: "name", In = ParameterLocation.Query, Required = true, Description = "Name of the person")]
// OpenApi response를 설정합니다.
[OpenApiResponseWithBody(statusCode: HttpStatusCode.OK, contentType: "application/json", bodyType: typeof(ResponseMessage), Description = "response description")]
```

다음의 namespace가 소스 파일에 있는지 확인합니다.

```csharp
using Microsoft.Azure.WebJobs.Extensions.OpenApi.Core.Attributes;
using Microsoft.Azure.WebJobs.Extensions.OpenApi.Core.Enums;
using Microsoft.OpenApi.Models;
using System.Net;
```

이제 다시 어플리케이션을 빌드하고, 로컬 서버를 실행하면, _엔드 포인트_ 가 늘어난 것을 확인할 수 있습니다.

브라우저에서 엔드포인트 중 _swaggerUI_ 가 포함된 url로 요청하면, _OpenAPI_ GUI를 확인할 수 있습니다. 직접 credential 정보와 쿼리 스트링을 포함해 요청해보고, 응답을 확인할 수도 있습니다.

# Azure Function UML Diagram

![Azure Function Diagram](./assets/images/Azure_Function_diagram.png)
