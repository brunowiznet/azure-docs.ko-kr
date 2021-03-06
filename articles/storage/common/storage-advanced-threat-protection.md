---
title: Advanced threat protection 구성
titleSuffix: Azure Storage
description: Azure Storage에 대 한 고급 위협 방지를 구성 하 여 계정 활동의 변칙을 감지 하 고 잠재적으로 위험한 계정 액세스 시도에 대 한 통지를 받습니다.
services: storage
author: tamram
ms.service: storage
ms.topic: conceptual
ms.date: 09/16/2019
ms.author: tamram
ms.reviewer: cbrooks
ms.openlocfilehash: 8efbf2107104f31bcfc5e4e5669dbed1835a034b
ms.sourcegitcommit: f4f626d6e92174086c530ed9bf3ccbe058639081
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75457404"
---
# <a name="configure-advanced-threat-protection-for-azure-storage"></a>Azure Storage에 대 한 advanced threat protection 구성

Azure Storage에 대 한 Advanced threat protection은 저장소 계정에 액세스 하거나 악용 하려는 비정상적이 고 잠재적으로 유해한 시도를 감지 하는 추가 보안 인텔리전스 계층을 제공 합니다. 이 보호 계층을 사용 하면 보안 전문가가 되거나 보안 모니터링 시스템을 관리 하지 않고도 위협을 해결할 수 있습니다.

