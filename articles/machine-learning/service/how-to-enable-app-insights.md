---
title: 프로덕션 환경에서 Azure Machine Learning 서비스에 대한 Application Insights 사용
description: Azure Kubernetes Service로 배포하기 위해 Azure Machine Learning 서비스에 대해 Application Insights를 설정하는 방법 알아보기
services: machine-learning
ms.service: machine-learning
ms.component: core
ms.topic: conceptual
ms.reviewer: jmartens
ms.author: marthalc
author: marthalc
ms.date: 10/01/2018
ms.openlocfilehash: 285486d5fe641d49ee21d7340b62f83d75862553
ms.sourcegitcommit: 0fc99ab4fbc6922064fc27d64161be6072896b21
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51578302"
---
# <a name="monitor-your-azure-machine-learning-models-in-production-with-application-insights"></a>Application Insights를 사용하여 프로덕션 환경에서 Azure Machine Learning 모델 모니터링

이 문서에서는 Azure Machine Learning 서비스에 대해 Azure Application Insights를 설정하는 방법을 알아봅니다. Application Insights를 통해 다음을 모니터링할 수 있습니다.
* 요청 속도, 응답 시간 및 실패율
* 종속성 비율, 응답 시간 및 실패율
* 예외.

[Application Insights에 대해 자세히 알아봅니다](../../application-insights/app-insights-overview.md). 

>[!NOTE]
> 이 문서의 코드는 Azure Machine Learning SDK 버전 0.1.74에서 테스트됨


## <a name="prerequisites"></a>필수 조건
* Azure 구독. 구독이 없으면 시작하기 전에 [계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)을 만드세요.
* Azure Machine Learning 작업 영역, 스크립트가 포함된 로컬 디렉터리 및 Python용 Azure Machine Learning SDK가 설치되어 있어야 합니다. 이러한 필수 구성 요소를 충족하는 방법을 알아보려면 [개발 환경 구성 방법](how-to-configure-environment.md)을 참조하세요.
* AKS(Azure Kubernetes Service)에 배포할 학습된 Machine Learning 모델. 이러한 모델이 없으면 [이미지 분류 모델 학습](tutorial-train-models-with-aml.md) 자습서를 참조하세요.
* [AKS 클러스터](how-to-deploy-to-aks.md)

## <a name="enable-and-disable-in-the-portal"></a>포털에서 사용 및 사용하지 않도록 설정

Azure Portal에서 Application Insights를 사용하거나 사용하지 않도록 설정할 수 있습니다.

### <a name="enable"></a>사용

