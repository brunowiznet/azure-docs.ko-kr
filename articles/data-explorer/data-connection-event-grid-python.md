---
title: Python을 사용 하 여 Azure 데이터 탐색기에 대 한 Event Grid 데이터 연결 만들기
description: 이 문서에서는 Python을 사용 하 여 Azure 데이터 탐색기에 대 한 Event Grid 데이터 연결을 만드는 방법에 대해 알아봅니다.
author: lucygoldbergmicrosoft
ms.author: lugoldbe
ms.reviewer: orspodek
ms.service: data-explorer
ms.topic: conceptual
ms.date: 10/07/2019
ms.openlocfilehash: 16f944146cf97666fd9866607ff436a49d5fb031
ms.sourcegitcommit: 3d4917ed58603ab59d1902c5d8388b954147fe50
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/02/2019
ms.locfileid: "74667732"
---
# <a name="create-an-event-grid-data-connection-for-azure-data-explorer-by-using-python"></a>Python을 사용 하 여 Azure 데이터 탐색기에 대 한 Event Grid 데이터 연결 만들기

> [!div class="op_single_selector"]
> * [Portal](ingest-data-event-grid.md)
> * [C#](data-connection-event-grid-csharp.md)
> * [Python](data-connection-event-grid-python.md)
> * [Azure Resource Manager 템플릿](data-connection-event-grid-resource-manager.md)

Azure 데이터 탐색기는 로그 및 원격 분석 데이터에 사용 가능한 빠르고 확장성이 우수한 데이터 탐색 서비스입니다. Azure 데이터 탐색기는 blob 컨테이너에 기록 된 Event Hubs, IoT Hub 및 blob에서 수집 (데이터 로드)을 제공 합니다. 이 문서에서는 Python을 사용 하 여 Azure 데이터 탐색기에 대 한 Event Grid 데이터 연결을 만듭니다.

## <a name="prerequisites"></a>전제 조건

* Azure 구독이 아직 없는 경우 시작하기 전에 [Azure 체험 계정](https://azure.microsoft.com/free/)을 만듭니다.
* [클러스터 및 데이터베이스](create-cluster-database-csharp.md) 만들기
* [테이블 및 열 매핑](net-standard-ingest-data.md#create-a-table-on-your-test-cluster) 만들기
* [데이터베이스 및 테이블 정책](database-table-policies-csharp.md) 설정 (선택 사항)
* [Event Grid 구독을 사용 하 여 저장소 계정을](ingest-data-event-grid.md#create-an-event-grid-subscription-in-your-storage-account)만듭니다.

[!INCLUDE [data-explorer-data-connection-install-package-python](../../includes/data-explorer-data-connection-install-package-python.md)]

[!INCLUDE [data-explorer-authentication](../../includes/data-explorer-authentication.md)]

## <a name="add-an-event-grid-data-connection"></a>Event Grid 데이터 연결 추가

다음 예제에서는 프로그래밍 방식으로 Event Grid 데이터 연결을 추가 하는 방법을 보여 줍니다. Azure Portal를 사용 하 여 Event Grid 데이터 연결을 추가 하려면 [Azure 데이터 탐색기에서 Event Grid 데이터 연결 만들기](ingest-data-event-grid.md#create-an-event-grid-data-connection-in-azure-data-explorer) 를 참조 하세요.


```Python
from azure.mgmt.kusto import KustoManagementClient
from azure.mgmt.kusto.models import EventGridDataConnection
from azure.common.credentials import ServicePrincipalCredentials

#Directory (tenant) ID
tenant_id = "xxxxxxxx-xxxxx-xxxx-xxxx-xxxxxxxxx"
#Application ID
client_id = "xxxxxxxx-xxxxx-xxxx-xxxx-xxxxxxxxx"
#Client Secret
client_secret = "xxxxxxxxxxxxxx"
subscription_id = "xxxxxxxx-xxxxx-xxxx-xxxx-xxxxxxxxx"
credentials = ServicePrincipalCredentials(
        client_id=client_id,
        secret=client_secret,
        tenant=tenant_id
    )
kusto_management_client = KustoManagementClient(credentials, subscription_id)

resource_group_name = "testrg";
#The cluster and database that are created as part of the Prerequisites
cluster_name = "mykustocluster";
database_name = "mykustodatabase";
data_connection_name = "myeventhubconnect";
#The event hub and storage account that are created as part of the Prerequisites
event_hub_resource_id = "/subscriptions/xxxxxxxx-xxxxx-xxxx-xxxx-xxxxxxxxx/resourceGroups/xxxxxx/providers/Microsoft.EventHub/namespaces/xxxxxx/eventhubs/xxxxxx"
storage_account_resource_id = "/subscriptions/xxxxxxxx-xxxxx-xxxx-xxxx-xxxxxxxxx/resourceGroups/xxxxxx/providers/Microsoft.Storage/storageAccounts/xxxxxx"
consumer_group = "$Default";
location = "Central US";
#The table and column mapping that are created as part of the Prerequisites
table_name = "StormEvents";
mapping_rule_name = "StormEvents_CSV_Mapping";
data_format = "csv";

#Returns an instance of LROPoller, check https://docs.microsoft.com/python/api/msrest/msrest.polling.lropoller?view=azure-python
poller = kusto_management_client.data_connections.create_or_update(resource_group_name=resource_group_name, cluster_name=cluster_name, database_name=database_name, data_connection_name=data_connection_name,
                                            parameters=EventGridDataConnection(storage_account_resource_id=storage_account_resource_id, event_hub_resource_id=event_hub_resource_id, 
                                                                                consumer_group=consumer_group, table_name=table_name, location=location, mapping_rule_name=mapping_rule_name, data_format=data_format))
```
|**설정** | **제안 값** | **필드 설명**|
|---|---|---|
| tenant_id | *xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx-xxxxx-xxxxxxxxx* | 테넌트 ID 디렉터리 ID 라고도 합니다.|
| subscription_id | *xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx-xxxxx-xxxxxxxxx* | 리소스를 만드는 데 사용 하는 구독 ID입니다.|
| client_id | *xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx-xxxxx-xxxxxxxxx* | 테 넌 트의 리소스에 액세스할 수 있는 응용 프로그램의 클라이언트 ID입니다.|
| client_secret | *xxxxxxxxxxxxxx* | 테 넌 트의 리소스에 액세스할 수 있는 응용 프로그램의 클라이언트 암호입니다. |
| resource_group_name | *testrg* | 클러스터를 포함 하는 리소스 그룹의 이름입니다.|
| cluster_name | *mykustocluster* | 클러스터의 이름입니다.|
| database_name | *mykustodatabase* | 클러스터에 있는 대상 데이터베이스의 이름입니다.|
| data_connection_name | *myeventhubconnect* | 원하는 데이터 연결 이름입니다.|
| table_name | *StormEvents* | 대상 데이터베이스에 있는 대상 테이블의 이름입니다.|
| mapping_rule_name | *StormEvents_CSV_Mapping* | 대상 테이블과 관련 된 열 매핑의 이름입니다.|
| data_format | *csv* | 메시지의 데이터 형식입니다.|
| event_hub_resource_id | *리소스 ID* | 이벤트를 보내도록 Event Grid 구성 된 이벤트 허브의 리소스 ID입니다. |
| storage_account_resource_id | *리소스 ID* | 수집할 데이터를 보유 하는 저장소 계정의 리소스 ID입니다. |
| consumer_group | *$Default* | 이벤트 허브의 소비자 그룹입니다.|
| location | *미국 중부* | 데이터 연결 리소스의 위치입니다.|

[!INCLUDE [data-explorer-data-connection-clean-resources-python](../../includes/data-explorer-data-connection-clean-resources-python.md)]