---
title: Azure Lab Services의 랩 계정 관리 | Microsoft Docs
description: Azure 구독에서 랩 계정을 만들거나 랩 계정을 모두 보거나 랩 계정을 삭제하는 방법을 알아봅니다.
services: lab-services
documentationcenter: na
author: spelluru
manager: ''
editor: ''
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/31/2019
ms.author: spelluru
ms.openlocfilehash: ee64780bca13bf497793dc90ad22d3eaf91949a6
ms.sourcegitcommit: c62a68ed80289d0daada860b837c31625b0fa0f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73606323"
---
# <a name="manage-lab-accounts-in-azure-lab-services"></a>Azure Lab Services의 랩 계정 관리 
Azure Lab Services에서 랩 계정은 교실 labs와 같은 관리 되는 랩 형식에 대 한 컨테이너입니다. 관리자는 Azure Lab Services를 사용하여 랩 계정을 설정하고 계정에 랩을 만들 수 있는 랩 소유자에게 액세스 권한을 제공합니다. 이 문서는 랩 계정을 만들거나, 모든 랩 계정을 보거나, 랩 계정을 삭제하는 방법을 설명합니다.

## <a name="create-a-lab-account"></a>랩 계정 만들기
다음 단계는 Azure Portal을 사용하여 Azure DevTest Labs로 랩 계정을 만드는 방법을 설명합니다. 

