---
title: '자습서: Cisco Spark와 Azure Active Directory 통합 | Microsoft Docs'
description: Azure Active Directory 및 Cisco Spark 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: c47894b1-f5df-4755-845d-f12f4c602dc4
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: bebc8d674d7448ea0ce6a1f11b7ae80335df9cdc
ms.sourcegitcommit: 1d850f6cae47261eacdb7604a9f17edc6626ae4b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/02/2018
ms.locfileid: "39431701"
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-spark"></a>자습서: Cisco Spark와 Azure Active Directory 통합

이 자습서에서는 Azure AD(Azure Active Directory)와 Cisco Spark를 통합하는 방법에 대해 알아봅니다.

Cisco Spark를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.

- Cisco Spark에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.
- 사용자가 해당 Azure AD 계정으로 Cisco Spark에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.
- 단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](../manage-apps/what-is-single-sign-on.md)를 참조하세요.

## <a name="prerequisites"></a>필수 조건

Cisco Spark와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.

- Azure AD 구독
- Cisco Spark Single Sign-On이 설정된 구독

> [!NOTE]
> 이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.

이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.
- Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.

1. 갤러리에서 Cisco Spark 추가
1. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-cisco-spark-from-the-gallery"></a>갤러리에서 Cisco Spark 추가
Cisco Spark의 Azure AD 통합을 구성하려면 갤러리의 Cisco Spark를 관리되는 SaaS 앱 목록에 추가해야 합니다.

**갤러리에서 Cisco Spark를 추가하려면 다음 단계를 수행합니다.**

