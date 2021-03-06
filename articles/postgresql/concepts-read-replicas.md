---
title: 복제본 읽기-Azure Database for PostgreSQL-단일 서버
description: 이 문서에서는 Azure Database for PostgreSQL 단일 서버의 복제본 읽기 기능에 대해 설명 합니다.
author: rachel-msft
ms.author: raagyema
ms.service: postgresql
ms.topic: conceptual
ms.date: 12/03/2019
ms.openlocfilehash: 35d568afa0c45529b33b7918fd453213f432ba06
ms.sourcegitcommit: 76b48a22257a2244024f05eb9fe8aa6182daf7e2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2019
ms.locfileid: "74792285"
---
# <a name="read-replicas-in-azure-database-for-postgresql---single-server"></a>Azure Database for PostgreSQL의 복제본 읽기-단일 서버

읽기 복제본 기능을 사용하면 Azure Database for PostgreSQL 서버에서 읽기 전용 서버로 데이터를 복제할 수 있습니다. 마스터 서버에서 최대 5개의 복제본으로 복제할 수 있습니다. 복제본은 PostgreSQL 엔진 기본 복제 기술을 사용하여 비동기식으로 업데이트 됩니다.

복제본은 일반 Azure Database for PostgreSQL 서버와 비슷한 방식으로 관리하는 새로운 서버입니다. 읽기 복제본의 경우, vCore 및 스토리지에 프로비저닝된 컴퓨팅에 대한 비용이 GB/월 단위로 청구됩니다.

[복제본을 만들고 관리](howto-read-replicas-portal.md)하는 방법을 알아봅니다.

## <a name="when-to-use-a-read-replica"></a>읽기 복제본을 사용하는 경우
읽기 복제본 기능은 읽기 작업이 많은 워크로드의 성능과 규모를 향상시키는 데 도움이 됩니다. 읽기 워크로드를 복제본과 격리할 수 있고 쓰기 워크로드를 마스터로 보낼 수 있습니다.

일반적인 시나리오는 BI와 분석 워크로드가 보고를 위한 데이터 원본으로 읽기 복제본을 사용하도록 합니다.

복제본은 읽기 전용이기 때문에 마스터에 대한 쓰기 용량 부담을 직접적으로 줄이지는 못합니다. 이 기능은 쓰기 작업이 많은 워크로드를 대상으로 하지 않습니다.

읽기 복제본 기능은 PostgreSQL 동기식 복제를 사용합니다. 이 기능은 동기식 복제 시나리오를 위한 것이 아닙니다. 마스터와 복제본 간에는 측정 가능한 지연이 발생합니다. 복제본의 데이터는 결과적으로 마스터의 데이터와 일치하게 됩니다. 이러한 지연 시간을 수용할 수 있는 워크로드에 이 기능을 사용합니다.

## <a name="cross-region-replication"></a>지역 간 복제
마스터 서버에서 다른 지역에 읽기 복제본을 만들 수 있습니다. 지역 간 복제는 재해 복구 계획 또는 사용자에 게 더 가까운 데이터 가져오기 등의 시나리오에 유용할 수 있습니다.

