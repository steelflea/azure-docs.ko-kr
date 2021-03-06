---
title: Azure Monitor의 Log Analytics 데이터 분석 | Microsoft Docs
description: 로그 검색을 통해 Log Analytics의 모든 데이터를 검색해야 합니다.  이 문서는 Log Analytics에서 새 로그 검색이 어떻게 사용되는지를 설명하고 새로 만들기 전에 이해해야 하는 개념을 제공합니다.
services: log-analytics
documentationcenter: ''
author: bwren
manager: carmonm
editor: ''
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 10/18/2018
ms.author: bwren
ms.component: ''
ms.openlocfilehash: 0a8a1ab41972aa2ae184b900c2dab94ec58f3e7c
ms.sourcegitcommit: b62f138cc477d2bd7e658488aff8e9a5dd24d577
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51612757"
---
# <a name="analyze-log-analytics-data-in-azure-monitor"></a>Azure Monitor의 Log Analytics 데이터 분석

Azure Monitor에서 수집된 로그 데이터는 [Azure Data Explorer](/azure/data-explorer)를 기반으로 하는 Log Analytics 작업 영역에 저장됩니다. 다양한 원본에서 원격 분석을 수집하고 [데이터 탐색기의 쿼리 언어](/azure/kusto/query)를 사용하여 데이터를 검색하고 분석합니다.

> [!NOTE]
> Log Analytics는 이전에 Azure의 자체 서비스로 간주되었습니다. 이제 Azure Monitor의 일부로 간주되며, 쿼리 언어를 사용한 로그 데이터 저장 및 분석에 집중합니다. 데이터 수집을 위한 Windows 및 Linux 에이전트, 기존 데이터를 시각화하는 뷰, 문제를 사전에 알리는 경고 등 Log Analytics의 일부로 간주되는 기능은 변경되지 않았지만 이제 Azure Monitor의 일부로 간주됩니다.



## <a name="log-queries"></a>로그 쿼리