1. [Azure Portal](https://portal.azure.com)에서 작업 영역을 엽니다.

1. **배포** 탭에서 Application Insights를 사용하도록 설정하려는 서비스를 선택합니다.

   [![배포 탭의 서비스 목록](media/how-to-enable-app-insights/Deployments.PNG)](./media/how-to-enable-app-insights/Deployments.PNG#lightbox)

3. **편집**을 선택합니다.

   [![편집 단추](media/how-to-enable-app-insights/Edit.PNG)](./media/how-to-enable-app-insights/Edit.PNG#lightbox)

4. **고급 설정**에서 **AppInsights 진단 사용** 확인란을 선택합니다.

   [![진단을 사용하도록 설정하기 위한 확인란을 선택함](media/how-to-enable-app-insights/AdvancedSettings.png)](./media/how-to-enable-app-insights/AdvancedSettings.png#lightbox)

1. 화면 맨 아래에서 **업데이트**를 선택하여 변경 내용을 적용합니다. 

### <a name="disable"></a>사용 안 함
1. [Azure Portal](https://portal.azure.com)에서 작업 영역을 엽니다.
1. **배포**를 선택하고 서비스를 선택한 후 **편집**을 선택합니다.

   [![편집 단추](media/how-to-enable-app-insights/Edit.PNG)](./media/how-to-enable-app-insights/Edit.PNG#lightbox)

1. **고급 설정**에서 **AppInsights 진단 사용** 확인란을 선택 취소합니다. 

   [![진단을 사용하도록 설정하기 위한 확인란을 선택 취소함](media/how-to-enable-app-insights/uncheck.png)](./media/how-to-enable-app-insights/uncheck.png#lightbox)

1. 화면 맨 아래에서 **업데이트**를 선택하여 변경 내용을 적용합니다. 

## <a name="enable-and-disable-from-the-sdk"></a>SDK에서 사용 및 사용하지 않도록 설정

### <a name="update-a-deployed-service"></a>배포된 서비스 업데이트
1. 작업 영역에서 서비스를 식별합니다. `ws` 값은 작업 영역의 이름입니다.

    ```python
    aks_service= Webservice(ws, "my-service-name")
    ```
2. 서비스를 업데이트하고 Application Insights를 사용하도록 설정합니다. 

    ```python
    aks_service.update(enable_app_insights=True)
    ```

### <a name="log-custom-traces-in-your-service"></a>서비스에서 사용자 지정 추적 로그
사용자 지정 추적을 기록하려는 경우 [AKS에 대한 표준 배포 프로세스](how-to-deploy-to-aks.md)를 수행합니다. 그렇다면

1. 인쇄 문을 추가하여 점수 매기기 파일을 업데이트합니다.
    
    ```python
    print ("model initialized" + time.strftime("%H:%M:%S"))
    ```

2. AKS 구성을 업데이트합니다.
    
    ```python
    aks_config = AksWebservice.deploy_configuration(enable_app_insights=True)
    ```

3. [이미지를 빌드하고 배포합니다](how-to-deploy-to-aks.md).  

### <a name="disable-tracking-in-python"></a>Python에서 추적을 사용하지 않도록 설정

Application Insights를 사용하지 않도록 설정하려면 다음 코드를 사용합니다.

```python 
## replace <service_name> with the name of the web service
<service_name>.update(enable_app_insights=False)
```
    

## <a name="evaluate-data"></a>데이터 평가
서비스의 데이터는 Azure Machine Learning 서비스가 있는 동일한 리소스 그룹 내 Application Insights 계정에 저장됩니다.
이 데이터를 보려면:
1. [Azure Portal](https://portal.azure.com)의 Machine Learning Service 작업 영역으로 이동하여 Application Insights 링크를 클릭합니다.

    [![AppInsightsLoc](media/how-to-enable-app-insights/AppInsightsLoc.png)](./media/how-to-enable-app-insights/AppInsightsLoc.png#lightbox)

1. **개요** 탭을 선택하면 서비스에 대한 기본 메트릭 집합이 표시됩니다.

   [![개요](media/how-to-enable-app-insights/overview.png)](./media/how-to-enable-app-insights/overview.png#lightbox)

3. 사용자 지정 추적을 살펴보려면 **분석**을 선택합니다.
4. 스키마 섹션에서 **추적**을 선택합니다. 그런 후 **실행**을 선택하여 쿼리를 실행합니다. 데이터가 테이블 형식으로 표시되며 점수 매기기 파일에서 사용자 지정 호출로 매핑되어야 합니다. 

   [![사용자 지정 추적](media/how-to-enable-app-insights/logs.png)](./media/how-to-enable-app-insights/logs.png#lightbox)

Application Insights 사용 방법에 대한 자세한 내용은 [Application Insights란?](../../application-insights/app-insights-overview.md)을 참조하세요.
    

## <a name="example-notebook"></a>예제 Notebook

[00.Getting Started/13.enable-app-insights-in-production-service.ipynb](https://github.com/Azure/MachineLearningNotebooks/tree/master/01.getting-started/13.enable-app-insights) Notebook에서는 이 문서의 개념을 설명합니다.  이 Notebook을 다운로드하려면 다음 단계를 수행합니다.
 
[!INCLUDE [aml-clone-in-azure-notebook](../../../includes/aml-clone-for-examples.md)]

## <a name="next-steps"></a>다음 단계
또한 프로덕션에서 모델에 대한 데이터를 수집할 수 있습니다. [프로덕션에서 모델용 데이터 수집](how-to-enable-data-collection.md) 문서를 읽어보세요. 


## <a name="other-references"></a>기타 참조
* [컨테이너용 Azure Monitor](https://docs.microsoft.com/azure/monitoring/monitoring-container-insights-overview?toc=%2fazure%2fmonitoring%2ftoc.json)