[Azure Database for PostgreSQL 지역](https://azure.microsoft.com/global-infrastructure/services/?products=postgresql)에 마스터 서버를 둘 수 있습니다. 마스터 서버는 쌍을 이루는 지역 또는 유니버설 복제본 지역에 복제본이 있을 수 있습니다. 아래 그림은 마스터 영역에 따라 사용할 수 있는 복제본 영역을 보여 줍니다.

[![읽기 복제본 영역](media/concepts-read-replica/read-replica-regions.png)](media/concepts-read-replica/read-replica-regions.png#lightbox)

### <a name="universal-replica-regions"></a>유니버설 복제본 영역
마스터 서버가 있는 위치에 관계 없이 항상 다음 지역에서 읽기 복제본을 만들 수 있습니다. 다음은 범용 복제본 지역입니다.

오스트레일리아 동부, 오스트레일리아 남동쪽, 미국 중부, 동아시아, 미국 동부, 미국 동부 2, 일본 동부, 일본 서 부, 대한민국 중부, 한국 남부, 미국 중 북부, 북부 유럽, 미국 동부, 동남 아시아, 영국 남부, 영국 서부, 유럽 서부, 미국 서 부.

\* 미국 서 부 2는 지역 간 복제 위치로 일시적으로 사용할 수 없습니다.


### <a name="paired-regions"></a>쌍을 이루는 지역
유니버설 복제본 영역 외에도 마스터 서버의 Azure 쌍을 이루는 지역에서 읽기 복제본을 만들 수 있습니다. 지역 쌍을 모를 경우 [Azure 쌍을 이루는 지역 문서](../best-practices-availability-paired-regions.md)에서 자세히 알아볼 수 있습니다.

재해 복구 계획에 지역 간 복제본을 사용 하는 경우 다른 지역 중 하나가 아닌 쌍을 이루는 지역에 복제본을 만드는 것이 좋습니다. 쌍을 이루는 지역은 동시 업데이트를 방지 하 고 물리적 격리 및 데이터 상주의 우선 순위를 지정 합니다.  

다음 사항을 고려해 야 합니다. 

* 지역별 가용성: Azure Database for PostgreSQL는 미국 서 부 2, 프랑스 중부, 아랍에미리트 북부 및 독일 중부에서 사용할 수 있습니다. 그러나 쌍을 이루는 지역에는 사용할 수 없습니다.
    
* 단방향 쌍: 일부 Azure 지역은 한 방향 으로만 쌍을 이룹니다. 이러한 지역에는 인도 서 부, 브라질 남부가 포함 됩니다. 
   즉, 인도 서 부의 마스터 서버는 남부 인도에서 복제본을 만들 수 있습니다. 그러나 인도 남부의 마스터 서버는 인도 서 부에서 복제본을 만들 수 없습니다. 이는 인도 서 부의 보조 지역이 남부 인도 이지만 남부 인도의 보조 지역은 인도 서 부가 아니기 때문입니다.


## <a name="create-a-replica"></a>복제본 만들기
마스터 서버는 `azure.replication_support` 매개 변수를 **REPLICA**로 설정해야 합니다. 이 매개 변수가 변경되면 서버를 다시 시작해야 변경 내용이 적용됩니다. (`azure.replication_support` 매개 변수는 범용 및 메모리 최적화 계층에만 적용됩니다).

복제본 만들기 워크플로를 시작하면 빈 Azure Database for PostgreSQL 서버가 만들어집니다. 새 서버는 마스터 서버에 있는 데이터로 채워집니다. 생성 시간은 마스터의 데이터 양과 지난 주 전체 백업 이후의 시간에 따라 달라집니다. 시간은 몇 분에서 몇 시간까지 걸릴 수 있습니다.

모든 복제본은 저장소 [자동 증가](concepts-pricing-tiers.md#storage-auto-grow)에 대해 사용 하도록 설정 됩니다. 자동 증가 기능을 사용 하면 복제본에 복제 된 데이터를 유지 하 고 저장소 오류로 인 한 복제의 중단을 방지할 수 있습니다.

읽기 복제본 기능은 PostgreSQL의 물리적 복제(논리 복제 아님)를 사용합니다. 복제 슬롯을 사용하는 스트리밍 복제가 기본 작동 모드입니다. 필요한 경우 따라잡기 위해 로그 전달이 사용됩니다.

[Azure Portal에서 읽기 복제본을 만드는 방법](howto-read-replicas-portal.md)을 알아봅니다.

## <a name="connect-to-a-replica"></a>복제본에 연결
복제본을 만들면 마스터 서버의 방화벽 규칙 또는 VNet 서비스 엔드포인트를 상속하지 않습니다. 이러한 규칙은 복제본에 대해 별도로 설정해야 합니다.

복제본은 마스터 서버에서 해당 관리자 계정을 상속합니다. 마스터 서버의 모든 사용자 계정은 읽기 복제본으로 복제됩니다. 마스터 서버에서 사용 가능한 사용자 계정을 사용해야만 읽기 복제본에 연결할 수 있습니다.

일반 Azure Database for PostgreSQL 서버에서처럼 같이 해당 호스트 이름 및 유효한 사용자 계정을 사용하여 복제본에 연결할 수 있습니다. 관리자 사용자 이름 **myadmin**을 사용 하 여 **내 복제본** 이라는 서버에서 psql을 사용 하 여 복제본에 연결할 수 있습니다.

```
psql -h myreplica.postgres.database.azure.com -U myadmin@myreplica -d postgres
```

프롬프트가 표시되면 사용자 계정의 암호를 입력합니다.

## <a name="monitor-replication"></a>복제 모니터링
Azure Database for PostgreSQL는 복제를 모니터링 하기 위한 두 가지 메트릭을 제공 합니다. 두 메트릭은 복제본의 **최대 지연** 및 **복제본 지연**입니다. 이러한 메트릭을 보는 방법에 대 한 자세한 내용은 [복제본 모니터링 방법 문서의](howto-read-replicas-portal.md) **복제본 모니터링** 섹션을 참조 하세요.

**복제본 간 최대 지연** 수 메트릭은 마스터와 가장 지연 복제본 사이의 지연 시간 (바이트)을 보여 줍니다. 이 메트릭은 마스터 서버에서만 사용할 수 있습니다.

**복제본 지연** 메트릭은 마지막으로 재생 된 트랜잭션 이후 경과 된 시간을 보여 줍니다. 마스터 서버에서 트랜잭션이 발생하지 않으면 메트릭은 이 지연 시간을 반영합니다. 이 메트릭은 복제본 서버에만 사용할 수 있습니다. 복제본 지연 시간은 `pg_stat_wal_receiver` 보기에서 계산 됩니다.

```SQL
EXTRACT (EPOCH FROM now() - pg_last_xact_replay_timestamp());
```

복제본 지연 시간이 워크로드에 적합하지 않은 값에 도달하면 알리도록 경고를 설정하십시오. 

추가 인사이트를 얻으려면 마스터 서버를 직접 쿼리하여 모든 복제본의 복제 지연 시간(바이트)을 가져옵니다.

PostgreSQL 버전 10:

```SQL
select pg_wal_lsn_diff(pg_current_wal_lsn(), stat.replay_lsn) 
AS total_log_delay_in_bytes from pg_stat_replication;
```

PostgreSQL 버전 9.6 이전:

```SQL
select pg_xlog_location_diff(pg_current_xlog_location(), stat.replay_location) 
AS total_log_delay_in_bytes from pg_stat_replication;
```

> [!NOTE]
> 마스터 서버 또는 읽기 복제본이 다시 시작되면 다시 시작하여 따라잡는 데 걸리는 시간이 복제본 지연 시간 메트릭에 반영됩니다.

## <a name="stop-replication"></a>복제 중지
마스터 및 복제본 간의 복제를 중지할 수 있습니다. 중지 작업을 수행하면 복제본이 다시 시작되고 복제 설정이 제거됩니다. 마스터 서버와 읽기 복제본 사이에서 복제가 중지된 후에 복제본은 독립 실행형 서버가 됩니다. 독립 실행형 서버의 데이터는 복제 중지 명령이 시작될 때 복제본에서 사용할 수 있던 데이터입니다. 독립 실행형 서버는 마스터 서버를 따라잡지 않습니다.

> [!IMPORTANT]
> 독립 실행형 서버는 복제본으로 다시 만들 수 없습니다.
> 읽기 복제본에서 복제를 중지하기 전에 복제본에 필요한 모든 데이터가 있는지 확인하십시오.

복제를 중지 하면 복제본은 이전 마스터 및 기타 복제본에 대 한 모든 링크를 잃게 됩니다.

[복제본에 대한 복제를 중지](howto-read-replicas-portal.md)하는 방법을 알아봅니다.

## <a name="failover"></a>장애 조치(failover)
마스터 서버와 복제 서버 간에는 자동화 된 장애 조치 (failover)가 없습니다. 

복제는 비동기 이므로 마스터와 복제본 사이에 지연이 발생 합니다. 지연 시간은 마스터 서버에서 실행 되는 워크 로드의 양과 데이터 센터 간의 대기 시간 등 여러 가지 요소에 의해 영향을 받을 수 있습니다. 대부분의 경우 복제본 지연 범위는 몇 초에서 몇 분 사이입니다. 각 복제본에 대해 사용 가능한 메트릭 *복제본 지연*시간을 사용 하 여 실제 복제 지연 시간을 추적할 수 있습니다. 이 메트릭은 마지막으로 재생 된 트랜잭션 이후 경과 된 시간을 표시 합니다. 일정 기간 동안 복제본 지연 시간을 관찰 하 여 평균 지연 시간을 확인 하는 것이 좋습니다. 복제본 지연에 대 한 경고를 설정 하 여 예상 범위를 벗어나면 작업을 수행할 수 있습니다.

> [!Tip]
> 복제본으로 장애 조치 (failover) 하는 경우 마스터에서 복제본을 연결 취소 한 시간의 지연 시간은 손실 되는 데이터의 양을 표시 합니다.

복제본으로 장애 조치 (failover)를 결정 한 후에는 다음을 선택 합니다. 

1. 복제본에 대 한 복제 중지<br/>
   이 단계는 복제본 서버에서 쓰기를 허용할 수 있도록 하는 데 필요 합니다. 이 프로세스의 일부로 복제본 서버가 다시 시작 되 고 마스터에서 분리 됩니다. 복제 중지를 시작한 후 백 엔드 프로세스는 일반적으로 완료 하는 데 약 2 분이 걸립니다. 이 작업의 의미를 이해 하려면이 문서의 [복제 중지](#stop-replication) 섹션을 참조 하세요.
    
2. 응용 프로그램이 (이전) 복제본을 가리키도록 합니다.<br/>
   각 서버에는 고유한 연결 문자열이 있습니다. 마스터가 아닌 (이전) 복제본을 가리키도록 응용 프로그램을 업데이트 합니다.
    
응용 프로그램이 읽기 및 쓰기를 성공적으로 처리 하면 장애 조치 (failover)를 완료 한 것입니다. 응용 프로그램의 가동 중지 시간은 문제를 감지 하 고 위의 1 단계와 2 단계를 완료 하는 시기에 따라 달라 집니다.


## <a name="considerations"></a>고려 사항

이 섹션에서는 읽기 복제본 기능의 고려 사항에 대한 요약이 제공됩니다.

### <a name="prerequisites"></a>전제 조건
읽기 복제본을 만들기 전에, 마스터 서버에서 `azure.replication_support` 매개 변수를 **REPLICA**로 설정해야 합니다. 이 매개 변수가 변경되면 서버를 다시 시작해야 변경 내용이 적용됩니다. `azure.replication_support` 매개 변수는 범용 및 메모리 최적화 계층에만 적용됩니다.

### <a name="new-replicas"></a>새 복제본
읽기 복제본은 새로운 Azure Database for PostgreSQL 서버로 생성됩니다. 기존 서버를 복제본으로 만들 수 없습니다. 다른 읽기 복제본의 복제본은 만들 수 없습니다.

### <a name="replica-configuration"></a>복제본 구성
복제본은 마스터와 동일한 계산 및 저장소 설정을 사용 하 여 생성 됩니다. 복제본을 만든 후에는 마스터 서버와는 별도로 컴퓨팅 생성, vCore, 스토리지 및 백업 보존 기간 등의 일부 설정을 변경할 수 있습니다. 가격 책정도 기본 계층에서 다른 계층으로 또는 다른 계층에서 기본 계층으로 변경하는 경우 이외의 다른 방식으로 독립적으로 변경할 수 있습니다.

> [!IMPORTANT]
> 마스터 설정을 새 값으로 업데이트 하기 전에 복제본 구성을 같거나 큰 값으로 업데이트 합니다. 이렇게 하면 복제본이 마스터 변경 내용을 유지할 수 있습니다.

PostgreSQL에서는 읽기 복제본의 `max_connections` 매개 변수 값이 마스터 값보다 크거나 같아야 합니다. 그렇지 않으면 해당 복제본이 시작되지 않습니다. Azure Database for PostgreSQL에서 `max_connections` 매개 변수 값은 SKU에 기반합니다. 자세한 내용은 [Azure Database for PostgreSQL의 제한](concepts-limits.md)을 참조하세요. 

위에서 설명한 서버 값을 업데이트 하려고 하지만 한도를 따르지 않는 경우 오류가 표시 됩니다.

복제본을 만들 때 또는 나중에 마스터 서버에서 복제본으로의 방화벽 규칙, 가상 네트워크 규칙 및 매개 변수 설정이 상속 되지 않습니다.

### <a name="max_prepared_transactions"></a>max_prepared_transactions
[PostgreSQL](https://www.postgresql.org/docs/current/runtime-config-resource.html#GUC-MAX-PREPARED-TRANSACTIONS) 에는 읽기 복제본의 `max_prepared_transactions` 매개 변수 값이 마스터 값 보다 크거나 같아야 합니다. 그렇지 않으면 복제본이 시작 되지 않습니다. 마스터의 `max_prepared_transactions` 변경 하려면 먼저 복제본에서 변경 하십시오.

### <a name="stopped-replicas"></a>중지된 복제본
마스터 서버와 읽기 복제본 간의 복제를 중지하면 복제본이 다시 시작되어 변경 내용이 적용됩니다. 중지된 복제본은 읽기와 쓰기를 모두 허용하는 독립 실행형 서버가 됩니다. 독립 실행형 서버는 복제본으로 다시 만들 수 없습니다.

### <a name="deleted-master-and-standalone-servers"></a>삭제된 마스터 및 독립 실행형 서버
마스터 서버를 삭제하면 이 서버의 모든 읽기 복제본이 독립 실행형 서버가 됩니다. 이 변경 내용을 반영하기 위해 복제본이 다시 시작됩니다.

## <a name="next-steps"></a>다음 단계
* [Azure Portal에서 읽기 복제본을 만들고 관리하는 방법](howto-read-replicas-portal.md)을 알아봅니다.
* [Azure CLI 및 REST API에서 읽기 복제본을 만들고 관리](howto-read-replicas-cli.md)하는 방법에 대해 알아봅니다.
