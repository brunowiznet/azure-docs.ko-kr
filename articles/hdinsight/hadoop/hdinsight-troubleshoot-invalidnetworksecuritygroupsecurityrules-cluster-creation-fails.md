---
title: InvalidNetworkSecurityGroupSecurityRules 오류-Azure HDInsight
description: 클러스터 만들기가 실패 하 고 오류 오류 InvalidNetworkSecurityGroupSecurityRules
ms.service: hdinsight
ms.topic: troubleshooting
author: hrasheed-msft
ms.author: hrasheed
ms.reviewer: jasonh
ms.date: 07/31/2019
ms.openlocfilehash: a73e1e9f7a9c017dd29b627a24c25ae2e064c0a9
ms.sourcegitcommit: 8e9a6972196c5a752e9a0d021b715ca3b20a928f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/11/2020
ms.locfileid: "75894140"
---
# <a name="scenario-invalidnetworksecuritygroupsecurityrules---cluster-creation-fails-in-azure-hdinsight"></a>시나리오: InvalidNetworkSecurityGroupSecurityRules-Azure HDInsight에서 클러스터 만들기 실패

이 문서에서는 Azure HDInsight 클러스터와 상호 작용할 때 문제에 대 한 문제 해결 단계 및 가능한 해결 방법을 설명 합니다.

## <a name="issue"></a>문제

"서브넷으로 구성 된 네트워크 보안 그룹의 보안 규칙에서 필요한 인바운드 및/또는 아웃 바운드 연결을 허용 하지 않습니다."와 비슷한 설명이 포함 된 오류 코드 `InvalidNetworkSecurityGroupSecurityRules` 표시 됩니다.

## <a name="cause"></a>원인

클러스터에 대해 구성 된 인바운드 [네트워크 보안 그룹](../../virtual-network/virtual-network-vnet-plan-design-arm.md) 규칙에 문제가 있을 수 있습니다.

## <a name="resolution"></a>해상도

Azure Portal로 이동 하 여 클러스터가 배포 되는 서브넷과 연결 된 NSG를 식별 합니다. **인바운드 보안 규칙** 섹션에서 규칙이 [여기](../hdinsight-plan-virtual-network-deployment.md#hdinsight-ip)에 언급 된 IP 주소에 대 한 포트 443에 대 한 인바운드 액세스를 허용 하는지 확인 합니다.

## <a name="next-steps"></a>다음 단계

문제가 표시되지 않거나 문제를 해결할 수 없는 경우 다음 채널 중 하나를 방문하여 추가 지원을 받으세요.

* Azure [커뮤니티 지원을](https://azure.microsoft.com/support/community/)통해 azure 전문가 로부터 답변을 받으세요.

* [@AzureSupport](https://twitter.com/azuresupport) 연결-Azure 커뮤니티를 적절 한 리소스 (답변, 지원 및 전문가)에 연결 하 여 고객 환경을 개선 하기 위한 공식 Microsoft Azure 계정입니다.

* 도움이 더 필요한 경우 [Azure Portal](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade/)에서 지원 요청을 제출할 수 있습니다. 메뉴 모음에서 **지원** 을 선택 하거나 **도움말 + 지원** 허브를 엽니다. 자세한 내용은 [Azure 지원 요청을 만드는 방법](https://docs.microsoft.com/azure/azure-portal/supportability/how-to-create-azure-support-request)을 참조 하세요. 구독 관리 및 청구 지원에 대 한 액세스는 Microsoft Azure 구독에 포함 되며, [Azure 지원 계획](https://azure.microsoft.com/support/plans/)중 하나를 통해 기술 지원이 제공 됩니다.
