---
author: kumudD
ms.service: load-balancer
ms.topic: include
ms.date: 11/09/2018
ms.author: kumud
ms.openlocfilehash: bf3aee30460e052db23cf9090f13e2af3b22628b
ms.sourcegitcommit: fa758779501c8a11d98f8cacb15a3cc76e9d38ae
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2018
ms.locfileid: "52271305"
---
이 시나리오에서는 다음 작업이 수행 됩니다.

* 포트 80의 네트워크 트래픽을 수신하는 부하 분산 장치를 만들고 부하가 분산된 트래픽을 가상 머신 "web1" 및 "web2"에 전송합니다.
* 부하 분산 장치 뒤에 있는 가상 머신의 원격 데스크톱 액세스/SSH에 대한 NAT 규칙 만들기
* 상태 프로브 만들기

![부하 분산 장치 시나리오](./media/load-balancer-get-started-internet-scenario-include/scenario-classic.png)
