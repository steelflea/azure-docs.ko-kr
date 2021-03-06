---
title: 모범 사례 - QnA Maker
titlesuffix: Azure Cognitive Services
description: 모범 사례를 사용하여 기술 자료를 개선하고 응용 프로그램/챗봇 최종 사용자에게 보다 나은 결과를 제공할 수 있습니다.
services: cognitive-services
author: tulasim88
manager: cgronlun
ms.service: cognitive-services
ms.component: qna-maker
ms.topic: article
ms.date: 09/24/2018
ms.author: tulasim
ms.openlocfilehash: cb171a666a4a54660a3bf54b8f26aed23f60d249
ms.sourcegitcommit: 4ecc62198f299fc215c49e38bca81f7eb62cdef3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2018
ms.locfileid: "47036306"
---
# <a name="best-practices"></a>모범 사례
[기술 자료 개발 수명 주기](../Concepts/development-lifecycle-knowledge-base.md)에서는 KB를 종합적으로 관리하는 방법을 안내합니다. 모범 사례를 사용하여 기술 자료를 개선하고 응용 프로그램/챗봇 최종 사용자에게 보다 나은 결과를 제공할 수 있습니다.

## <a name="extraction"></a>추출
QnA Maker 서비스는 콘텐츠에서 QnA를 추출하고 지원되는 파일 및 HTML 형식 목록을 확장하는 알고리즘을 지속적으로 개선하고 있습니다. 문서 형식에 따라 데이터 추출에 대한 [지침](../Concepts/data-sources-supported.md)을 수행합니다. 

일반적으로 FAQ 페이지는 독립 실행형이어야 하며, 다른 정보와 결합되지 않아야 합니다. 제품 설명서는 제목에 명확해야 하고 인덱스 페이지까지 명확하면 더욱 좋습니다. 

## <a name="chit-chat"></a>잠답
봇에 잡담을 추가하여 적은 노력으로 봇을 대화형이고 몰입도 높게 만듭니다. KB를 만들 때 미리 정의된 3가지 개성에 대한 잡담 데이터 집합을 추가하고 언제든지 변경할 수 있습니다. [KB에 잡담을 추가](../How-To/chit-chat-knowledge-base.md)하는 방법을 알아봅니다. 

### <a name="choosing-a-personality"></a>개성 선택
미리 정의된 3가지 개성에 잡담이 지원됩니다. 

|개성|
|--|
|전문가|
|친구|
|재미|

응답은 격식체에서 비격식체의 범위까지 지정됩니다. 봇에 원하는 어조와 가장 가깝게 맞춰진 개성을 선택해야 합니다. 데이터 집합을 보고, 봇에 대한 기준으로 사용되는 데이터 집합을 선택한 다음, 응답을 사용자 지정할 수 있습니다. 

### <a name="edit-bot-specific-questions"></a>봇 관련 질문 편집
잠답 데이터 집합의 일부이며 일반 답변으로 채워진 몇 가지 봇 관련 질문이 있습니다. 이 대답을 변경하여 봇 세부 정보를 가장 잘 반영합니다. 

잡담 QnA를 구체적으로 만드는 것이 좋습니다.

* 당신은 누구인가요?
* 어떻게 해야 합니까?
* 나이가 어떻게 되세요?
* 만든 사람은 누구인가요?
* 안녕하세요.
   

## <a name="rankingscoring"></a>순위 지정/채점
QnA Maker가 지원하는 순위 기능을 최대로 활용하시기 바랍니다. 그러면 특정 사용자 쿼리에 적절하게 답변할 가능성이 높아집니다.

### <a name="choosing-a-threshold"></a>임계값 선택
임계값으로 사용되는 기본 신뢰성 점수는 50이지만 필요에 따라 KB에 대해 변경할 수 있습니다. 모든 KB가 다르므로 KB에 가장 적합한 임계값을 에 테스트하고 선택해야 합니다. [신뢰성 점수](../Concepts/confidence-score.md)에 대해 자세히 알아봅니다. 


