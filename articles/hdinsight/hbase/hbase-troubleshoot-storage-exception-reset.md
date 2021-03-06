---
title: Azure HDInsight에서 연결을 다시 설정한 후의 저장소 예외
description: Azure HDInsight에서 연결을 다시 설정한 후의 저장소 예외
ms.service: hdinsight
ms.topic: troubleshooting
author: hrasheed-msft
ms.author: hrasheed
ms.reviewer: jasonh
ms.date: 08/08/2019
ms.openlocfilehash: a7af6407191577112f936bfb9048985e85c868ea
ms.sourcegitcommit: 8e9a6972196c5a752e9a0d021b715ca3b20a928f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/11/2020
ms.locfileid: "75887226"
---
# <a name="scenario-storage-exception-after-connection-reset-in-azure-hdinsight"></a>시나리오: Azure HDInsight에서 연결을 다시 설정한 후 저장소 예외

이 문서에서는 Azure HDInsight 클러스터와 상호 작용할 때 문제에 대 한 문제 해결 단계 및 가능한 해결 방법을 설명 합니다.

## <a name="issue"></a>문제

새 Apache HBase 테이블을 만들 수 없습니다.

## <a name="cause"></a>원인

테이블 잘림 프로세스가 진행 되는 동안 저장소 연결 문제가 발생 했습니다. HBase 메타 데이터 테이블에서 테이블 항목이 삭제 되었습니다. Blob 파일이 하나 이지만 모두 삭제 되었습니다.

`/hbase/data/default/ThatTable` 라는 폴더 blob는 저장소에 저장 되지 않습니다. WASB 드라이버는 위의 blob 파일에 존재 하는 것을 발견 하 고 부모 폴더가 존재 한다고 가정 하 여 `/hbase/data/default/ThatTable` 이라는 blob을 만들 수 없습니다. 따라서 테이블을 만드는 작업이 실패 합니다.

## <a name="resolution"></a>해상도

1. Apache Ambari UI에서 활성 HMaster를 다시 시작 합니다. 이렇게 하면 두 개의 대기 HMaster 중 하나가 활성 상태가 되 고 새 활성 HMaster가 메타 데이터 테이블 정보를 다시 로드 합니다. 따라서 HMaster UI에 `already-deleted` 테이블이 표시 되지 않습니다.

1. 클라우드 탐색기 또는 `hdfs dfs -ls /xxxxxx/yyyyy`같은 명령을 실행 하는 등의 UI 도구에서 고아 blob 파일을 찾을 수 있습니다. `hdfs dfs -rmr /xxxxx/yyyy`를 실행 하 여 해당 blob을 삭제 합니다. `hdfs dfs -rmr /hbase/data/default/ThatTable/ThatFile`)을 입력합니다.

이제 HBase에서 동일한 이름을 사용 하 여 새 테이블을 만들 수 있습니다.

## <a name="next-steps"></a>다음 단계

문제가 표시되지 않거나 문제를 해결할 수 없는 경우 다음 채널 중 하나를 방문하여 추가 지원을 받으세요.

* Azure [커뮤니티 지원을](https://azure.microsoft.com/support/community/)통해 azure 전문가 로부터 답변을 받으세요.

* [@AzureSupport](https://twitter.com/azuresupport) 연결-고객 환경을 개선 하기 위한 공식 Microsoft Azure 계정입니다. Azure 커뮤니티를 적절 한 리소스 (답변, 지원 및 전문가)에 연결 합니다.

* 도움이 더 필요한 경우 [Azure Portal](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade/)에서 지원 요청을 제출할 수 있습니다. 메뉴 모음에서 **지원** 을 선택 하거나 **도움말 + 지원** 허브를 엽니다. 자세한 내용은 [Azure 지원 요청을 만드는 방법](https://docs.microsoft.com/azure/azure-portal/supportability/how-to-create-azure-support-request)을 참조 하세요. 구독 관리 및 청구 지원에 대 한 액세스는 Microsoft Azure 구독에 포함 되며, [Azure 지원 계획](https://azure.microsoft.com/support/plans/)중 하나를 통해 기술 지원이 제공 됩니다.
