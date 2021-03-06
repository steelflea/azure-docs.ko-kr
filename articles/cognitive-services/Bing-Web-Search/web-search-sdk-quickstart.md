---
title: '빠른 시작: C#용 Bing Web Search SDK 사용'
titleSuffix: Azure Cognitive Services
description: Bing Web Search SDK를 사용하면 Bing Web Search를 C# 응용 프로그램에 쉽게 통합할 수 있습니다. 이 빠른 시작에서는 클라이언트를 인스턴스화하고, 요청을 보내며, 응답을 출력하는 방법에 대해 알아봅니다.
services: cognitive-services
author: erhopf
manager: cgronlun
ms.service: cognitive-services
ms.component: bing-web-search
ms.topic: quickstart
ms.date: 08/16/2018
ms.author: erhopf
ms.openlocfilehash: 04a70c2afbd499d3965e23487cd49540b38e08af
ms.sourcegitcommit: 74941e0d60dbfd5ab44395e1867b2171c4944dbe
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2018
ms.locfileid: "49318659"
---
# <a name="quickstart-use-the-bing-web-search-sdk-for-c"></a>빠른 시작: C#용 Bing Web Search SDK 사용

Bing Web Search SDK를 사용하면 Bing Web Search를 C# 응용 프로그램에 쉽게 통합할 수 있습니다. 이 빠른 시작에서는 클라이언트를 인스턴스화하고, 요청을 보내며, 응답을 출력하는 방법에 대해 알아봅니다.

[!INCLUDE [bing-web-search-quickstart-signup](../../../includes/bing-web-search-quickstart-signup.md)]

## <a name="prerequisites"></a>필수 조건

이 빠른 시작을 실행하기 전에 필요한 몇 가지 조건은 다음과 같습니다.