### <a name="add-alternate-questions"></a>대체 질문 추가
[대체 질문](../How-To/edit-knowledge-base.md)은 사용자 쿼리와 일치할 가능성을 높입니다. 대체 질문은 같은 질문을 여러 가지 방식으로 받을 수 있는 경우에 유용합니다. 여기에는 문장 구조 및 단어 스타일 변경이 포함됩니다.

|원래 쿼리|대체 쿼리|변경| 
|--|--|--|
|주차 가능하나요?|주차장이 있나요?|문장 구조|
 |Hi|Yo<br>Hey there!|단어 스타일 또는 속어|

### <a name="use-metadata-filters"></a>메타데이터 필터 사용
[메타데이터](../How-To/edit-knowledge-base.md)는 필터에 따라 사용자 쿼리 결과를 줄일 수 있는 기능을 추가합니다. 쿼리가 같더라도 메타데이터 태그에 따라 기술 자료 답변이 달라질 수 있습니다. 예를 들어 식당 지점의 위치가 다르면 *"주차장 위치는 어디인가요"* 에 대한 대답이 달라질 수 있습니다. 즉, 메타데이터는 *위치: 시애틀* 또는 *위치: 레드몬드*입니다.

### <a name="use-synonyms"></a>동의어 사용
영어에서는 동의어에 대한 지원이 일부 제공되므로 [단어 변경](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75fd)을 사용하여 다른 형식의 키워드에 동의어를 추가할 수 있습니다. 동의어는 QnA Maker 서비스 수준에서 추가하고 서비스의 모든 기술 자료에서 공유해야 합니다.

|원래 단어|동의어|
|--|--|
|구입|구매<br>인터넷 뱅킹<br>인터넷 뱅킹|

### <a name="use-distinct-words-to-differentiate-questions"></a>고유한 단어를 사용하여 질문을 구분
사용자 쿼리를 기술 자료의 질문과 일치시키는 QnA Maker 일치-순위 알고리즘은 각 질문이 여러 요구 사항을 해결하는 경우에 가장 적합합니다. 질문 사이에 같은 단어 집합을 반복하면 해당 단어가 포함된 특정 사용자 쿼리에 대해 올바른 대답이 선택될 확률이 감소합니다. 

예를 들어, 다음과 같은 질문을 사용하여 두 개의 별도 QnA가 있을 수 있습니다.

|QnA|
|--|
|주차 *위치*는 어디인가요|
|ATM *위치*는 어디인가요|

이러한 두 QnA가 매우 유사한 단어로 구성되었으므로 이 유사성은 *"`<x>`위치는 어디인가요"* 와 같이 구성된 사용자 쿼리에 대해 유사한 점수가 발생할 수 있습니다. 대신, KB의 많은 질문에 포함된 "위치"와 같은 단어를 방지하여 *"주차장은 어디인가요"* 및 *"ATM은 어디인가요"* 와 같은 쿼리와 명확하게 구분하려고 합니다. 


## <a name="collaborate"></a>공동 작업
QnA Maker를 통해 사용자들이 기술 자료를 [공동으로 작업](../How-to/collaborate-knowledge-base.md)할 수 있습니다. 사용자는 기술 자료에 액세스하기 위해 Azure QnA Maker 리소스 그룹에 대한 액세스 권한이 필요합니다. 기술 자료 편집 및 유지 관리를 아웃소싱하려는 조직도 있을 것이며, 이 경우에도 여전히 Azure 리소스에 대한 액세스를 보호할 수 있습니다. 이 편집자-승인자 모델은 서로 다른 구독에 최대 2개의 동일한 [QnA Maker 서비스](../How-to/set-up-qnamaker-service-azure.md)를 설정하고 하나를 편집-테스트 주기용으로 지정하여 수행할 수 있습니다. 테스트가 완료되면 [가져오기-내보내기](../Tutorials/migrate-knowledge-base.md) 프로세스를 사용하여 최종적으로 기술 자료를 게시하고 엔드포인트를 업데이트하는 승인자의 QnA Maker 서비스로 기술 자료 콘텐츠를 전송할 수 있습니다.

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [기술 자료 편집](../How-to/edit-knowledge-base.md)
