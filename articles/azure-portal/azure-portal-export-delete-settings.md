---
title: Azure Portal 설정 내보내기 또는 삭제 | Microsoft Docs
description: Azure Portal에서 사용자 설정, 개인 대시보드 및 사용자 지정 설정을 내보내거나 삭제할 수 있는 방법에 대해 알아봅니다.
services: azure-portal
keywords: ''
author: santhoshsomayajula
ms.date: 04/08/2019
ms.topic: conceptual
ms.service: azure-portal
ms.custom: ''
manager: mtillman
ms.author: mblythe
ms.openlocfilehash: f033af37985077f4d8df9d541b55764df0c75eda
ms.sourcegitcommit: f788bc6bc524516f186386376ca6651ce80f334d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/03/2020
ms.locfileid: "75640179"
---
# <a name="export-or-delete-user-settings"></a>사용자 설정 내보내기 또는 삭제

Azure Portal의 설정 및 기능을 사용 하 여 사용자 지정 환경을 만들 수 있습니다. 사용자 지정 설정에 대 한 정보는 Azure에 저장 됩니다. 다음 사용자 데이터를 내보내거나 삭제할 수 있습니다.

* Azure Portal의 개인 대시보드
* 즐겨 찾는 구독 또는 디렉터리와 같은 사용자 설정 및 마지막으로 로그인 한 디렉터리
* 테마 및 기타 사용자 지정 포털 설정

설정을 삭제 하기 전에 내보내고 검토 하는 것이 좋습니다. 대시보드를 다시 작성 하거나 사용자 지정 설정을 다시 실행 하는 것은 시간이 많이 걸릴 수 있습니다.

[!INCLUDE [GDPR-related guidance](../../includes/gdpr-intro-sentence.md)]

## <a name="export-or-delete-your-portal-settings"></a>포털 설정 내보내기 또는 삭제

1. [Azure Portal](https://portal.azure.com)에 로그인합니다.
2. 포털의 헤더에서 **설정**을 선택 합니다.

    ![포털 설정 기어를 보여주는 스크린샷](media/azure-portal-export-delete-settings/azure-portal-settings-icon.png)

3. **모든 설정 내보내기** 또는 **모든 설정 및 프라이빗 대시보드 삭제**를 선택합니다.

    ![포털 내보내기 및 삭제 설정을 보여 주는 스크린샷](media/azure-portal-export-delete-settings/azure-portal-export-delete-settings.png)

      다음 표에서는 이러한 작업을 설명 합니다.

      | 실행력 | Description |
      | --- | --- |
      | **모든 설정 내보내기** | 색 테마, 즐겨찾기, 개인 대시보드 등의 사용자 설정이 포함 된 json 파일을 만듭니다.|
      | **모든 설정 및 프라이빗 대시보드 삭제** | 개인 대시보드 및 포털에 대 한 기타 사용자 지정 설정에 대 한 모든 링크를 삭제 합니다. |

> [!NOTE]
> 사용자 설정의 동적 특성과 데이터 손상의 위험 때문에, json 파일에서 설정을 가져올 수 없습니다.
>
>


## <a name="next-steps"></a>다음 단계

* [Azure 대시보드 만들기 및 공유](azure-portal-dashboard-share-access.md)
* [즐겨찾기 추가, 제거 및 정렬](azure-portal-add-remove-sort-favorites.md)
