---
title: B2B 메시지에 대 한 사용자 지정 추적 스키마
description: 엔터프라이즈 통합 팩을 사용하여 Azure Logic Apps 통합 계정에서 B2B 메시지를 모니터링하는 사용자 지정 추적 스키마 만들기
services: logic-apps
ms.suite: integration
author: divyaswarnkar
ms.author: divswa
ms.reviewer: jonfan, estfan, logicappspm
ms.topic: article
ms.date: 01/27/2017
ms.openlocfilehash: 7d7c5ef9e9a86c8b061a56fe41c0c8bbfc5ddbb3
ms.sourcegitcommit: 76b48a22257a2244024f05eb9fe8aa6182daf7e2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2019
ms.locfileid: "74792789"
---
# <a name="create-custom-tracking-schemas-that-monitor-end-to-end-workflows-in-azure-logic-apps"></a>Azure Logic Apps에서 엔드투엔드 워크플로를 모니터링하는 사용자 지정 추적 스키마 만들기

기업 간 워크플로의 다양한 부분에 대해 사용할 수 있는 기본 제공 추적(예: AS2 또는 X12 메시지 추적)이 있습니다. 논리 앱, BizTalk Server, SQL Server 또는 다른 계층을 포함하는 워크플로를 만들 경우 워크플로의 시작부터 끝까지 이벤트를 기록하는 사용자 지정 추적을 사용하도록 설정할 수 있습니다. 

이 문서에서는 논리 앱 외부의 계층에서 사용할 수 있는 사용자 지정 코드를 제공합니다. 

## <a name="custom-tracking-schema"></a>사용자 지정 추적 스키마

```json
{
   "sourceType": "",
   "source": {
      "workflow": {
         "systemId": ""
      },
      "runInstance": {
         "runId": ""
      },
      "operation": {
         "operationName": "",
         "repeatItemScopeName": "",
         "repeatItemIndex": "",
         "trackingId": "",
         "correlationId": "",
         "clientRequestId": ""
      }
   },
   "events": [
      {
         "eventLevel": "",
         "eventTime": "",
         "recordType": "",
         "record": {                
         }
      }
   ]
}
```

| 자산 | 필수 | Type | 설명 |
| --- | --- | --- | --- |
| sourceType | yes |   | 실행 원본의 유형입니다. 허용되는 값은**Microsoft.Logic/workflows** 및 **custom**입니다. |
| source | yes |   | 소스 형식이 **Microsoft.Logic/workflows**이면 소스 정보는 이 스키마를 따라야 합니다. 소스 형식이 **custom**이면 스키마는 JToken입니다. |
| systemId | yes | string | 논리 앱 시스템 ID입니다. |
| runId | yes | string | 논리 앱 실행 ID입니다. |
| operationName | yes | string | 작업의 이름(예: action 또는 trigger)입니다. |
| repeatItemScopeName | yes | string | 작업이 `foreach`/`until` 루프에 있으면 아이템 이름을 반복합니다. |
| repeatItemIndex | yes | 정수 | 작업이 `foreach`/`until` 루프에 있는지의 여부입니다. 반복된 항목 인덱스를 나타냅니다. |
| trackingId | 아닙니다. | string | 메시지에 상호 연결할 추적 ID입니다. |
| correlationId | 아닙니다. | string | 메시지에 상호 연결할 상관 관계 ID입니다. |
| clientRequestId | 아닙니다. | string | 클라이언트는 메시지에 상호 연결하기 위해 이 항목을 채울 수 있습니다. |
| eventLevel | yes |   | 이벤트의 수준입니다. |
| eventTime | yes |   | UTC 형식 YYYY-MM-DDTHH:MM:SS.00000Z의 이벤트 시간입니다. |
| recordType | yes |   | 트랙 레코드의 유형입니다. 허용되는 값은 **custom**입니다. |
| record | yes |   | 사용자 지정 레코드 유형입니다. 허용된 형식은 JToken입니다. |
||||

## <a name="b2b-protocol-tracking-schemas"></a>B2B 프로토콜 추적 스키마

스키마를 추적하는 B2B 프로토콜에 대한 정보는 다음을 참조하세요.

* [AS2 추적 스키마](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)   
* [X12 추적 스키마](logic-apps-track-integration-account-x12-tracking-schema.md)

## <a name="next-steps"></a>다음 단계

* [B2B 메시지 모니터링](logic-apps-monitor-b2b-message.md)에 대해 자세히 알아봅니다.
* [Azure Monitor 로그에서 B2B 메시지 추적](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) 에 대해 알아봅니다.
