---
title: Azure HPC 캐시에 저장소 추가
description: Azure HPC 캐시가 장기 파일 저장소에 대해 온-프레미스 NFS 시스템 또는 Azure Blob 컨테이너를 사용할 수 있도록 저장소 대상을 정의 하는 방법
author: ekpgh
ms.service: hpc-cache
ms.topic: conceptual
ms.date: 12/30/2019
ms.author: rohogue
ms.openlocfilehash: 75d657fd9f3ee13c331450b324fd3b99e9cb6ca5
ms.sourcegitcommit: f788bc6bc524516f186386376ca6651ce80f334d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/03/2020
ms.locfileid: "75647227"
---
# <a name="add-storage-targets"></a>스토리지 대상 추가

*저장소 대상은* Azure HPC 캐시 인스턴스를 통해 액세스 되는 파일에 대 한 백 엔드 저장소입니다. NFS 저장소 (예: 온-프레미스 하드웨어 시스템)를 추가 하거나 Azure Blob에 데이터를 저장할 수 있습니다.

한 캐시에 대해 최대 10 개의 서로 다른 저장소 대상을 정의할 수 있습니다. 캐시는 하나의 집계 된 네임 스페이스에 있는 모든 저장소 대상을 제공 합니다.

저장소 내보내기는 캐시의 가상 네트워크에서 액세스할 수 있어야 합니다. 온-프레미스 하드웨어 저장소의 경우 NFS 저장소 액세스의 호스트 이름을 확인할 수 있는 DNS 서버를 설정 해야 할 수 있습니다. 자세한 내용은 [DNS 액세스](hpc-cache-prereqs.md#dns-access)를 참조 하세요.

캐시를 만든 후 저장소 대상을 추가 합니다. 이 절차는 Azure Blob storage를 추가 하는지 아니면 NFS 내보내기를 추가 하는지에 따라 약간 다릅니다. 각각에 대 한 세부 정보는 아래와 같습니다.

## <a name="open-the-storage-targets-page"></a>저장소 대상 페이지 열기

Azure Portal에서 캐시 인스턴스를 열고 왼쪽 세로 막대에서 **저장소 대상** 을 클릭 합니다. 저장소 대상 페이지에는 기존의 모든 대상이 나열 되며 새 대상이 추가 될 수 있는 링크가 제공 됩니다.

![범주 제목 설정 및 모니터링의 제목 구성 아래에 있는 사이드바의 저장소 대상 링크 스크린샷](media/hpc-cache-storage-targets-sidebar.png)

## <a name="add-a-new-azure-blob-storage-target"></a>새 Azure Blob 저장소 대상 추가

새 Blob 저장소 대상에는 빈 Blob 컨테이너 또는 Azure HPC 캐시 클라우드 파일 시스템 형식의 데이터로 채워지는 컨테이너가 필요 합니다. [Azure blob storage로 데이터 이동](hpc-cache-ingest.md)에서 blob 컨테이너를 미리 로드 하는 방법에 대해 자세히 알아보세요.

이 페이지를 추가 하기 바로 전에이 페이지에서 새 컨테이너를 만들 수 있습니다.

Azure Blob 컨테이너를 정의 하려면이 정보를 입력 합니다.

![새 Azure Blob 저장소 대상에 대 한 정보로 채워진 저장소 대상 추가 페이지의 스크린샷](media/hpc-cache-add-blob.png)

<!-- need to replace screenshot after note text is updated with both required RBAC roles and also with correct search term -->

* **저장소 대상 이름** -Azure HPC 캐시에서이 저장소 대상을 식별 하는 이름을 설정 합니다.
* **대상 유형** - **Blob**을 선택 합니다.
* **저장소 계정** -사용 하려는 계정을 선택 합니다.

  [액세스 역할 추가](#add-the-access-control-roles-to-your-account)에 설명 된 대로 저장소 계정에 액세스 하려면 캐시 인스턴스에 권한을 부여 해야 합니다.

  사용할 수 있는 저장소 계정 종류에 대 한 자세한 내용은 [Blob 저장소 요구 사항](hpc-cache-prereqs.md#blob-storage-requirements)을 참조 하세요.

* **저장소 컨테이너** -이 대상에 대 한 Blob 컨테이너를 선택 하거나 **새로 만들기**를 클릭 합니다.

  ![새 컨테이너의 이름 및 액세스 수준 (개인)을 지정 하는 대화 상자의 스크린샷](media/add-blob-new-container.png)

* **가상 네임 스페이스 경로** -이 저장소 대상에 대 한 클라이언트 쪽 파일 경로를 설정 합니다. 가상 네임 스페이스 기능에 대해 자세히 알아보려면 [집계 된 네임 스페이스 구성](hpc-cache-namespace.md) 을 참조 하세요.

완료 되 면 **확인** 을 클릭 하 여 저장소 대상을 추가 합니다.

> [!NOTE]
> 저장소 계정 방화벽이 "선택한 네트워크"로만 액세스를 제한 하도록 설정 된 경우에는 [Blob storage 계정 방화벽 설정](hpc-cache-blob-firewall-fix.md)에 설명 된 임시 해결 방법을 사용 합니다.

### <a name="add-the-access-control-roles-to-your-account"></a>계정에 액세스 제어 역할 추가

Azure HPC 캐시는 [RBAC (역할 기반 액세스 제어)](https://docs.microsoft.com/azure/role-based-access-control/index) 를 사용 하 여 azure Blob 저장소 대상에 대 한 저장소 계정에 액세스 하도록 캐시 서비스에 권한을 부여 합니다.

저장소 계정 소유자는 "HPC 캐시 리소스 공급자" 사용자에 대 한 역할 [저장소 계정 참가자](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#storage-account-contributor) 및 [저장소 Blob 데이터 참가자](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#storage-blob-data-contributor) 를 명시적으로 추가 해야 합니다.

이렇게 하려면 나중에 또는 Blob 저장소 대상을 추가 하는 페이지의 링크를 클릭 하면 됩니다. 역할 설정이 Azure 환경을 통해 전파 되는 데 최대 5 분이 걸릴 수 있으므로 저장소 대상을 만들기 전에 역할을 추가한 후 몇 분 정도 기다려야 합니다.

RBAC 역할을 추가 하는 단계:

1. 저장소 계정에 대 한 **액세스 제어 (IAM)** 페이지를 엽니다. ( **저장소 대상 추가** 페이지의 링크를 선택 하면 선택한 계정에 대해이 페이지가 자동으로 열립니다.)

1. 페이지 맨 위에 있는 **+** 를 클릭 하 고 **역할 할당 추가**를 선택 합니다.

1. 목록에서 "저장소 계정 참가자" 역할을 선택 합니다.

1. **액세스 할당** 필드에서 기본값 ("Azure AD 사용자, 그룹 또는 서비스 사용자")을 선택 된 채로 둡니다.  

1. **선택** 필드에서 "hpc"를 검색 합니다.  이 문자열은 "HPC 캐시 리소스 공급자" 라는 하나의 서비스 사용자와 일치 해야 합니다. 해당 보안 주체를 클릭 하 여 선택 합니다.

   > [!NOTE]
   > "Hpc" 검색이 작동 하지 않는 경우 "storagecache" 문자열을 대신 사용해 보세요. 미리 보기 (GA 이전)에 가입한 사용자는 서비스 사용자의 이전 이름을 사용 해야 할 수 있습니다.

1. 아래쪽에 있는 **저장** 단추를 클릭 합니다.

1. 이 프로세스를 반복 하 여 "Storage Blob Data 참여자" 역할을 할당 합니다.  

![역할 할당 GUI의 스크린샷](media/hpc-cache-add-role.png)

## <a name="add-a-new-nfs-storage-target"></a>새 NFS 저장소 대상 추가

NFS 저장소 대상에 Blob 저장소 대상 보다 많은 필드가 있습니다. 이러한 필드는 저장소 내보내기에 연결 하는 방법 및 데이터를 효율적으로 캐시 하는 방법을 지정 합니다. 또한 nfs 호스트에 사용 가능한 내보내기가 둘 이상 있는 경우 NFS 저장소 대상을 사용 하 여 여러 네임 스페이스 경로를 만들 수 있습니다.

![NFS 대상이 정의 된 저장소 대상 추가 페이지의 스크린샷](media/hpc-cache-add-nfs-target.png)

NFS 지원 저장소 대상에 대 한 다음 정보를 제공 합니다.

* **저장소 대상 이름** -Azure HPC 캐시에서이 저장소 대상을 식별 하는 이름을 설정 합니다.

* **대상 유형** - **NFS**를 선택 합니다.

* **호스트 이름** -NFS 저장소 시스템에 대 한 IP 주소 또는 정규화 된 도메인 이름을 입력 합니다. (이름을 확인할 수 있는 DNS 서버에 대 한 액세스 권한이 캐시에 있는 경우에만 도메인 이름을 사용 합니다.)

* **사용 모델** -아래에서 [사용 모델 선택](#choose-a-usage-model)에 설명 된 대로 워크플로를 기반으로 하는 데이터 캐싱 프로필 중 하나를 선택 합니다.

### <a name="nfs-namespace-paths"></a>NFS 네임 스페이스 경로

각 경로가 동일한 저장소 시스템의 다른 내보내기 또는 하위 디렉터리를 나타내는 한 NFS 저장소 대상에는 여러 개의 가상 경로가 있을 수 있습니다.

하나의 저장소 대상에서 모든 경로를 만듭니다.

언제 든 지 저장소 대상에서 [네임 스페이스 경로를 추가 하 고 편집할](hpc-cache-edit-storage.md) 수 있습니다.

각 네임 스페이스 경로에 대해 다음 값을 입력 합니다.

* **가상 네임 스페이스 경로** -이 저장소 대상에 대 한 클라이언트 쪽 파일 경로를 설정 합니다. 가상 네임 스페이스 기능에 대해 자세히 알아보려면 [집계 된 네임 스페이스 구성](hpc-cache-namespace.md) 을 참조 하세요.

<!--  The virtual path should start with a slash ``/``. -->

* **Nfs 내보내기 경로** -nfs 내보내기의 경로를 입력 합니다.

* **하위 디렉터리 경로** -내보내기의 특정 하위 디렉터리를 탑재 하려면 여기에 입력 합니다. 그렇지 않으면이 필드를 비워 둡니다.

완료 되 면 **확인** 을 클릭 하 여 저장소 대상을 추가 합니다.

### <a name="choose-a-usage-model"></a>사용 모델 선택
<!-- referenced from GUI - update aka.ms link if you change this heading -->

NFS 저장소 시스템을 가리키는 저장소 대상을 만들 때 해당 대상에 대 한 *사용 모델* 을 선택 해야 합니다. 이 모델은 데이터를 캐시 하는 방법을 결정 합니다.

세 개의 옵션이 있습니다.

* 자주 발생 하지 않는 **많은 쓰기 읽기** -정적 이거나 거의 변경 되지 않은 파일에 대 한 읽기 액세스를 가속화 하려면이 옵션을 사용 합니다.

  이 옵션은 클라이언트가 읽는 파일을 캐시 하지만 백 엔드 저장소에 즉시 쓰기를 전달 합니다. 캐시에 저장 된 파일은 NFS 저장소 볼륨의 파일과 비교 되지 않습니다.

  저장소 시스템에서 파일을 직접 캐시에 쓰지 않고 수정할 수 있는 위험이 있는 경우이 옵션을 사용 하지 마세요. 이 경우 캐시 된 버전의 파일이 백 엔드에서의 변경 내용으로 업데이트 되지 않으며 데이터 집합이 일치 하지 않을 수 있습니다.

* **쓰기 수 15% 이상** -이 옵션을 선택 하면 읽기 및 쓰기 성능이 향상 됩니다. 이 옵션을 사용 하는 경우 모든 클라이언트는 백 엔드 저장소를 직접 탑재 하는 대신 Azure HPC 캐시를 통해 파일에 액세스 해야 합니다. 캐시 된 파일에는 백 엔드에 저장 되지 않은 최근 변경 내용이 포함 됩니다.

  이 사용 모델에서 캐시의 파일은 백 엔드 저장소에 있는 파일에 대해 확인 되지 않습니다. 캐시 된 버전의 파일은 더 최신 버전으로 간주 됩니다. 캐시에 있는 수정 된 파일은 추가 변경 없이 1 시간 동안 캐시에 있는 백 엔드 저장소 시스템에만 기록 됩니다.

* **클라이언트에서 NFS 대상에 기록 하 고 캐시를 무시** 합니다. 워크플로에서 클라이언트를 먼저 캐시에 쓰지 않고 저장소 시스템에 직접 기록 하는 경우에는이 옵션을 선택 합니다. 클라이언트에서 요청 하는 파일은 캐시 되지만 클라이언트에서 해당 파일에 대 한 변경 내용은 즉시 백 엔드 저장소 시스템으로 다시 전달 됩니다.

  이 사용 모델을 사용 하면 캐시의 파일을 백 엔드 버전에 대해 자주 확인 하 여 업데이트를 수행 합니다. 이 확인을 통해 데이터 일관성을 유지 하면서 캐시 외부에서 파일을 변경할 수 있습니다.

이 표에는 사용 모델의 차이점이 요약 되어 있습니다.

| 사용 모델 | 캐싱 모드 | 백 엔드 확인 | 최대 다시 쓰기 지연 |
| ---- | ---- | ---- | ---- |
| 자주 발생 하지 않는 매우 많은 쓰기 읽기 | 읽기 | 사용 안 함 | 없음 |
| 쓰기 15% 초과 | 읽기/쓰기 | 사용 안 함 | 1시간 |
| 클라이언트에서 캐시 무시 | 읽기 | 30초 | 없음 |

## <a name="next-steps"></a>다음 단계

저장소 대상을 만든 후 다음 작업 중 하나를 고려 합니다.

* [Azure HPC Cache 마운트](hpc-cache-mount.md)
* [Azure Blob storage로 데이터 이동](hpc-cache-ingest.md)

설정을 업데이트 해야 하 [는 경우 저장소 대상을 편집할](hpc-cache-edit-storage.md)수 있습니다.