1. [Azure 포털](https://portal.azure.com)에 로그인합니다.
2. 왼쪽 메뉴에서 **모든 서비스**를 선택합니다. **Devops** 섹션에서 **랩 계정** 을 선택 합니다. `*`랩 계정 **옆에 있는 별표(** )를 선택하여 왼쪽 메뉴의 **즐겨찾기** 섹션에 추가합니다. 다음부터는 **즐겨찾기** 아래에서 **랩 계정**을 선택합니다.

    ![모든 서비스 -> 랩 계정](../media/tutorial-setup-lab-account/select-lab-accounts-service.png)
3. **랩 계정** 페이지에서 도구 모음에 있는 **추가**를 선택합니다. 

    ![랩 계정 페이지에서 추가 선택](../media/tutorial-setup-lab-account/add-lab-account-button.png)
4. **랩 계정** 페이지에서 다음 작업을 수행합니다. 
    1. **랩 계정 이름**에 이름을 입력합니다. 
    2. 랩 계정을 만들려는 **Azure 구독**을 선택합니다.
    3. **리소스 그룹**의 경우 **새로 만들기**를 선택하고 리소스 그룹의 이름을 입력합니다.
    4. **위치**에서 랩 계정을 만들 위치/지역을 선택합니다. 
    5. 기존 **공유 이미지 갤러리**를 선택하거나 새로 만듭니다. 다른 사용자가 다시 사용할 수 있도록 템플릿 VM을 공유 이미지 갤러리에 저장할 수 있습니다. 공유 이미지 갤러리에 대한 자세한 내용은 [Azure Lab Services에서 공유 이미지 갤러리 사용](how-to-use-shared-image-gallery.md)을 참조하세요.
    6. **가상 네트워크 피어 지정**에서 랩 네트워크에 대한 VNet(가상 네트워크) 피어 지정을 선택합니다. 이 계정에서 생성된 랩은 선택한 VNet에 연결되어 있으며 선택한 VNet의 리소스에 액세스할 수 있습니다. 
    7. 랩의 VM에 대해 **주소 범위**를 지정합니다. 주소 범위는 클래스 없는 CIDR (도메인 간 라우팅) 표기법 (예: 10.20.0.0/23)에 있어야 합니다. 랩의 가상 머신은 이 주소 범위에서 만들어집니다. 자세한 내용은 [랩의 VM에 대해 주소 범위 지정](how-to-configure-lab-accounts.md#specify-an-address-range-for-vms-in-the-lab)을 참조하세요.    
    8. **랩 작성자가 랩 위치를 선택하도록 허용** 필드에서 랩 작성자가 랩의 위치를 선택할 수 있도록 할지 여부를 지정합니다. 이 옵션은 기본적으로 '사용 안 함'으로 설정되어 있습니다. 이 기능이 '사용 안 함'으로 설정되면 랩 작성자가 만들고 있는 랩의 위치를 지정할 수 없습니다. 랩은 랩 계정과 가장 가까운 지리적 위치에 만들어집니다. 이 기능이 '사용'으로 설정되면 랩 작성자가 랩을 만들 때 위치를 선택할 수 있습니다.      
    9. **만들기**를 선택합니다. 

        ![랩 계정 만들기 창](../media/tutorial-setup-lab-account/lab-account-settings.png)
5. 도구 모음의 **종 모양 아이콘**(**알림**)을 선택하고 배포가 성공했는지 확인한 후 **리소스로 이동**을 선택합니다. 

    또는 **랩 계정** 페이지에서 **새로 고침**을 선택하고 생성된 랩 계정을 선택합니다. 

    ![랩 계정 만들기 창](../media/tutorial-setup-lab-account/go-to-lab-account.png)    
6. 다음과 같은 **랩 계정** 페이지가 표시됩니다.

    ![랩 계정 페이지](../media/tutorial-setup-lab-account/lab-account-page.png)

## <a name="view-lab-accounts"></a>랩 계정 보기
1. [Azure 포털](https://portal.azure.com)에 로그인합니다.
2. 메뉴에서 **모든 리소스**를 선택합니다. 
3. **형식**에 대한 **랩 계정**을 선택합니다. 
    구독, 리소스 그룹, 위치 및 태그별로 필터링할 수도 있습니다. 

    ![모든 리소스 -> 랩 계정](../media/how-to-manage-lab-accounts/all-resources-lab-accounts.png)

## <a name="view-and-manage-labs-in-the-lab-account"></a>랩 계정의 랩 보기 및 관리

1. **랩 계정** 페이지의 왼쪽 메뉴에서 **랩**을 선택합니다.

    ![계정의 랩](../media/how-to-manage-lab-accounts/labs-in-account.png)
1. 계정에는 다음 정보가 있는 **랩** 목록이 표시됩니다. 
    1. 랩의 이름
    2. 랩을 만든 날짜 
    3. 랩을 만든 사용자의 메일 주소 
    4. 랩에 허용되는 최대 사용자 수 
    5. 랩 상태 

## <a name="delete-a-lab-in-the-lab-account"></a>랩 계정에서 랩 삭제
이전 섹션의 지침에 따라 랩 계정의 랩 목록을 표시합니다.

1. **...(줄임표)** 를 선택하고 **삭제**를 선택합니다. 

    ![랩 삭제 - 단추](../media/how-to-manage-lab-accounts/delete-lab-button.png)
2. 경고 메시지에서 **예**를 선택합니다. 

    ![랩 삭제 확인](../media/how-to-manage-lab-accounts/confirm-lab-delete.png)

## <a name="delete-a-lab-account"></a>랩 계정 삭제
랩 계정을 목록으로 표시하는 이전 섹션의 지침을 따릅니다. 다음 지침에 따라 랩 계정을 삭제합니다. 

1. 삭제하려는 **랩 계정**을 선택합니다. 
2. 도구 모음에서 **삭제**를 선택합니다. 

    ![랩 계정 -> 삭제 단추](../media/how-to-manage-lab-accounts/delete-button.png)
1. 확인을 위해 **예**를 입력합니다.
1. **삭제**를 선택합니다. 

    ![랩 계정 삭제 - 확인](../media/how-to-manage-lab-accounts/delete-lab-account-confirmation.png)

> [!NOTE]
> Az. 연구원 서비스 PowerShell 모듈 (미리 보기)을 사용 하 여 랩 계정을 관리할 수도 있습니다. 자세한 내용은 [GitHub의 Az 서비스 홈 페이지](https://github.com/Azure/azure-devtestlab/tree/master/samples/ClassroomLabs/Modules/Library)를 참조 하세요.

## <a name="next-steps"></a>다음 단계
[랩 계정을 구성 하는 방법](how-to-configure-lab-accounts.md)문서를 참조 하세요.