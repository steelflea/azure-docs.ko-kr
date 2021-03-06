---
title: Azure Cosmos DB에 대한 SQL API Python 예제 | Microsoft Docs
description: CRUD 작업을 비롯한 Azure Cosmos DB의 일반적인 작업에 대한 github의 Python 예제를 찾습니다.
keywords: Python 예제
services: cosmos-db
author: SnehaGunda
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-sql
ms.devlang: python
ms.topic: sample
ms.date: 03/14/2018
ms.author: sngun
ms.openlocfilehash: 2eb585876f91526633fb2844e67ba734648b38e5
ms.sourcegitcommit: f20e43e436bfeafd333da75754cd32d405903b07
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2018
ms.locfileid: "49389539"
---
# <a name="azure-cosmos-db-python-examples"></a>Azure Cosmos DB Python 예제

> [!div class="op_single_selector"]
> * [.NET 예제](sql-api-dotnet-samples.md)
> * [Java 예제](sql-api-java-samples.md)
> * [비동기 Java 예제](sql-api-async-java-samples.md)
> * [Node.js 예제](sql-api-nodejs-samples.md)
> * [Python 예제](sql-api-python-samples.md)
> * [Azure 코드 샘플 갤러리](https://azure.microsoft.com/resources/samples/?sort=0&service=cosmos-db)
> 
> 

Azure Cosmos DB 리소스에 대해 CRUD 작업 및 다른 일반적인 작업을 수행하는 샘플 솔루션은 [azure-documentdb-python](https://github.com/Azure/azure-documentdb-python) GitHub 리포지토리에 포함되어 있습니다. 이 문서는 다음을 제공합니다.

* 각 Python 예제 프로젝트 파일에서 작업에 연결합니다. 
* 관련된 API 참조 콘텐츠에 대한 링크입니다.

**필수 구성 요소**

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

- [Visual Studio 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio)할 수 있음: Visual Studio 구독은 유료 Azure 서비스에 사용할 수 있는 크레딧을 매달 제공합니다.

[!INCLUDE [cosmos-db-emulator-docdb-api](../../includes/cosmos-db-emulator-docdb-api.md)]

또한 [Python SDK](sql-api-sdk-python.md)가 필요합니다. 
   
   > [!NOTE]
   > 각 샘플은 자체 포함되므로 자체 설정된 후 자체 정리됩니다. 샘플은 [document_client.CreateCollection](https://docs.microsoft.com/python/api/pydocumentdb.document_client.documentclient#createcollection)에 대한 여러 호출을 실행합니다. 이 작업이 완료될 때마다 구독에 1시간 사용 요금이 청구됩니다. Azure Cosmos DB 청구에 대한 자세한 내용은 [Azure Cosmos DB 가격 책정](https://azure.microsoft.com/pricing/details/cosmos-db/)을 참조하세요.
   > 
   > 

## <a name="database-examples"></a>데이터베이스 예제
[DatabaseManagement](https://github.com/Azure/azure-documentdb-python/blob/master/samples/DatabaseManagement) 프로젝트의 [Program.py](https://github.com/Azure/azure-documentdb-python/blob/master/samples/DatabaseManagement/Program.py) 파일은 다음 작업을 수행하는 방법을 보여 줍니다.

| Task | API 참조 |
| --- | --- |
| [데이터베이스 만들기](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L65-L76) |[document_client.CreateDatabase](https://docs.microsoft.com/python/api/pydocumentdb.document_client.documentclient?view=azure-python#createdatabase) |
| [ID별 데이터베이스 읽기](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L79-L96) |[document_client.ReadDatabase](https://docs.microsoft.com/python/api/pydocumentdb.document_client.documentclient?view=azure-python#readdatabase) |
| [계정에 대한 데이터베이스 나열](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L99-L110) |[document_client.ReadDatabases](https://docs.microsoft.com/python/api/pydocumentdb.document_client.documentclient?view=azure-python#readdatabases) |
| [데이터베이스 삭제](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L113-L126) |[document_client.DeleteDatabase](https://docs.microsoft.com/python/api/pydocumentdb.document_client.documentclient?view=azure-python#deletedatabase) |

## <a name="collection-examples"></a>컬렉션 예제
[CollectionManagement](https://github.com/Azure/azure-documentdb-python/blob/master/samples/CollectionManagement) 프로젝트의 [Program.py](https://github.com/Azure/azure-documentdb-python/blob/master/samples/CollectionManagement/Program.py) 파일은 다음 작업을 수행하는 방법을 보여 줍니다.

| Task | API 참조 |
| --- | --- |
| [컬렉션 만들기](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L84-L135) |[document_client.CreateCollection](https://docs.microsoft.com/python/api/pydocumentdb.document_client.documentclient?view=azure-python#createcollection) |
| [데이터베이스에서 모든 컬렉션의 목록 읽기](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L198-L209) |[document_client.ReadCollections](https://docs.microsoft.com/python/api/pydocumentdb.document_client.documentclient?view=azure-python#readcollections) |
| [ID별 컬렉션 가져오기](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L178-L195) |[document_client.ReadCollection](https://docs.microsoft.com/python/api/pydocumentdb.document_client.documentclient?view=azure-python#readcollection) |
| [컬렉션의 처리량 변경](https://github.com/Azure/azure-documentdb-python/blob/master/samples/CollectionManagement/Program.py#L168-L172) | [document_client.ReplaceOffer](https://docs.microsoft.com/python/api/pydocumentdb.document_client.documentclient?view=azure-python#replaceoffer)|
| [컬렉션 삭제](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L212-L225) |[document_client.DeleteCollection](https://docs.microsoft.com/python/api/pydocumentdb.document_client.documentclient?view=azure-python#deletecollection) |

## <a name="document-examples"></a>문서 예제
[DocumentManagement](https://github.com/Azure/azure-documentdb-python/blob/master/samples/DocumentManagement) 프로젝트의 [Program.py](https://github.com/Azure/azure-documentdb-python/blob/master/samples/DocumentManagement/Program.py) 파일은 다음 작업을 수행하는 방법을 보여줍니다.

| Task | API 참조 |
| --- | --- |
| [문서 만들기](https://github.com/Azure/azure-documentdb-python/blob/master/samples/DocumentManagement/Program.py#L55-L66) |[document_client.CreateDocument](https://docs.microsoft.com/python/api/pydocumentdb.document_client.documentclient?view=azure-python#createdocument) |
| [문서 컬렉션 만들기](https://github.com/Azure/azure-documentdb-python/blob/master/samples/DocumentManagement/Program.py#L55-L66) |[document_client.CreateDocuments](https://docs.microsoft.com/python/api/pydocumentdb.document_client.documentclient?view=azure-python) |
| [ID로 문서 읽기](https://github.com/Azure/azure-documentdb-python/blob/master/samples/DocumentManagement/Program.py#L69-L78) |[document_client.ReadDocument](https://docs.microsoft.com/python/api/pydocumentdb.document_client.documentclient?view=azure-python#readdocument) |
| [컬렉션의 모든 문서 읽기](https://github.com/Azure/azure-documentdb-python/blob/master/samples/DocumentManagement/Program.py#L81-L92) |[document_client.ReadDocuments](https://docs.microsoft.com/python/api/pydocumentdb.document_client.documentclient?view=azure-python#readdocuments) |

## <a name="indexing-examples"></a>청구 예제
[IndexManagement](https://github.com/Azure/azure-documentdb-python/blob/master/samples/IndexManagement) 프로젝트의 [Program.py](https://github.com/Azure/azure-documentdb-python/blob/master/samples/IndexManagement/Program.py) 파일은 다음 작업을 수행하는 방법을 보여줍니다.

| Task | API 참조 |
| --- | --- |
| [(자동 대신) 수동 인덱싱 사용](https://github.com/Azure/azure-documentdb-python/blob/master/samples/IndexManagement/Program.py#L245-L246) |[IndexingPolicy.Automatic](https://docs.microsoft.com/python/api/pydocumentdb.documents?view=azure-python) |
| [인덱스에서 지정된 문서 경로 제외](https://github.com/Azure/azure-documentdb-python/blob/master/samples/IndexManagement/Program.py#L294-L367) |[IndexingPolicy.ExcludedPaths](https://docs.microsoft.com/python/api/pydocumentdb.documents.indexingdirective?view=azure-python) |
| [인덱스에서 문서 제외](https://github.com/Azure/azure-documentdb-python/blob/master/samples/IndexManagement/Program.py#L204-L210) |[documents.IndexingDirective.Exclude](https://docs.microsoft.com/python/api/pydocumentdb.documents.indexingdirective?view=azure-python) |
| [인덱싱 모드 설정](https://github.com/Azure/azure-documentdb-python/blob/master/samples/IndexManagement/Program.py#L533) |[documents.IndexingMode](https://docs.microsoft.com/python/api/pydocumentdb.documents.indexingmode?view=azure-python) |
| [문자열에서 범위 인덱스 사용](https://github.com/Azure/azure-documentdb-python/blob/master/samples/IndexManagement/Program.py#L440-L456) |[IndexingPolicy.IncludedPaths](https://docs.microsoft.com/python/api/pydocumentdb.documents.indexingdirective?view=azure-python) |
| [인덱스 변환 수행](https://github.com/Azure/azure-documentdb-python/blob/master/samples/IndexManagement/Program.py#L514-L559) |[document_client.ReplaceCollection](https://docs.microsoft.com/python/api/pydocumentdb.document_client.documentclient?view=azure-python#replacecollection) |

## <a name="query-examples"></a>쿼리 예제
샘플 프로젝트는 다음 쿼리 작업을 수행하는 방법도 보여줍니다.

| Task | API 참조 |
| --- | --- |
| [데이터베이스에 대한 계정 쿼리](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L49-L62) |[document_client.QueryDatabases](https://docs.microsoft.com/python/api/pydocumentdb.document_client.documentclient?view=azure-python#querydatabases) |
| [문서에 대한 쿼리](https://github.com/Azure/azure-documentdb-python/blob/master/samples/IndexManagement/Program.py#L152-L169) |[document_client.QueryDocuments](https://docs.microsoft.com/python/api/pydocumentdb.document_client.documentclient?view=azure-python#querydocuments) |
| [해시 인덱스된 경로에 범위 검색 강제](https://github.com/Azure/azure-documentdb-python/blob/master/samples/IndexManagement/Program.py#L409-L415) |[http_constants.HttpHeaders.EnableScanInQuery](https://docs.microsoft.com/python/api/pydocumentdb.http_constants.httpheaders?view=azure-python#enablescaninquery) |
