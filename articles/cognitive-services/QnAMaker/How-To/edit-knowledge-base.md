---
title: 기술 자료 편집 - QnA Maker
titleSuffix: Azure Cognitive Services
description: QnA Maker는 사용하기 쉬운 편집 환경을 제공하여 기술 자료 콘텐츠를 관리할 수 있게 해줍니다.
services: cognitive-services
author: tulasim88
manager: cgronlun
ms.service: cognitive-services
ms.component: qna-maker
ms.topic: article
ms.date: 11/06/2018
ms.author: tulasim
ms.openlocfilehash: adcefe8fed927aca2533ea811bac56f0b92288de
ms.sourcegitcommit: ba4570d778187a975645a45920d1d631139ac36e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/08/2018
ms.locfileid: "51279764"
---
# <a name="edit-a-knowledge-base"></a>기술 자료 편집

QnA Maker는 사용하기 쉬운 편집 환경을 제공하여 기술 자료 콘텐츠를 관리할 수 있게 해줍니다.

## <a name="edit-your-knowledge-base-content"></a>기술 자료 콘텐츠 편집

1.  맨 위 탐색 모음에서 **내 기술 자료**를 선택합니다. 

    직접 만들었거나 공유된 모든 서비스를 **마지막으로 수정한 날짜**의 내림차순으로 볼 수 있습니다.

    ![내 기술 자료](../media/qnamaker-how-to-edit-kb/my-kbs.png)

2. 특정 기술 자료를 선택하여 편집합니다.
 
3. **설정**을 클릭합니다.

   여기에서 필수 필드인 서비스 이름을 편집할 수 있습니다.
  
   **기술 자료 관리 -> '+ URL 추가'** 링크를 클릭하여 기술 자료에 새 FAQ 콘텐츠를 추가할 새 URL을 추가할 수 있습니다.
   
   **삭제 아이콘**을 클릭하여 기존 URL을 삭제할 수 있습니다.
   
   기술 자료에서 기존 URL의 최신 콘텐츠를 크롤링하려는 경우 확인란 이름 **'새로 고침'** 을 클릭합니다. 그러면 기술 자료를 최신 URL 콘텐츠로 업데이트합니다.
   
**기술 자료 관리 -> '+파일 추가'** 를 클릭하여 지원되는 파일 문서를 기술 자료의 일부로 추가할 수 있습니다.

**'기술 자료 가져오기'** 단추를 클릭하여 기존 기술 자료를 가져올 수도 있습니다. 
   
기술 자료의 업데이트는 기술 자료와 관련된 QnA Maker 서비스를 만드는 동안 사용되는 **관리 가격 책정 계층**에 따라 달라집니다. 필요한 경우 Azure Portal에서 관리 계층을 업데이트할 수도 있습니다.

4. 기술 자료 변경을 마쳤으면 변경 내용을 유지하기 위해 페이지의 오른쪽 맨 위에 있는 **저장 후 학습**을 클릭합니다.    

    ![저장 후 학습](../media/qnamaker-how-to-edit-kb/save-and-train.png)

    >[!NOTE]
    저장 후 학습을 클릭하기 전에 페이지를 닫으면 변경 내용이 유지되지 않습니다.

## <a name="add-a-qna-pair"></a>QnA 쌍 추가

**QnA 쌍 추가**를 선택하여 기술 자료 표에 새 행을 추가합니다.

![QnA 쌍 추가](../media/qnamaker-how-to-edit-kb/add-qnapair.png)

## <a name="delete-a-qna-pair"></a>QnA 쌍 삭제

QnA를 삭제하려면 QnA 행의 맨 오른쪽에 있는 **삭제** 아이콘을 클릭합니다.

![QnA 쌍 삭제](../media/qnamaker-how-to-edit-kb/delete-qnapair.png)

## <a name="add-alternate-questions"></a>대체 질문 추가

기존 QnA 쌍에 대체 질문을 추가하여 사용자 쿼리와 일치할 가능성을 높입니다.

![대체 질문 추가](../media/qnamaker-how-to-edit-kb/add-alternate-question.png)

## <a name="add-metadata"></a>메타데이터 추가


필터 아이콘을 선택하여 메타데이터 쌍을 추가합니다.

![메타데이터 추가](../media/qnamaker-how-to-edit-kb/add-metadata.png)

> [!TIP]
> 변경 내용이 손실되지 않도록 하려면 편집한 후 기술 자료를 주기적으로 저장하고 학습해야 합니다.

## <a name="manage-large-knowledge-bases"></a>큰 기술 자료 관리

1. QnA는 추출된 데이터 원본에 따라 **그룹화**됩니다. 데이터 원본을 확장하거나 축소할 수 있습니다.
2. 기술 자료 표의 맨 위에 있는 텍스트 상자에 입력하여 기술 자료를 **검색**할 수 있습니다. 질문, 답변 또는 메타데이터 콘텐츠를 검색하려면 Enter 키를 누릅니다. 검색 필터를 제거하려면 X 아이콘을 클릭합니다.
3. **페이지 매김**을 사용하면 큰 기술 자료를 관리할 수 있습니다.

    ![검색, 페이지 매김, 그룹화](../media/qnamaker-how-to-edit-kb/search-paginate-group.png)

## <a name="delete-knowledge-bases"></a>기술 자료 삭제

KB(기술 자료)를 삭제하는 것은 영구 작업입니다. 실행을 취소할 수 없습니다. 기술 자료를 삭제하기 전에 QnA Maker 포털의 **설정** 페이지에서 기술 자료를 내보내야 합니다. 

[협력자](collaborate-knowledge-base.md)와 KB를 공유한 다음, 삭제하는 경우 모든 사용자가 KB에 액세스할 수 없습니다. 

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [기술 자료에 대한 공동 작업](./collaborate-knowledge-base.md)
