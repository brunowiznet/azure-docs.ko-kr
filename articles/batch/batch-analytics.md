---
title: Azure Batch 분석 | Microsoft Docs
description: Azure Batch 분석에 대한 참조입니다.
services: batch
author: ju-shim
manager: gwallace
ms.assetid: ''
ms.service: batch
ms.topic: article
ms.tgt_pltfrm: ''
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: jushiman
ms.openlocfilehash: 39a8bfb6a48bf55ae9f2ec36f7716959e6ada9dd
ms.sourcegitcommit: dbcc4569fde1bebb9df0a3ab6d4d3ff7f806d486
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/15/2020
ms.locfileid: "76027392"
---
# <a name="batch-analytics"></a>Batch 분석
Batch 분석의 항목에는 Batch 서비스 리소스에 사용할 수 있는 이벤트 및 경고에 대한 참조 정보가 포함되어 있습니다.

Batch 진단 로그를 활성화하고 사용하는 방법에 대한 자세한 내용은 [Azure Batch 진단 로깅](https://azure.microsoft.com/documentation/articles/batch-diagnostics/)을 참조하세요.

## <a name="diagnostic-logs"></a>진단 로그

Azure Batch 서비스는 특정 Batch 리소스의 수명 동안 다음과 같은 진단 로그 이벤트를 내보냅니다.

**서비스 로그 이벤트**
* [풀 만들기](batch-pool-create-event.md)
* [풀 삭제 시작](batch-pool-delete-start-event.md)
* [풀 삭제 완료](batch-pool-delete-complete-event.md)
* [풀 크기 조정 시작](batch-pool-resize-start-event.md)
* [풀 크기 조정 완료](batch-pool-resize-complete-event.md)
* [작업 시작](batch-task-start-event.md)
* [작업 완료](batch-task-complete-event.md)
* [작업 실패](batch-task-fail-event.md)