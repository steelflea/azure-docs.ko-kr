---
title: 포함 파일
description: 포함 파일
services: vpn-gateway
author: cherylmc
ms.service: vpn-gateway
ms.topic: include
ms.date: 10/21/2018
ms.author: cherylmc
ms.custom: include file
ms.openlocfilehash: bc1e2803a420b95e1abec0886733c5e42a8cfdb4
ms.sourcegitcommit: f6050791e910c22bd3c749c6d0f09b1ba8fccf0c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50026626"
---
1. [포털](http://portal.azure.com)에서 가상 네트워크 게이트웨이를 만들려는 Resource Manager 가상 네트워크로 이동합니다.
2. VNet 페이지의 **설정** 섹션에서 **서브넷**을 클릭하여 **서브넷** 페이지를 확장합니다.
3. **서브넷** 페이지에서 **+게이트웨이 서브넷**을 클릭하여 **서브넷 추가** 페이지를 엽니다. 

  ![게이트웨이 서브넷 추가](./media/vpn-gateway-add-gwsubnet-p2s-rm-portal-include/addgwsubnet.png "게이트웨이 서브넷 추가")
4. 서브넷의 **이름**에 'GatewaySubnet' 값이 자동으로 채워집니다. Azure가 서브넷을 게이트웨이 서브넷으로 인식하기 위해 이 값이 필요합니다. 자동으로 채워진 **주소 범위** 값을 구성 요구 사항과 일치하도록 조정합니다. 경로 테이블 또는 서비스 엔드포인트를 구성하지 마세요.

  ![서브넷 추가](./media/vpn-gateway-add-gwsubnet-p2s-rm-portal-include/p2sgwsub.png "서브넷 추가")
5.  서브넷을 만들려면 페이지 아래쪽에서 **확인**을 클릭합니다.