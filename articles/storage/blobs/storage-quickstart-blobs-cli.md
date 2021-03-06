---
title: 빠른 시작 - Azure CLI를 사용하여 Blob 만들기
titleSuffix: Azure Storage
description: 이 빠른 시작에서는 Azure CLI를 사용하여 Azure Storage에 BLOB을 업로드하고, BLOB을 다운로드하고, 컨테이너의 BLOB을 나열하는 방법을 알아봅니다.
services: storage
author: tamram
ms.custom: mvc
ms.service: storage
ms.topic: quickstart
ms.date: 12/04/2019
ms.author: tamram
ms.openlocfilehash: c913cb978796abeed5766ffa030aaeb6142320ec
ms.sourcegitcommit: 8bd85510aee664d40614655d0ff714f61e6cd328
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/06/2019
ms.locfileid: "74892926"
---
# <a name="quickstart-create-download-and-list-blobs-with-azure-cli"></a>빠른 시작: Azure CLI를 사용하여 Blob 생성, 다운로드 및 나열

Azure CLI는 Azure 리소스를 관리하는 Azure의 명령줄 환경입니다. 브라우저에서 Azure Cloud Shell과 함께 사용할 수 있습니다. macOS, Linux 또는 Windows에 설치하여 명령줄에서 실행할 수도 있습니다. 빠른 시작에서는 Azure CLI를 사용하여 Azure Blob Storage에서 데이터를 업로드 및 다운로드하는 방법을 알아봅니다.

[!INCLUDE [storage-multi-protocol-access-preview](../../../includes/storage-multi-protocol-access-preview.md)]

## <a name="prerequisites"></a>필수 조건

[!INCLUDE [storage-quickstart-prereq-include](../../../includes/storage-quickstart-prereq-include.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 빠른 시작에서 Azure CLI 버전 2.0.4 이상을 실행해야 합니다. 버전을 확인하려면 `az --version`을 실행합니다. 설치 또는 업그레이드가 필요한 경우, [Azure CLI 설치](/cli/azure/install-azure-cli)를 참조하세요.

[!INCLUDE [storage-quickstart-tutorial-intro-include-cli](../../../includes/storage-quickstart-tutorial-intro-include-cli.md)]

## <a name="create-a-container"></a>컨테이너 만들기

Blob은 항상 컨테이너에 업로드됩니다. 폴더에서 컴퓨터의 파일을 구성하는 방식과 비슷하게 Blob 그룹을 구성할 수 있습니다.

Blob 저장을 위한 컨테이너는 [az storage container create](/cli/azure/storage/container) 명령을 사용하여 만듭니다.

```azurecli-interactive
az storage container create --name sample-container
```

## <a name="upload-a-blob"></a>Blob 업로드

Blob Storage는 블록 Blob, 추가 Blob 및 페이지 Blob을 지원합니다. 이 빠른 시작의 예제에서는 블록 Blob을 사용하는 방법을 보여 줍니다.

먼저 Blob에 업로드할 파일을 만듭니다. Azure Cloud Shell을 사용하는 경우 다음 명령을 사용하여 파일을 만듭니다.

```bash
vi helloworld
```

파일이 열리면 **삽입**을 누릅니다. *Hello World*를 입력한 다음, **Esc** 키를 누릅니다. 그런 다음, *:x*를 입력하고 **Enter** 키를 누릅니다.

이 예제에서는 [az storage blob upload](/cli/azure/storage/blob) 명령을 사용하여 마지막 단계에서 만든 컨테이너에 Blob을 업로드합니다. 루트 디렉터리에서 파일을 만들었기 때문에 파일 경로를 지정할 필요는 없습니다.

```azurecli-interactive
az storage blob upload \
    --container-name sample-container \
    --name helloworld \
    --file helloworld
```

이 작업은 Blob이 없는 경우 만들고, Blob이 있는 경우 덮어씁니다. 원하는 만큼 파일을 업로드한 후 계속합니다.

동시에 여러 파일을 업로드하려면 [az storage blob upload-batch](/cli/azure/storage/blob) 명령을 사용할 수 있습니다.

## <a name="list-the-blobs-in-a-container"></a>컨테이너의 Blob 나열

[az storage blob list](/cli/azure/storage/blob) 명령으로 컨테이너에 있는 Blob을 나열합니다.

```azurecli-interactive
az storage blob list \
    --container-name sample-container \
    --output table
```

## <a name="download-a-blob"></a>Blob 다운로드

[az storage blob download](/cli/azure/storage/blob) 명령을 사용하여 이전에 업로드한 Blob을 다운로드합니다.

```azurecli-interactive
az storage blob download \
    --container-name sample-container \
    --name helloworld \
    --file ~/destination/path/for/file
```

## <a name="data-transfer-with-azcopy"></a>AzCopy를 사용한 데이터 전송

[AzCopy](../common/storage-use-azcopy-linux.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) 유틸리티는 Azure Storage를 위한 또 다른 스크립팅 가능한 고성능 데이터 전송 옵션입니다. AzCopy를 사용하여 Blob, File 및 Table Storage 간에 데이터를 전송할 수 있습니다.

다음 예제에서는 AzCopy를 사용하여 *myfile.txt*라는 파일을 *sample-container* 컨테이너에 업로드합니다. 꺾쇠 괄호로 묶인 자리 표시자 값을 사용자 고유의 값으로 바꿔야 합니다.

```bash
azcopy \
    --source /mnt/myfiles \
    --destination https://<account-name>.blob.core.windows.net/sample-container \
    --dest-key <account-key> \
    --include "myfile.txt"
```

## <a name="clean-up-resources"></a>리소스 정리

이 빠른 시작에서 만든 스토리지 계정을 비롯하여 리소스 그룹의 어떠한 리소스도 더 이상 필요하지 않은 경우 [az group delete](/cli/azure/group) 명령으로 리소스 그룹을 삭제합니다. 꺾쇠 괄호로 묶인 자리 표시자 값을 사용자 고유의 값으로 바꿔야 합니다.

```azurecli-interactive
az group delete --name <resource-group-name>
```

## <a name="next-steps"></a>다음 단계

이 빠른 시작에서는 로컬 파일 시스템과 Azure Blob 스토리지의 컨테이너 간에 파일을 전송하는 방법을 알아보았습니다. Azure Storage에서 Blob을 사용하는 방법을 자세히 알아보려면 계속해서 Azure Blob Storage 사용에 대한 자습서를 진행하세요.

> [!div class="nextstepaction"]
> [방법: Azure CLI를 사용한 Blob Storage 작업](storage-how-to-use-blobs-cli.md)
