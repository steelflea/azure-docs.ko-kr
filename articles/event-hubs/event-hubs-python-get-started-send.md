---
title: Python을 사용하여 Azure Event Hubs로 이벤트 전송 | Microsoft Docs
description: Python을 사용하여 Event Hubs로 이벤트 전송 시작
services: event-hubs
author: ShubhaVijayasarathy
manager: femila
ms.service: event-hubs
ms.workload: core
ms.topic: article
ms.date: 10/16/2018
ms.author: shvija
ms.openlocfilehash: 05feab0227633ab52f0865fa7c19a310b612eb1c
ms.sourcegitcommit: 02ce0fc22a71796f08a9aa20c76e2fa40eb2f10a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/08/2018
ms.locfileid: "51286897"
---
# <a name="send-events-to-event-hubs-using-python"></a>Python을 사용하여 Event Hubs에 이벤트 보내기

Azure Event Hubs는 초당 수백만 개의 이벤트를 수신하여 처리할 수 있는 빅 데이터 스트리밍 플랫폼이자 이벤트 수집 서비스입니다. Event Hubs는 분산된 소프트웨어와 장치에서 생성된 이벤트, 데이터 또는 원격 분석을 처리하고 저장할 수 있습니다. Event Hub로 전송된 데이터는 실시간 분석 공급자 또는 일괄 처리/저장소 어댑터를 사용하여 변환하고 저장할 수 있습니다. Event Hubs에 대한 자세한 개요는 [Event Hubs 개요](event-hubs-about.md) 및 [Event Hubs 기능](event-hubs-features.md)을 참조하세요.

이 자습서에서는 Python으로 작성된 응용 프로그램에서 이벤트 허브로 이벤트를 전송하는 방법을 설명합니다. 

> [!NOTE]
> [GitHub](https://github.com/Azure/azure-event-hubs-python/tree/master/examples)에서 샘플로 이 빠른 시작을 다운로드하여 `EventHubConnectionString` 및 `EventHubName` 문자열을 이벤트 허브 값으로 대체하고, 실행합니다. 또는 이 자습서의 단계를 수행하여 직접 만들 수 있습니다.

## <a name="prerequisites"></a>필수 조건

이 자습서를 완료하려면 다음 필수 구성 요소가 필요합니다.

- Python 3.4 이상


## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a>Event Hubs 네임스페이스 및 이벤트 허브 만들기
첫 번째 단계에서는 [Azure Portal](https://portal.azure.com)을 사용하여 Event Hubs 형식의 네임스페이스를 만들고 응용 프로그램에서 Event Hub와 통신하는 데 필요한 관리 자격 증명을 얻습니다. 네임스페이스와 이벤트 허브를 만들려면 [이 문서](event-hubs-create.md)의 절차를 수행한 다음, 이 자습서의 다음 단계를 진행하세요.

## <a name="install-python-package"></a>Python 패키지 설치

Event Hubs용 Python 패키지를 설치하려면 해당 경로에 Python이 있는 명령 프롬프트를 열고 다음 명령을 실행합니다. 

```bash
pip install azure-eventhub
```

## <a name="create-a-python-script-to-send-events"></a>이벤트를 보내는 Python 스크립트 만들기

다음으로, 이벤트 허브로 이벤트를 보내는 Python 응용 프로그램을 만듭니다.

1. 선호하는 Python 편집기(예: [Visual Studio Code][Visual Studio Code])를 엽니다.
2. **send.py**라는 스크립트를 만듭니다. 이 스크립트는 이벤트 허브에 100개의 이벤트를 전송합니다.
3. send.py에 다음 코드를 붙여넣습니다. 여기서 ADDRESS, USER 및 KEY 값을 이전 섹션의 Azure Portal에서 얻은 값으로 바꿉니다. 

```python
import sys
import logging
import datetime
import time
import os

from azure.eventhub import EventHubClient, Sender, EventData

logger = logging.getLogger("azure")

# Address can be in either of these formats:
# "amqps://<URL-encoded-SAS-policy>:<URL-encoded-SAS-key>@<mynamespace>.servicebus.windows.net/myeventhub"
# "amqps://<mynamespace>.servicebus.windows.net/myeventhub"
# For example:
ADDRESS = "amqps://mynamespace.servicebus.windows.net/myeventhub"

# SAS policy and key are not required if they are encoded in the URL
USER = "RootManageSharedAccessKey"
KEY = "namespaceSASKey"

try:
    if not ADDRESS:
        raise ValueError("No EventHubs URL supplied.")

    # Create Event Hubs client
    client = EventHubClient(ADDRESS, debug=False, username=USER, password=KEY)
    sender = client.add_sender(partition="0")
    client.run()
    try:
        start_time = time.time()
        for i in range(100):
            print("Sending message: {}".format(i))
            sender.send(EventData(str(i)))
    except:
        raise
    finally:
        end_time = time.time()
        client.stop()
        run_time = end_time - start_time
        logger.info("Runtime: {} seconds".format(run_time))

except KeyboardInterrupt:
    pass
```

## <a name="run-application-to-send-events"></a>응용 프로그램을 실행하여 이벤트 전송

이 스크립트를 실행하려면 해당 경로에 Python이 있는 명령 프롬프트를 열고 다음 명령을 실행합니다.

```bash
start python send.py
```

축하합니다! 이제 Event Hub에 메시지를 보냈습니다.
 
## <a name="next-steps"></a>다음 단계
이 빠른 시작에서는 Python을 사용하여 이벤트 허브로 메시지를 전송했습니다. Python을 사용하여 이벤트 허브에서 이벤트를 수신하는 방법을 알아보려면 [이벤트 허브에서 이벤트 수신 - Python](event-hubs-python-get-started-receive.md)을 참조하세요.

<!-- Links -->
[Event Hubs overview]: event-hubs-about.md
[Visual Studio Code]: https://code.visualstudio.com/
[free account]: https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio
