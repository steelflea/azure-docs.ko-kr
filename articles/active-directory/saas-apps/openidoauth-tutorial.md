---
title: Azure AD 앱 갤러리에서 OpenID/OAuth 응용 프로그램 구성 | Microsoft Docs
description: Azure AD 앱 갤러리에서 OpenID/OAuth 응용 프로그램을 구성하는 단계
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: eedebb76-e78c-428f-9cf0-5891852e79fb
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2018
ms.author: jeedes
ms.openlocfilehash: 04639e6d27854d9c25b97936b163cfaaa25fc375
ms.sourcegitcommit: 02ce0fc22a71796f08a9aa20c76e2fa40eb2f10a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/08/2018
ms.locfileid: "51287441"
---
# <a name="configure-an-openidoauth-application-from-the-azure-ad-app-gallery"></a>Azure AD 앱 갤러리에서 OpenID/OAuth 응용 프로그램 구성

## <a name="process-of-adding-an-openid-application-from-the-gallery"></a>갤러리에서 OpenID 응용 프로그램을 추가하는 프로세스

1. [Azure Portal](https://portal.azure.com)의 왼쪽 창에서 **Azure Active Directory**를 선택합니다. 

    ![Azure Active Directory 단추](./media/openidoauth-tutorial/tutorial_general_01.png)

2. **Enterprise 응용 프로그램** > **모든 응용 프로그램**으로 이동합니다.

    ![엔터프라이즈 응용 프로그램 블레이드](./media/openidoauth-tutorial/tutorial_general_02.png)

3. 대화 상자 맨 위 있는 **새 응용 프로그램**을 선택합니다.

    ![새 응용 프로그램 단추](./media/openidoauth-tutorial/tutorial_general_03.png)

4. 검색 상자에 응용 프로그램 이름을 입력합니다. 결과 패널에서 원하는 응용 프로그램을 선택하고, 응용 프로그램에 로그인합니다.

    ![응용 프로그램 추가](./media/openidoauth-tutorial/addfromgallery.png)

    > [!NOTE]
    > OpenID Connect 및 OAuth 앱의 경우 **추가** 단추가 기본적으로 비활성화됩니다. 여기에서 테넌트 관리자는 등록 단추를 선택하고 응용 프로그램에 대한 동의를 제공해야 합니다. 그러면 구성을 수행할 수 있는 고객 테넌트에 응용 프로그램이 추가됩니다. 응용 프로그램을 명시적으로 추가할 필요가 없습니다.

    ![추가 단추](./media/openidoauth-tutorial/addbutton.png)

5. 등록 링크를 선택하면 로그인 자격 증명에 대한 Azure AD(Azure Active Directory) 페이지로 리디렉션됩니다.

6. 인증이 성공하면 동의 페이지에서 동의를 승인합니다. 그런 다음, 응용 프로그램 홈페이지가 표시됩니다.

    > [!NOTE]
    > 응용 프로그램의 인스턴스를 하나만 추가할 수 있습니다. 이미 인스턴스를 추가하고 다시 동의하려고 하는 경우 테넌트에 추가되지 않습니다. 따라서 논리적으로 테넌트에서 하나의 앱 인스턴스만을 사용할 수 있습니다.

## <a name="authentication-flow-using-openid-connect"></a>OpenID Connect를 사용하는 인증 흐름

가장 기본적인 로그인 흐름은 다음 단계를 포함합니다.

![OpenID Connect를 사용하는 인증 흐름](./media/openidoauth-tutorial/authenticationflow.png)

### <a name="multitenant-application"></a>다중 테넌트 응용 프로그램 
다중 테넌트 응용 프로그램은 하나의 조직이 아니라 많은 조직에서 사용하기 위한 것입니다. 일반적으로 ISV(Independent Software Vendor)가 작성한 SaaS(Software-as-a-Service) 응용 프로그램이 이에 해당합니다. 

다중 테넌트 응용 프로그램은 사용될 수는 있는 각 디렉터리에 프로비전되어야 합니다. 등록하려면 사용자 또는 관리자 동의가 필요합니다. 이러한 동의 프로세스는 응용 프로그램이 디렉터리에 등록되고 Graph API 또는 다른 웹 API에 대한 액세스 권한이 제공되면 시작됩니다. 다른 조직의 사용자나 관리자가 응용 프로그램을 사용하기 위해 등록할 때는 대화 상자에서 응용 프로그램에서 요구되는 권한을 표시합니다. 

그런 다음, 사용자 또는 관리자는 응용 프로그램에 동의할 수 있습니다. 동의는 명시된 데이터에 대한 응용 프로그램 액세스를 제공하고 마지막으로 디렉터리에 응용 프로그램을 등록합니다.

> [!NOTE]
> 여러 디렉터리에 있는 사용자에게 응용 프로그램을 사용할 수 있도록 만들려면 사용자가 속한 테넌트를 확인할 수 있는 메커니즘이 필요합니다. 단일 테넌트 응용 프로그램은 사용자에 대한 고유한 디렉터리에서 확인해야 합니다. 다중 테넌트 응용 프로그램은 Azure AD의 모든 디렉터리에서 특정 사용자를 식별해야 합니다.
> 
> 이 작업을 수행할 수 있도록 Azure AD는 테넌트 특정 엔드포인트를 제공하지 않고 다중 테넌트 응용 프로그램이 로그인 요청을 디렉션할 수 있는 공통 인증 엔드포인트를 제공합니다. 이 엔드포인트는 Azure AD의 모든 디렉터리에 대한 [https://login.microsoftonline.com/common](https://login.microsoftonline.com/common)입니다. 테넌트별 엔드포인트는 [https://login.microsoftonline.com/contoso.onmicrosoft.com](https://login.microsoftonline.com/contoso.onmicrosoft.com)일 수 있습니다. 
>
> 응용 프로그램을 개발하는 경우 공통 엔드포인트를 고려하는 것은 중요합니다. 로그인, 로그아웃 및 토큰 유효성 검사 중에 여러 테넌트를 처리하는 데 필요한 논리가 필요합니다.

기본적으로 Azure AD는 다중 테넌트 응용 프로그램을 승격합니다. 조직에 쉽게 액세스하며, 동의를 수락한 후 사용하기 쉽습니다.

## <a name="consent-framework"></a>동의 프레임워크

Azure AD 동의 프레임워크를 사용하여 다중 테넌트 웹 및 네이티브 클라이언트 응용 프로그램을 개발할 수 있습니다. 이러한 응용 프로그램을 사용하면 응용 프로그램이 등록되어 있는 계정과 다르게 Azure AD 테넌트의 사용자 계정으로 로그인할 수 있습니다. 다음과 같은 웹 API에 액세스해야 할 수 있습니다.
- Azure AD, Intune 및 Office 365의 서비스에 액세스하기 위한 Microsoft Graph API 
- 기타 Microsoft 서비스의 API
- 사용자 고유의 웹 API 

이 프레임워크는 응용프로그램을 자신의 디렉터리에 등록하는 것에 동의하는 사용자나 관리자를 기반으로 합니다. 등록은 디렉터리 데이터 액세스가 필요할 수도 있습니다. 사용자가 동의해 주면 해당 클라이언트 응용 프로그램에서 사용자를 대신하여 Microsoft Graph API를 호출하고 필요한 대로 정보를 사용할 수 있습니다.

[Microsoft Graph API](https://developer.microsoft.com/graph/)는 Office 365에서 다음과 같은 데이터에 대한 액세스를 제공합니다.

- Exchange의 일정 및 메시지
- SharePoint의 사이트 및 목록
- OneDrive의 문서
- OneNote의 노트북
- Planner의 작업
- Excel의 통합 문서

Graph API는 또한 더 많은 Microsoft 클라우드 서비스에서 사용자 및 그룹에게 Azure AD 및 기타 데이터 개체에 대한 액세스를 제공합니다.

다음 단계는 응용 프로그램 개발자와 사용자에 대해 동의 경험이 어떻게 작동하는지를 보여줍니다.

1. 리소스 또는 API에 액세스할 수 있는 특정 사용 권한을 요청해야 하는 웹 클라이언트 응용 프로그램이 있다고 가정합니다. Azure Portal은 구성 시 권한 요청을 선언하는 데 사용됩니다. 다른 구성 설정과 마찬가지로 응용 프로그램 Azure AD 등록의 일부입니다.

    ![그래프 API](./media/openidoauth-tutorial/graphapi.png)

2. 응용 프로그램의 권한을 업데이트하는 것이 좋습니다. 응용 프로그램이 실행되고 사용자가 처음으로 사용하려고 합니다. 먼저 응용 프로그램은 Azure AD/authorize 엔드포인트에서 권한 부여 코드를 가져와야 합니다. 그런 다음 권한 부여 코드를 사용하여 새로운 액세스 토큰 및 새로 고침 토큰을 획득할 수 있습니다.

3. 사용자가 인증되지 않은 경우 Azure AD/authorize 엔드포인트는 로그인하라는 메시지를 표시합니다.

    ![인증](./media/openidoauth-tutorial/authentication.png)

4. 사용자가 로그인한 후 Azure AD는 사용자를 동의 페이지에 표시해야 하는지 여부를 결정합니다. 이 결정은 사용자(또는 해당 조직의 관리자)가 응용 프로그램 동의를 부여했는지 여부에 따라 다릅니다.

   동의가 부여되지 않았다면 Azure AD는 사용자에게 동의 여부를 묻는 메시지를 표시하며 작동에 필요한 사용 권한을 표시합니다. 동의 대화 상자에 표시되는 사용 권한은 Azure Portal의 위임된 권한에서 선택한 집합과 일치합니다.

    ![동의 페이지](./media/openidoauth-tutorial/consentpage.png)

일반 사용자는 몇 가지 사용 권한에 동의할 수 있습니다. 기타 사용 권한은 테넌트 관리자의 동의를 필요로 합니다.

## <a name="difference-between-admin-consent-and-user-consent"></a>관리자 승인과 사용자 동의 간의 차이

관리자로 테넌트의 모든 사용자를 대신하여 응용 프로그램의 위임된 권한에 동의할 수도 있습니다. 관리 동의는 테넌트의 모든 사용자에게 동의 대화 상자를 표시하지 않도록 방지합니다. 관리자 역할이 있는 사용자는 Azure Portal에서 동의를 제공할 수 있습니다. 응용 프로그램의 **설정** 페이지에서 **필요한 사용 권한** > **권한 부여**를 선택합니다.

![권한 부여 단추](./media/openidoauth-tutorial/grantpermission.png)

> [!NOTE]
> **권한 부여** 단추를 사용하는 명시적 동의 부여는 현재 ADAL.js를 사용하는 SPA(단일 페이지 응용 프로그램)에 필요합니다. 그렇지 않고 액세스 토큰을 요청하는 경우 응용 프로그램이 실패합니다.

응용 프로그램 전용 권한은 테넌트 관리자의 동의를 항상 필요로 합니다. 응용 프로그램이 응용 프로그램 전용 사용 권한을 요청하고 사용자가 응용 프로그램에 로그인을 시도하는 경우 오류 메시지가 나타납니다. 메시지는 사용자가 동의할 수 없음을 알립니다.

응용 프로그램이 관리자 동의가 필요한 권한을 사용할 경우 관리자가 작업을 시작할 수 있도록 단추나 링크와 같은 제스처가 있어야 합니다. 응용 프로그램에서 이 작업에 대해 보내는 요청은 일반적인 OAuth2/OpenID Connect 권한 부여 요청입니다. 이 요청은 *prompt=admin_consent* 쿼리 문자열 매개 변수를 포함합니다. 

관리자가 동의하고 서비스 주체가 고객 테넌트에 만들어진 후 이후의 로그인 요청은 *prompt=admin_consent* 매개 변수를 필요로 하지 않습니다. 관리자가 요청된 권한이 허용된다고 결정했다면 테넌트의 다른 사용자들에게 그 시점 이후로 동의하라는 메시지가 표시되지 않습니다.

테넌트 관리자는 일반 사용자가 응용 프로그램에 동의하는 기능을 사용하지 않도록 설정할 수 있습니다. 이 기능이 사용되지 않는 경우 테넌트에서 응용 프로그램을 사용하려면 항상 관리자 동의가 필요합니다. 최종 사용자 동의를 사용하지 않도록 설정된 응용 프로그램을 테스트하려면 [Azure Portal](https://portal.azure.com/)에서 구성 스위치를 찾을 수 있습니다. **엔터프라이즈 응용 프로그램** 아래의 [사용자 설정](https://portal.azure.com/#blade/Microsoft_AAD_IAM/StartboardApplicationsMenuBlade/UserSettings/menuId/) 섹션에 있습니다.

관리 동의가 필요하지 않은 사용 권한을 요청하는 응용 프로그램에서 *prompt=admin_consent* 매개 변수를 사용할 수도 있습니다. 예제는 테넌트 관리자가 한 번 "등록"한 환경이 필요하고, 다른 사용자에게 해당 지점에서 동의를 확인하는 메시지가 표시되지 않는 응용 프로그램입니다.

응용 프로그램에 관리자 동의 및 *prompt=admin_consent* 매개 변수가 전송되지 않은 관리자 로그인이 필요하다고 가정합니다. 관리자가 응용 프로그램에 성공적으로 동의하면 해당 사용자 계정에 대해서만 적용됩니다. 일반 사용자는 여전히 응용 프로그램에 로그인하거나 동의할 수 없습니다. 이 기능은 다른 사용자에게 액세스를 허용하기 전에 응용 프로그램을 탐색하는 기능을 테넌트 관리자에게 부여하고자 할 때 유용합니다.