* [Visual Studio](https://visualstudio.microsoft.com/downloads/) 또는
* [Visual Studio Code 2017](https://code.visualstudio.com/download)
  * [C# for Visual Studio Code](https://visualstudio.microsoft.com/downloads/)
  * [NuGet 패키지 관리자](https://github.com/jmrog/vscode-nuget-package-manager)
* [.Net Core SDK](https://www.microsoft.com/net/download)

## <a name="create-a-project-and-install-dependencies"></a>프로젝트 만들기 및 종속성 설치

> [!TIP]
> [GitHub](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/)에서 최신 코드를 Visual Studio 솔루션으로 가져옵니다.

첫 번째 단계는 새 콘솔 프로젝트를 만드는 것입니다. 콘솔 프로젝트를 설정하는 데 도움이 필요하면 [Hello World - 프로그램 처음 만들기(C# 프로그래밍 가이드)](https://docs.microsoft.com/dotnet/csharp/programming-guide/inside-a-program/hello-world-your-first-program)를 참조하세요. 응용 프로그램에서 Bing Web Search SDK를 사용하려면 NuGet 패키지 관리자를 사용하여 `Microsoft.Azure.CognitiveServices.Search.WebSearch`를 설치해야 합니다.

또한 [Web Search SDK 패키지](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.Search.WebSearch/1.2.0)는 다음을 설치합니다.

* Microsoft.Rest.ClientRuntime
* Microsoft.Rest.ClientRuntime.Azure
* Newtonsoft.Json

## <a name="declare-dependencies"></a>종속성 선언

Visual Studio 또는 Visual Studio Code에서 프로젝트를 열고, 다음과 같은 종속성을 가져옵니다.

```csharp
using System;
using System.Collections.Generic;
using Microsoft.Azure.CognitiveServices.Search.WebSearch;
using Microsoft.Azure.CognitiveServices.Search.WebSearch.Models;
using System.Linq;
```

## <a name="create-project-scaffolding"></a>프로젝트 스캐폴딩 만들기

새 콘솔 프로젝트가 만들어지면 응용 프로그램에 대한 네임스페이스 및 클래스가 만들어져 있습니다. 프로그램은 다음과 같습니다.

```csharp
namespace WebSearchSDK
{
    class YOUR_PROGRAM
    {

        // The code in the following sections goes here.

    }
}
```

다음 섹션에서는 이 클래스 내에 샘플 응용 프로그램을 빌드합니다.

## <a name="construct-a-request"></a>요청 구성

이 코드는 검색 쿼리를 구성합니다.

```csharp
public static void WebResults(WebSearchAPI client)
{
    try
    {
        var webData = client.Web.Search(query: "Yosemite National Park");
        Console.WriteLine("Searching for \"Yosemite National Park\"");

        // Code for handling responses is provided in the next section...

    }
    catch (Exception ex)
    {
        Console.WriteLine("Encountered exception. " + ex.Message);
    }
}
```

## <a name="handle-the-response"></a>응답 처리

다음으로, 응답을 구문 분석하고 결과를 출력하는 코드를 추가해 보겠습니다. 첫 번째 웹 페이지, 이미지, 뉴스 기사 및 비디오에 대한 `name` 및 `url`이 응답 개체에 있으면 출력됩니다.

```csharp
if (webData?.WebPages?.Value?.Count > 0)
{
    // find the first web page
    var firstWebPagesResult = webData.WebPages.Value.FirstOrDefault();

    if (firstWebPagesResult != null)
    {
        Console.WriteLine("Webpage Results # {0}", webData.WebPages.Value.Count);
        Console.WriteLine("First web page name: {0} ", firstWebPagesResult.Name);
        Console.WriteLine("First web page URL: {0} ", firstWebPagesResult.Url);
    }
    else
    {
        Console.WriteLine("Didn't find any web pages...");
    }
}
else
{
    Console.WriteLine("Didn't find any web pages...");
}

/*
 * Images
 * If the search response contains images, the first result's name
 * and url are printed.
 */
if (webData?.Images?.Value?.Count > 0)
{
    // find the first image result
    var firstImageResult = webData.Images.Value.FirstOrDefault();

    if (firstImageResult != null)
    {
        Console.WriteLine("Image Results # {0}", webData.Images.Value.Count);
        Console.WriteLine("First Image result name: {0} ", firstImageResult.Name);
        Console.WriteLine("First Image result URL: {0} ", firstImageResult.ContentUrl);
    }
    else
    {
        Console.WriteLine("Didn't find any images...");
    }
}
else
{
    Console.WriteLine("Didn't find any images...");
}

/*
 * News
 * If the search response contains news articles, the first result's name
 * and url are printed.
 */
if (webData?.News?.Value?.Count > 0)
{
    // find the first news result
    var firstNewsResult = webData.News.Value.FirstOrDefault();

    if (firstNewsResult != null)
    {
        Console.WriteLine("\r\nNews Results # {0}", webData.News.Value.Count);
        Console.WriteLine("First news result name: {0} ", firstNewsResult.Name);
        Console.WriteLine("First news result URL: {0} ", firstNewsResult.Url);
    }
    else
    {
        Console.WriteLine("Didn't find any news articles...");
    }
}
else
{
    Console.WriteLine("Didn't find any news articles...");
}

/*
 * Videos
 * If the search response contains videos, the first result's name
 * and url are printed.
 */
if (webData?.Videos?.Value?.Count > 0)
{
    // find the first video result
    var firstVideoResult = webData.Videos.Value.FirstOrDefault();

    if (firstVideoResult != null)
    {
        Console.WriteLine("\r\nVideo Results # {0}", webData.Videos.Value.Count);
        Console.WriteLine("First Video result name: {0} ", firstVideoResult.Name);
        Console.WriteLine("First Video result URL: {0} ", firstVideoResult.ContentUrl);
    }
    else
    {
        Console.WriteLine("Didn't find any videos...");
    }
}
else
{
    Console.WriteLine("Didn't find any videos...");
}
```

## <a name="declare-the-main-method"></a>main 메서드 선언

이 응용 프로그램에서 main 메서드는 클라이언트를 인스턴스화하고, `subscriptionKey`의 유효성을 검사하고, `WebResults`를 호출하는 코드를 포함합니다. 계속하기 전에 Azure 계정에 유효한 구독 키를 입력했는지 확인합니다.

```csharp
static void Main(string[] args)
{
    var client = new WebSearchAPI(new ApiKeyServiceClientCredentials("YOUR_SUBSCRIPTION_KEY"));

    WebResults(client);

    Console.WriteLine("Press any key to exit...");
    Console.ReadKey();
}
```

## <a name="run-the-application"></a>응용 프로그램 실행

응용 프로그램을 실행해 보겠습니다!

```console
dotnet run
```

## <a name="define-functions-and-filter-results"></a>함수 정의 및 결과 필터링

이제 Bing Web Search API에 대한 첫 번째 호출이 수행되었으므로 SDK 기능을 강조 표시하여 쿼리를 구체화하고 결과를 필터링하는 몇 가지 함수를 살펴보겠습니다. 각 함수는 이전 섹션에서 만든 C# 응용 프로그램에 추가할 수 있습니다.

### <a name="limit-the-number-of-results-returned-by-bing"></a>Bing에서 반환하는 결과 수 제한

이 샘플에서는 `count` 및 `offset` 매개 변수를 사용하여 "Best restaurants in Seattle(시애틀 최고의 레스토랑)"로 반환되는 결과의 수를 제한합니다. 첫 번째 결과에 대한 `name` 및 `URL`이 출력됩니다.

1. 이 코드를 콘솔 프로젝트에 추가합니다.
    ```csharp
    public static void WebResultsWithCountAndOffset(WebSearchAPI client)
    {
        try
        {
            var webData = client.Web.SearchAsync(query: "Best restaurants in Seattle", offset: 10, count: 20).Result;
            Console.WriteLine("\r\nSearching for \" Best restaurants in Seattle \"");

            if (webData?.WebPages?.Value?.Count > 0)
            {
                var firstWebPagesResult = webData.WebPages.Value.FirstOrDefault();

                if (firstWebPagesResult != null)
                {
                    Console.WriteLine("Web Results #{0}", webData.WebPages.Value.Count);
                    Console.WriteLine("First web page name: {0} ", firstWebPagesResult.Name);
                    Console.WriteLine("First web page URL: {0} ", firstWebPagesResult.Url);
                }
                else
                {
                    Console.WriteLine("Couldn't find first web result!");
                }
            }
            else
            {
                Console.WriteLine("Didn't see any Web data..");
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine("Encountered exception. " + ex.Message);
        }
    }
    ```
2. `WebResultsWithCountAndOffset`을 `main`에 추가합니다.
    ```csharp
    static void Main(string[] args)
    {
        var client = new WebSearchAPI(new ApiKeyServiceClientCredentials("YOUR_SUBSCRIPTION_KEY"));

        WebResults(client);
        // Search with count and offset...
        WebResultsWithCountAndOffset(client);  

        Console.WriteLine("Press any key to exit...");
        Console.ReadKey();
    }
    ```
3. 응용 프로그램을 실행합니다.

### <a name="filter-for-news"></a>뉴스에 대한 필터링

이 샘플에서는 `response_filter` 매개 변수를 사용하여 검색 결과를 필터링합니다. 반환되는 검색 결과는 "Microsoft"에 대한 뉴스 기사로 제한됩니다. 첫 번째 결과에 대한 `name` 및 `URL`이 출력됩니다.

1. 이 코드를 콘솔 프로젝트에 추가합니다.
    ```csharp
    public static void WebSearchWithResponseFilter(WebSearchAPI client)
    {
        try
        {
            IList<string> responseFilterstrings = new List<string>() { "news" };
            var webData = client.Web.SearchAsync(query: "Microsoft", responseFilter: responseFilterstrings).Result;
            Console.WriteLine("\r\nSearching for \" Microsoft \" with response filter \"news\"");

            if (webData?.News?.Value?.Count > 0)
            {
                var firstNewsResult = webData.News.Value.FirstOrDefault();

                if (firstNewsResult != null)
                {
                    Console.WriteLine("News Results #{0}", webData.News.Value.Count);
                    Console.WriteLine("First news result name: {0} ", firstNewsResult.Name);
                    Console.WriteLine("First news result URL: {0} ", firstNewsResult.Url);
                }
                else
                {
                    Console.WriteLine("Couldn't find first News results!");
                }
            }
            else
            {
                Console.WriteLine("Didn't see any News data..");
            }

        }
        catch (Exception ex)
        {
            Console.WriteLine("Encountered exception. " + ex.Message);
        }
    }
    ```
2. `WebResultsWithCountAndOffset`을 `main`에 추가합니다.
    ```csharp
    static void Main(string[] args)
    {
        var client = new WebSearchAPI(new ApiKeyServiceClientCredentials("YOUR_SUBSCRIPTION_KEY"));

        WebResults(client);
        // Search with count and offset...
        WebResultsWithCountAndOffset(client);  
        // Search with news filter...
        WebSearchWithResponseFilter(client);

        Console.WriteLine("Press any key to exit...");
        Console.ReadKey();
    }
    ```
3. 응용 프로그램을 실행합니다.

### <a name="use-safe-search-answer-count-and-the-promote-filter"></a>안전 검색, 응답 수 및 승격 필터 사용

이 샘플에서는 `answer_count`, `promote` 및 `safe_search` 매개 변수를 사용하여 "Music Videos(뮤직 비디오)"에 대한 검색 결과를 필터링합니다. 첫 번째 결과에 대한 `name` 및 `URL`이 표시됩니다.

1. 이 코드를 콘솔 프로젝트에 추가합니다.
    ```csharp
    public static void WebSearchWithAnswerCountPromoteAndSafeSearch(WebSearchAPI client)
    {
        try
        {
            IList<string> promoteAnswertypeStrings = new List<string>() { "videos" };
            var webData = client.Web.SearchAsync(query: "Music Videos", answerCount: 2, promote: promoteAnswertypeStrings, safeSearch: SafeSearch.Strict).Result;
            Console.WriteLine("\r\nSearching for \"Music Videos\"");

            if (webData?.Videos?.Value?.Count > 0)
            {
                var firstVideosResult = webData.Videos.Value.FirstOrDefault();

                if (firstVideosResult != null)
                {
                    Console.WriteLine("Video Results # {0}", webData.Videos.Value.Count);
                    Console.WriteLine("First Video result name: {0} ", firstVideosResult.Name);
                    Console.WriteLine("First Video result URL: {0} ", firstVideosResult.ContentUrl);
                }
                else
                {
                    Console.WriteLine("Couldn't find videos results!");
                }
            }
            else
            {
                Console.WriteLine("Didn't see any data..");
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine("Encountered exception. " + ex.Message);
        }
    }
    ```
2. `WebResultsWithCountAndOffset`을 `main`에 추가합니다.
    ```csharp
    static void Main(string[] args)
    {
        var client = new WebSearchAPI(new ApiKeyServiceClientCredentials("YOUR_SUBSCRIPTION_KEY"));

        WebResults(client);
        // Search with count and offset...
        WebResultsWithCountAndOffset(client);  
        // Search with news filter...
        WebSearchWithResponseFilter(client);
        // Search with answer count, promote, and safe search
        WebSearchWithAnswerCountPromoteAndSafeSearch(client);

        Console.WriteLine("Press any key to exit...");
        Console.ReadKey();
    }
    ```
3. 응용 프로그램을 실행합니다.

## <a name="clean-up-resources"></a>리소스 정리

이 프로젝트가 완료되면 응용 프로그램의 코드에서 구독 키를 제거해야 합니다.

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [Cognitive Services Node.js SDK 샘플](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/)