보안 경고는 활동의 비정상 현상이 발생할 때 트리거됩니다. 이러한 보안 경고는 [Azure Security Center](https://azure.microsoft.com/services/security-center/)와 통합 되며, 의심 스러운 활동 및 위협 조사 및 해결 방법에 대 한 권장 사항을 포함 하 여 구독 관리자에 게 전자 메일을 통해 전송 됩니다.

> [!NOTE]
> Azure Storage에 대 한 Advanced threat protection은 현재 Blob 저장소에만 사용할 수 있습니다. Azure 정부 및 소 버린 클라우드 지역에서 사용할 수 없습니다. 무료 30 일 평가판을 비롯 한 가격 정보는 [Azure Security Center 가격 책정 페이지]( https://azure.microsoft.com/pricing/details/security-center/)를 참조 하세요.

위협 감지를 위해 Blob 저장소에 대 한 읽기, 쓰기 및 삭제 요청의 진단 로그를 Azure Storage 수집에 대 한 고급 위협 방지 Advanced threat protection에서 경고를 조사 하려면 스토리지 분석 로깅을 사용 하 여 관련 저장소 작업을 볼 수 있습니다. 자세한 내용은 [Azure Portal에서 저장소 계정 모니터링](storage-monitor-storage-account.md#configure-logging)의 **로깅 구성** 을 참조 하세요.

## <a name="set-up-advanced-threat-protection"></a>Advanced threat protection 설정

고급 위협 방지는 저장소 계정에 대해 기본적으로 사용 하도록 설정 됩니다. 다음 섹션에서 설명 하는 여러 가지 방법으로 advanced threat protection을 구성할 수 있습니다.

### <a name="portaltabazure-portal"></a>[포털](#tab/azure-portal)

1. [Azure Portal](https://portal.azure.com/)을 시작합니다.
1. Azure Storage 계정으로 이동 합니다. **설정**아래에서 **고급 보안**을 선택 합니다.
1. 고급 보안 구성 페이지에서 **설정** 링크를 선택 합니다.
1. **고급 보안** 을 **켜기**로 설정 합니다.
1. **저장** 을 클릭 하 여 새로운 또는 업데이트 된 정책을 저장 합니다.

    ![Azure Storage Advanced Threat Protection 켜기](./media/storage-advanced-threat-protection/storage-advanced-threat-protection-turn-on.png)

### <a name="azure-security-centertabazure-security-center"></a>[Azure Security Center](#tab/azure-security-center)

Azure Security Center 표준 계층을 구독할 때 advanced threat protection은 모든 저장소 계정에 자동으로 설정 됩니다. 다음과 같이 특정 구독에서 저장소 계정에 대 한 고급 위협 방지를 사용 하거나 사용 하지 않도록 설정할 수 있습니다.

1. [Azure Portal](https://portal.azure.com)에서 **Azure Security Center** 를 시작 합니다.
1. 주 메뉴에서 **가격 책정 & 설정**을 클릭 합니다.
1. 저장소 계정에 대해 위협 방지를 사용 하거나 사용 하지 않도록 설정할 구독을 클릭 합니다.

    ![구독 선택](./media/storage-advanced-threat-protection/storage-advanced-threat-protection-subscription.png)

1. **가격 책정 계층**을 클릭합니다.
1. **리소스 유형별 가격 책정 계층 선택** 섹션의 **저장소 계정** 행에서 **사용** 또는 **사용 안 함**을 클릭 합니다.

    ![Security Center에서 ATP 사용](./media/storage-advanced-threat-protection/storage-advanced-threat-protection-pricing2.png)
1. **저장**을 클릭합니다.

### <a name="templatetabtemplate"></a>[템플릿](#tab/template)

Azure Resource Manager 템플릿을 사용 하 여 advanced threat protection이 설정 된 Azure Storage 계정을 배포 합니다. 자세한 내용은 [advanced threat protection을 사용 하는 저장소 계정](https://azure.microsoft.com/resources/templates/201-storage-advanced-threat-protection-create/)을 참조 하세요.

### <a name="azure-policytabazure-policy"></a>[Azure Policy](#tab/azure-policy)

Azure Policy를 사용 하 여 특정 구독 또는 리소스 그룹의 저장소 계정에서 advanced threat protection을 사용 하도록 설정 합니다.

1. Azure **정책 정의** 페이지를 시작 합니다.

1. **저장소 계정에 Advanced Threat Protection 배포** 정책을 검색 합니다.

     ![검색 정책](./media/storage-advanced-threat-protection/storage-atp-policy-definitions.png)

1. Azure 구독 또는 리소스 그룹을 선택 합니다.

    ![구독 또는 그룹 선택](./media/storage-advanced-threat-protection/storage-atp-policy2.png)

1. 정책을 할당 합니다.

    ![정책 정의 페이지](./media/storage-advanced-threat-protection/storage-atp-policy1.png)

### <a name="rest-apitabrest-api"></a>[REST API](#tab/rest-api)

Rest API 명령을 사용 하 여 특정 저장소 계정에 대 한 advanced threat protection 설정을 만들거나 업데이트 하거나 가져옵니다.

* [Advanced threat protection-만들기](https://docs.microsoft.com/rest/api/securitycenter/advancedthreatprotection/create)
* [Advanced threat protection-Get](https://docs.microsoft.com/rest/api/securitycenter/advancedthreatprotection/get)

### <a name="powershelltabazure-powershell"></a>[PowerShell](#tab/azure-powershell)

다음 PowerShell cmdlet을 사용 합니다.

* [Advanced threat protection 사용](https://docs.microsoft.com/powershell/module/az.security/enable-azsecurityadvancedthreatprotection)
* [Advanced threat protection 가져오기](https://docs.microsoft.com/powershell/module/az.security/get-azsecurityadvancedthreatprotection)
* [Advanced threat protection 사용 안 함](https://docs.microsoft.com/powershell/module/az.security/disable-azsecurityadvancedthreatprotection)

---

## <a name="explore-security-anomalies"></a>보안 비정상 탐색

스토리지 작업에서 잘못된 부분이 발생하면 의심스러운 보안 이벤트에 대한 정보가 포함된 이메일 알림을 받게 됩니다. 이벤트 세부 정보에는 다음과 같은 내용이 포함됩니다.

* 변칙의 특성
* 스토리지 계정 이름입니다.
* 이벤트 시간
* 저장소 유형
* 가능한 원인
* 조사 단계
* 수정 단계

또한 이메일에는 가능한 원인에 대한 세부 정보와 잠재적 위협을 조사하고 완화하기 위한 권장 조치가 포함됩니다.

![Azure Storage Advanced Threat Protection 경고 이메일](./media/storage-advanced-threat-protection/storage-advanced-threat-protection-alert-email.png)

Azure Security Center의 [보안 경고 타일](../../security-center/security-center-managing-and-responding-alerts.md)에서 현재 보안 경고를 검토 및 관리할 수 있습니다. 특정 경고를 클릭하면 현재 위협을 조사하고 향후 위협을 해결하기 위한 추가 세부 정보 및 조치가 제공됩니다.

![Azure Storage Advanced Threat Protection 경고 이메일](./media/storage-advanced-threat-protection/storage-advanced-threat-protection-alert.png)

## <a name="protection-alerts"></a>보호 경고

경고는 평소와 다르고 잠재적 위험이 있는 액세스 시도 또는 스토리지 계정 악용에 의해 생성됩니다. Azure Storage에 대 한 경고 목록은 [Azure Security Center 경고에서 데이터 서비스에 대 한 위협 검색](../../security-center/security-center-alerts-data-services.md#azure-storage) 의 **저장소** 섹션을 참조 하세요.

## <a name="next-steps"></a>다음 단계

* [Azure Storage 계정의 로그](/rest/api/storageservices/About-Storage-Analytics-Logging) 에 대해 자세히 알아보기
* [Azure Security Center](../../security-center/security-center-intro.md)에 대한 자세한 정보
