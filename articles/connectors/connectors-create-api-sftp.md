---
title: SFTP 계정에 연결 - Azure Logic Apps | Microsoft Docs
description: Azure Logic Apps를 사용하여 SSH를 통해 SFTP 서버에 대한 파일을 모니터링, 만들기, 관리, 전송 및 수신하는 작업 및 프로세스 자동화
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: ecfan
ms.author: estfan
ms.reviewer: divswa, klam, LADocs
ms.assetid: 697eb8b0-4a66-40c7-be7b-6aa6b131c7ad
ms.topic: article
tags: connectors
ms.date: 10/26/2018
ms.openlocfilehash: 3dbe40476757ba93f33d39f71c46bf58302b3570
ms.sourcegitcommit: 1fc949dab883453ac960e02d882e613806fabe6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/03/2018
ms.locfileid: "50979457"
---
# <a name="monitor-create-and-manage-sftp-files-by-using-azure-logic-apps"></a>Azure Logic Apps를 사용하여 SFTP 파일 모니터링, 만들기 및 관리

[SFTP(보안 파일 전송 프로토콜)](https://www.ssh.com/ssh/sftp/) 서버에서 파일을 모니터링, 만들기, 전송 및 수신하는 작업을 자동화하려면 Azure Logic Apps 및 SFTP 커넥터를 사용하여 통합 워크플로를 빌드하고 자동화할 수 있습니다. SFTP는 신뢰할 수 있는 데이터 스트림을 통해 파일 액세스, 파일 전송 및 파일 관리를 제공하는 네트워크 프로토콜입니다. 다음은 자동화할 수 있는 몇 가지 예제 작업입니다. 

* 파일이 추가되거나 변경될 때 모니터링합니다.
* 파일을 가져오고, 만들고, 복사, 업데이트, 나열 및 삭제합니다.
* 파일 콘텐츠 및 메타데이터를 가져옵니다.
* 보관을 폴더로 추출합니다.

[SFTP-SSH 커넥터](../connectors/connectors-sftp-ssh.md)에 비교하여 SFTP 커넥터는 [큰 메시지 처리를 위한 청크](../logic-apps/logic-apps-handle-large-messages.md)를 사용하지 않는 한 최대 50MB 크기의 파일을 읽거나 쓸 수 있습니다. 최대 1GB 크기 파일의 경우 [SFTP-SSH 커넥터](../connectors/connectors-sftp-ssh.md)를 사용합니다. 1GB보다 큰 파일의 경우 SFTP-SSH 커넥터와 [큰 메시지에 대한 청크](../logic-apps/logic-apps-handle-large-messages.md)를 사용할 수 있습니다. 

SFTP 서버에서 이벤트를 모니터링하는 트리거를 사용하고 다른 작업에서 출력을 사용하도록 할 수 있습니다. SFTP 서버에서 다양한 작업을 수행하는 작업을 사용할 수 있습니다. 또한 논리 앱의 다른 작업에서 SFTP 작업의 출력을 사용하도록 할 수 있습니다. 예를 들어 정기적으로 SFTP 서버에서 파일을 검색하는 경우 Office 365 Outlook 커넥터 또는 Outlook.com 커넥터를 사용하여 해당 파일 및 해당 콘텐츠에 대한 이메일 경고를 보낼 수 있습니다.
논리 앱을 처음 접하는 경우 [Azure Logic Apps란?](../logic-apps/logic-apps-overview.md)을 검토합니다.

## <a name="prerequisites"></a>필수 조건

* Azure 구독. Azure 구독이 없는 경우 <a href="https://azure.microsoft.com/free/" target="_blank">체험 Azure 계정에 등록</a>합니다. 

* 논리 앱에서 SFTP 계정에 액세스하도록 하는 SFTP 서버 주소 및 계정 자격 증명 [SSH(Secure Shell)](https://www.ssh.com/ssh/protocol/) 프로토콜을 사용하려면 SSH 개인 키 및 SSH 개인 키 암호에 대한 액세스도 필요합니다. 

  > [!NOTE]
  > 
  > SFTP 커넥터는 OpenSSH, ssh.com 및 PuTTY와 같은 개인 키 형식을 지원합니다.
  > 
  > 논리 앱을 만들 때 원하는 SFTP 트리거 또는 작업을 추가한 후 SFTP 서버에 대한 연결 정보를 제공해야 합니다. 
  > SSH 개인 키를 사용하는 경우 SSH 개인 키 파일에서 키를 ***복사***하고, 해당 키를 연결 세부 정보에 ***붙여넣었는지*** 확인합니다. ***키를 수동으로 입력하거나 편집하지 마십시오***. 연결 실패가 발생할 수 있습니다. 
  > 자세한 내용은 이 문서의 뒷부분에 나오는 단계를 참조하세요.

* [논리 앱 만드는 방법](../logic-apps/quickstart-create-first-logic-app-workflow.md)에 관한 기본 지식

* SFTP 계정에 액세스하려는 논리 앱입니다. SFTP 트리거를 시작하려면 [빈 논리 앱을 만듭니다](../logic-apps/quickstart-create-first-logic-app-workflow.md). SFTP 동작을 사용하려면 예를 들어 **되풀이** 트리거 같은 다른 트리거를 통해 논리 앱을 시작합니다.

## <a name="connect-to-sftp"></a>SFTP에 연결

[!INCLUDE [Create connection general intro](../../includes/connectors-create-connection-general-intro.md)]

1. [Azure Portal](https://portal.azure.com)에 로그인하고, 아직 열리지 않은 경우 Logic App Designer에서 논리 앱을 엽니다.

1. 빈 논리 앱의 경우 검색 상자에서 필터로 “sftp”를 입력합니다. 트리거 목록에서 원하는 트리거를 선택합니다. 

   또는

   기존 논리 앱의 경우 작업을 추가하려는 마지막 단계에서 **새 단계**를 선택합니다. 
   검색 상자에서 필터로 “sftp”를 입력합니다. 
   작업 목록에서 원하는 작업을 선택합니다.

   단계 사이에서 작업을 추가하려면 단계 사이에 있는 화살표 위로 포인터를 이동합니다. 
   표시되는 더하기 기호(**+**)를 선택한 다음, **작업 추가**를 선택합니다.

1. 연결에 필요한 정보를 입력합니다.

   > [!IMPORTANT] 
   >
   > **SSH 개인 키** 속성에 SSH 개인 키를 입력할 때 이 속성에 대한 완전하고 올바른 값을 제공하는 데 도움이 되는 다음 추가 단계를 수행합니다. 
   > 잘못된 키로 인해 연결 실패가 발생합니다.
   
   모든 텍스트 편집기를 사용할 수 있지만 예를 들어 Notepad.exe를 사용하여 키를 올바르게 복사하고 붙여넣는 방법을 보여주는 샘플 단계는 다음과 같습니다.
    
   1. 텍스트 편집기에서 SSH 개인 키 파일을 엽니다. 
   이러한 단계는 예제로 메모장을 사용합니다.

   1. 메모장의 **편집** 메뉴에서 **모두 선택**을 선택합니다.

   1. **편집** > **복사**를 선택합니다.

   1. 추가한 SFTP 트리거 또는 작업에서 **SSH 개인 키** 속성으로 복사한 *전체* 키를 붙여넣습니다. 이는 여러 줄을 지원합니다. 
   키를 ***붙여넣었는지 확인합니다***. ***키를 수동으로 입력하거나 편집하지 마십시오***.

1. 연결 세부 정보 입력이 완료되면 **만들기**를 선택합니다.

1. 선택한 트리거 또는 작업에 대해 필요한 세부 정보를 제공하고 논리 앱의 워크플로를 계속 빌드합니다.

## <a name="trigger-limits"></a>트리거 제한

SFTP 트리거는 SFTP 파일 시스템을 폴링하여 마지막 폴링 이후 변경된 파일을 찾는 방식으로 작동합니다. 일부 도구를 통해 파일을 변경하는 경우 타임스탬프를 유지할 수 있습니다. 이러한 경우 트리거가 작동할 수 있도록 이 기능을 사용하지 않도록 설정해야 합니다. 아래에는 몇 가지 일반적인 설정이 나와 있습니다.

| SFTP 클라이언트 | 조치 | 
|-------------|--------| 
| Winscp | **옵션** > **기본 설정** > **전송** > **편집** > **타임스탬프 보존** > **사용 안 함**으로 이동 |
| FileZilla | **전송** > **전송된 파일의 타임스탬프 보존** > **사용 안 함**으로 이동 | 
||| 

트리거는 새 파일을 찾으면 해당 파일이 완전한 상태이며 부분적으로 작성된 것이 아닌지 확인합니다. 예를 들어 트리거가 파일 서버를 확인할 때 파일을 변경하는 중일 수 있습니다. 부분적으로 작성된 파일이 반환되지 않도록 하기 위해 트리거는 최근 변경된 내용이 있는 파일의 타임스탬프를 기록하되 해당 파일을 즉시 반환하지는 않으며, 서버를 다시 폴링할 때만 해당 파일을 반환합니다. 이 동작으로 인해 트리거 폴링 간격의 최대 2배까지 지연이 발생하는 경우도 있습니다. 

## <a name="examples"></a>예

### <a name="sftp-trigger-when-a-file-is-added-or-modified"></a>SFTP 트리거: 파일이 추가되거나 수정되는 경우

이 트리거는 SFTP 서버에서 파일이 추가되거나 변경되는 경우 논리 앱 워크플로를 시작합니다. 예를 들어 콘텐츠가 지정된 조건을 충족하는지 여부에 따라 파일의 콘텐츠를 확인하고 콘텐츠를 가져오는 조건을 추가할 수 있습니다. 그런 다음, 파일의 콘텐츠를 가져오고 해당 콘텐츠를 SFTP 서버의 폴더에 넣는 작업을 추가할 수 있습니다. 

**엔터프라이즈 예제**: 이 트리거를 사용하여 고객의 주문을 나타내는 새 파일에 대한 SFTP 폴더를 모니터링할 수 있습니다. 그런 다음, **파일 콘텐츠 가져오기**와 같은 SFTP 작업을 사용할 수 있으므로 추가로 처리할 주문의 콘텐츠를 가져오고 주문 데이터베이스에 해당 주문을 저장합니다.

### <a name="sftp-action-get-content"></a>SFTP 작업: 콘텐츠 가져오기

이 작업은 SFTP 서버의 파일에서 콘텐츠를 가져옵니다. 따라서 예를 들어 이전 예제의 트리거와 파일의 콘텐츠가 충족해야 하는 조건을 추가할 수 있습니다. 조건이 true인 경우 콘텐츠를 가져오는 작업을 실행할 수 있습니다. 

## <a name="connector-reference"></a>커넥터 참조

커넥터의 OpenAPI(이전의 Swagger) 설명서에 설명된 트리거, 작업 및 제한에 대한 기술 정보는 커넥터의 [참조 페이지](/connectors/sftpconnector/)를 검토하세요.

## <a name="get-support"></a>지원 받기

* 질문이 있는 경우 [Azure Logic Apps 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)을 방문해 보세요.
* 기능 아이디어를 제출하거나 투표하려면 [Logic Apps 사용자 의견 사이트](https://aka.ms/logicapps-wish)를 방문하세요.

## <a name="next-steps"></a>다음 단계

* 다른 [Logic Apps 커넥터](../connectors/apis-list.md)에 대해 알아봅니다.