1. **[Azure Portal](https://portal.azure.com)** 의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다. 

    ![Active Directory][1]

1. **엔터프라이즈 응용 프로그램**으로 이동합니다. 그런 후 **모든 응용 프로그램**으로 이동합니다.

    ![응용 프로그램][2]
    
1. 새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.

    ![응용 프로그램][3]

1. 검색 상자에 **Cisco Spark**를 입력합니다.

    ![Azure AD 테스트 사용자 만들기](./media/cisco-spark-tutorial/tutorial_ciscospark_search.png)

1. 결과 패널에서 **Cisco Spark**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.

    ![Azure AD 테스트 사용자 만들기](./media/cisco-spark-tutorial/tutorial_ciscospark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD Single Sign-on 구성 및 테스트
이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 Cisco Spark에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Cisco Spark 사용자가 누구인지 알고 있어야 합니다. 즉, Azure AD 사용자와 Cisco Spark의 관련 사용자 간에 연결이 형성되어야 합니다.

Cisco Spark에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.

Cisco Spark에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.
1. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On 테스트하는 데 사용합니다.
1. **[Cisco Spark 테스트 사용자 만들기](#creating-a-cisco-spark-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Cisco Spark에 만듭니다.
1. **[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.
1. **[Single Sign-On 테스트](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Cisco Spark 응용 프로그램에서 Single Sign-On을 구성합니다.

**Cisco Spark에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**

1. Azure Portal의 **Cisco Spark** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.

    ![Configure Single Sign-On][4]

1. **Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.
 
    ![Configure Single Sign-On](./media/cisco-spark-tutorial/tutorial_ciscospark_samlbase.png)

1. **Cisco Spark 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.

    ![Configure Single Sign-On](./media/cisco-spark-tutorial/tutorial_ciscospark_url.png)

    a. **로그온 URL** 텍스트 상자에 URL을 입력합니다. `https://web.ciscospark.com/#/signin`

    나. **식별자** 텍스트 상자에서 `https://idbroker.webex.com/<companyname>` 패턴을 사용하여 URL을 입력합니다.

    > [!NOTE] 
    > 이 값은 실제 값이 아닙니다. 실제 식별자로 이 값을 업데이트하세요. 이 값을 얻으려면 [Cisco Spark 클라이언트 지원 팀](https://support.ciscospark.com/)에 문의하세요. 
 
1. **SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.

    ![Configure Single Sign-On](./media/cisco-spark-tutorial/tutorial_ciscospark_certificate.png) 

1. Cisco Spark 응용 프로그램은 특정 특성을 포함하는 SAML 어설션이 필요합니다. 이 응용 프로그램에 대한 다음 특성을 구성합니다. 응용 프로그램 통합 페이지의 **사용자 특성** 섹션에서 이러한 특성의 값을 관리할 수 있습니다. 다음 스크린샷은 이에 대한 예제를 보여 줍니다.
    
    ![Configure Single Sign-On](./media/cisco-spark-tutorial/tutorial_ciscospark_07.png) 

1. **Single sign-on** 대화 상자의 **사용자 특성** 섹션에서 위의 이미지에 표시된 것과 같이 SAML 토큰 특성을 구성하고 다음 단계를 수행합니다.
    
    | 특성 이름  | 특성 값 |
    | --------------- | -------------------- |    
    |   uid    | user.userprincipalname |   

    a. **특성 추가**를 클릭하여 **특성 추가** 대화 상자를 엽니다.

    ![Configure Single Sign-On](./media/cisco-spark-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On](./media/cisco-spark-tutorial/tutorial_attribute_05.png)
    
    나. **이름** 텍스트 상자에서 해당 행에 표시된 특성 이름을 입력합니다.
    
    다. **값** 목록에서 해당 행에 대해 표시된 특성을 입력합니다.
    
    d. **Ok**를 클릭합니다.

1. **저장** 단추를 클릭합니다.

    ![Configure Single Sign-On](./media/cisco-spark-tutorial/tutorial_general_400.png)

1. 전체 관리자 자격 증명으로 [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/)에 로그인합니다.

1. **설정**을 선택하고 **인증** 섹션 아래에서 **수정**을 클릭합니다.
   
    ![Configure Single Sign-On](./media/cisco-spark-tutorial/tutorial_cisco_spark_10.png)
    
1. **타사 ID 공급자 통합 (고급)** 을 선택하고 다음 화면으로 이동합니다.

1. **Idp 메타데이터 가져오기** 페이지에서 Azure AD 메타데이터 파일을 페이지로 끌어다 놓거나 파일 브라우저 옵션을 사용하여 Azure AD 메타데이터 파일을 찾아 업로드합니다. 그런 다음 **메타데이터에서 인증 기관이 서명한 인증서 필요(더 안전)** 를 선택하고 **다음**을 클릭합니다. 
    
    ![Configure Single Sign-On](./media/cisco-spark-tutorial/tutorial_cisco_spark_11.png)

1. **SSO 연결 테스트**를 선택하고 새 브라우저 탭이 열리면 로그인하여 Azure AD로 인증합니다.

1. **Cisco Cloud Collaboration Management** 브라우저 탭으로 돌아갑니다. 테스트에 성공하면 **이 테스트에 성공했습니다. Single Sign-On 사용 옵션**을 선택하고 **다음**을 클릭합니다.

> [!TIP]
> 이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.  **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다. 포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.
> 

### <a name="creating-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.

![Azure AD 사용자 만들기][100]

**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**

1. **Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.

    ![Azure AD 테스트 사용자 만들기](./media/cisco-spark-tutorial/create_aaduser_01.png) 

1. 사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.
    
    ![Azure AD 테스트 사용자 만들기](./media/cisco-spark-tutorial/create_aaduser_02.png) 

1. **사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/cisco-spark-tutorial/create_aaduser_03.png) 

1. **사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/cisco-spark-tutorial/create_aaduser_04.png) 

    a. **이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.

    나. **사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.

    다. **암호 표시**를 선택하고 **암호** 값을 적어둡니다.

    d. **만들기**를 클릭합니다.
 
### <a name="creating-a-cisco-spark-test-user"></a>Cisco Spark 테스트 사용자 만들기

이 섹션에서는 Cisco Spark에서 Britta Simon이라는 사용자를 만듭니다. 이 섹션에서는 Cisco Spark에서 Britta Simon이라는 사용자를 만듭니다.

1. 전체 관리자 자격 증명으로 [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/)로 이동합니다.

1. **사용자**, **사용자 관리**를 차례로 클릭합니다.
   
    ![Configure Single Sign-On](./media/cisco-spark-tutorial/tutorial_cisco_spark_12.png) 

1. **사용자 관리** 창에서 **수동으로 사용자 추가 또는 수정**을 선택하고 **다음**을 클릭합니다.

1. **이름 및 전자 메일 주소**를 선택합니다. 그런 다음 아래와 같이 텍스트 상자에 내용을 입력합니다.
   
    ![Configure Single Sign-On](./media/cisco-spark-tutorial/tutorial_cisco_spark_13.png) 
    
    a. **이름** 텍스트 상자에 **Britta**를 입력합니다. 
    
    나. **성** 텍스트 상자에 **Simon**을 입력합니다.
    
    다. **전자 메일 주소** 텍스트 상자에 **britta.simon@contoso.com**을 입력합니다.

1. 더하기 기호를 클릭하여 Britta Simon을 추가합니다. 그런 후 **다음**을 클릭합니다.

1. **사용자에 대한 서비스 추가** 창에서 **저장**을 클릭한 후 **마침**을 클릭합니다.

### <a name="assigning-the-azure-ad-test-user"></a>Azure AD 테스트 사용자 할당

이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Cisco Spark에 대한 액세스 권한을 부여합니다.

![사용자 할당][200] 

**Britta Simon을 Cisco Spark에 할당하려면 다음 단계를 수행합니다.**

1. Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.

    ![사용자 할당][201] 

1. 응용 프로그램 목록에서 **Cisco Spark**를 선택합니다.

    ![Configure Single Sign-On](./media/cisco-spark-tutorial/tutorial_ciscospark_app.png) 

1. 왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.

    ![사용자 할당][202] 

1. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![사용자 할당][203]

1. **사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.

1. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

1. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    
### <a name="testing-single-sign-on"></a>Single Sign-On 테스트

이 섹션은 액세스 패널을 사용하여 Azure AD SSO 구성을 테스트하기 위한 것입니다.

액세스 패널에서 Cisco Spark 타일을 클릭하면 Cisco Spark 응용 프로그램에 자동으로 로그온됩니다.

## <a name="additional-resources"></a>추가 리소스

* [Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록](tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On을 구현하는 방법](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/cisco-spark-tutorial/tutorial_general_01.png
[2]: ./media/cisco-spark-tutorial/tutorial_general_02.png
[3]: ./media/cisco-spark-tutorial/tutorial_general_03.png
[4]: ./media/cisco-spark-tutorial/tutorial_general_04.png
[10]: ./media/cisco-spark-tutorial/tutorial_general_060.png
[100]: ./media/cisco-spark-tutorial/tutorial_general_100.png

[200]: ./media/cisco-spark-tutorial/tutorial_general_200.png
[201]: ./media/cisco-spark-tutorial/tutorial_general_201.png
[202]: ./media/cisco-spark-tutorial/tutorial_general_202.png
[203]: ./media/cisco-spark-tutorial/tutorial_general_203.png