Log Analytics에서 데이터를 검색하려면 로그 쿼리가 필요합니다.  [포털에서 데이터를 분석](log-analytics-log-search-portals.md)하든, 특정 조건에 대해 알리도록 [경고 규칙을 구성](../monitoring-and-diagnostics/alert-metric.md)하든, [Log Analytics API](https://dev.loganalytics.io/)를 사용하여 데이터를 검색하든 관계없이 쿼리를 사용하여 원하는 데이터를 지정합니다.  이 문서에서는 Log Analytics에서 쿼리를 사용하는 방법을 설명하고 쿼리를 만들기 전에 이해해야 하는 개념을 제공합니다.



## <a name="where-log-queries-are-used"></a>로그 쿼리가 사용되는 위치

Log Analytics에서 쿼리를 사용하는 방법은 다음과 같습니다.

- **포털.** [Azure Portal](log-analytics-log-search-portals.md)에서 로그 데이터에 대한 대화형 분석을 수행할 수 있습니다.  그러면 다양한 형식 및 시각화로 쿼리를 편집하고 결과를 분석할 수 있습니다.  
- **경고 규칙.** [경고 규칙](../monitoring-and-diagnostics/monitoring-overview-alerts.md)은 작업 영역에서 데이터의 문제를 사전에 식별합니다.  각 경고 규칙은 일정한 간격으로 자동으로 실행되는 로그 검색을 기반으로 합니다.  경고를 만들어야 하는지 여부를 결정하도록 결과를 검사합니다.
- **대시보드.** 쿼리 결과를 [Azure 대시보드]()에 고정하여 로그 및 메트릭 데이터를 함께 시각화하고 다른 Azure 사용자와 선택적으로 공유할 수 있습니다. 
- **뷰.**  [뷰 디자이너](log-analytics-view-designer.md)를 통해 사용자 대시보드에 포함될 데이터의 시각화를 만들 수 있습니다.  로그 쿼리는 각 뷰의 [타일](log-analytics-view-designer-tiles.md) 및 [시각화 파트](log-analytics-view-designer-parts.md)에서 사용되는 데이터를 제공합니다.  
- **내보내기.**  Log Analytics 작업 영역에서 Excel 또는 [Power BI](log-analytics-powerbi.md)로 데이터를 가져오는 경우 로그 쿼리를 만들어 내보낼 데이터를 정의합니다.
- **PowerShell.** [Get-AzureRmOperationalInsightsSearchResults](https://docs.microsoft.com/powershell/module/azurerm.operationalinsights/get-azurermoperationalinsightssearchresults?view=azurermps-4.0.0)를 사용하는 명령줄 또는 Azure Automation Runbook에서 PowerShell 스크립트를 실행하여 Log Analytics에서 데이터를 검색합니다.  이 cmdlet에는 검색할 데이터를 결정하는 쿼리가 필요합니다.
- **Log Analytics API.**  REST API 클라이언트는 [Log Analytics 로그 검색 API](../monitoring-and-diagnostics/monitoring-overview-alerts.md)를 통해 작업 영역에서 로그 데이터를 검색할 수 있습니다.  API 요청에는 검색할 데이터를 확인하기 위해 Log Analytics에 대해 실행되는 쿼리가 포함됩니다.

![로그 검색](media/log-analytics-queries/queries-overview.png)

## <a name="write-a-query"></a>쿼리 작성
Log Analytics에서는 다양한 방법으로 로그 데이터를 검색하고 분석하는 [버전의 데이터 탐색기 쿼리 언어](query-language/get-started-queries.md)를 사용합니다.  일반적으로 기본 쿼리로 시작하고, 요구 사항이 복잡해지면 더 많은 고급 기능을 사용하게 됩니다.

쿼리의 기본 구조는 원본 테이블이며 그 뒤에 파이프 문자 `|`로 구분된 일련의 연산자가 있습니다.  여러 연산자와 함께 연결하여 데이터를 구체화하고 고급 기능을 수행할 수 있습니다.

예를 들어, 과거 오류 이벤트가 가장 많은 상위 10개 컴퓨터를 찾는다고 가정합니다.

```Kusto
Event
| where (EventLevelName == "Error")
| where (TimeGenerated > ago(1days))
| summarize ErrorCount = count() by Computer
| top 10 by ErrorCount desc
```

또는 마지막 날에 하트비트를 보유하지 않은 컴퓨터를 찾을 수도 있습니다.

```Kusto
Heartbeat
| where TimeGenerated > ago(7d)
| summarize max(TimeGenerated) by Computer
| where max_TimeGenerated < ago(1d)  
```

지난 주 각 컴퓨터의 프로세서 사용률과 관련된 꺾은선형 차트는 어떨까요?

```Kusto
Perf
| where ObjectName == "Processor" and CounterName == "% Processor Time"
| where TimeGenerated  between (startofweek(ago(7d)) .. endofweek(ago(7d)) )
| summarize avg(CounterValue) by Computer, bin(TimeGenerated, 5min)
| render timechart    
```

이러한 간단한 샘플 쿼리에서, 작업하는 데이터의 종류에 관계 없이 구조는 비슷하다는 점을 알 수 있습니다.  한 명령의 결과 데이터가 파이프라인을 통해 다음 명령에 전송되는 별개의 단계로 구분할 수 있습니다.

또한 구독 내에서 Log Analytics 작업 영역 전반에 걸쳐 데이터를 쿼리할 수도 있습니다.

```Kusto
union Update, workspace("contoso-workspace").Update
| where TimeGenerated >= ago(1h)
| summarize dcount(Computer) by Classification 
```

## <a name="how-log-analytics-data-is-organized"></a>Log Analytics 데이터 구성 방법
쿼리를 작성하는 경우 원하는 데이터가 있는 테이블이 무엇인지 확인하는 것으로 시작합니다. 각기 다른 종류의 데이터가 각 [Log Analytics 작업 영역](log-analytics-quick-create-workspace.md)의 전용 테이블에 구분됩니다.  다양한 데이터 원본의 설명서에는 생성되는 데이터 형식의 이름 및 각 속성에 대한 설명이 포함되어 있습니다.  많은 쿼리의 경우 단일 테이블의 데이터만 필요하지만, 여러 테이블의 데이터를 포함하는 다양한 옵션이 사용되는 경우도 있습니다.

[Application Insights](../application-insights/app-insights-overview.md)는 요청, 예외, 추적 및 사용과 같은 응용 프로그램 데이터를 Log Analytics에 저장하지만, 이 데이터는 다른 로그 데이터와 다른 파티션에 저장됩니다. 동일한 쿼리 언어를 사용하여 이 데이터에 액세스하지만, [Application Insights 콘솔](../application-insights/app-insights-analytics.md) 또는 [Application Insights REST API](https://dev.applicationinsights.io/)를 사용하여 액세스해야 합니다. [리소스 간 쿼리](log-analytics-cross-workspace-search.md)를 사용하여 Application Insights 데이터를 Log Analytics의 다른 데이터와 결합할 수 있습니다.


![테이블](media/log-analytics-queries/queries-tables.png)







## <a name="next-steps"></a>다음 단계

- [로그 검색을 만들고 편집하는 데 사용하는 포털](log-analytics-log-search-portals.md)에 대해 알아보세요.
- 새로운 쿼리 언어를 사용한 [쿼리 작성 자습서](log-analytics-tutorial-viewdata.md)를 확인해 보세요.
