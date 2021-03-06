---
title: 레지스트리 인증 옵션
description: Azure 컨테이너 레지스트리에 대한 인증 옵션(Azure Active Directory ID로 로그인, 서비스 주체 사용 및 선택적 관리자 자격 사용 등)입니다.
ms.topic: article
ms.date: 12/21/2018
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fbe77dee4104e3c654aad58db82765733b2c3e1d
ms.sourcegitcommit: 2a2af81e79a47510e7dea2efb9a8efb616da41f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/17/2020
ms.locfileid: "76264512"
---
# <a name="authenticate-with-a-private-docker-container-registry"></a>프라이빗 Docker 컨테이너 레지스트리로 인증

Azure Container Registry로 인증하는 방법은 여러 가지가 있으며 각 방법을 하나 이상의 레지스트리 사용 시나리오에 적용할 수 있습니다.

권장 되는 방법으로는 [개별 로그인](#individual-login-with-azure-ad)을 통해 레지스트리를 직접 인증 하거나, 응용 프로그램 및 컨테이너 orchestrator는 Azure Active Directory (Azure AD) [서비스 주체](#service-principal)를 사용 하 여 무인 또는 "헤드리스" 인증을 수행할 수 있습니다.

## <a name="individual-login-with-azure-ad"></a>Azure AD로 개별 로그인

개발용 워크스테이션에서 이미지 풀 및 푸시와 같이 직접 레지스트리를 사용하여 작업할 때 [Azure CLI](/cli/azure/install-azure-cli)에서 [az acr login](/cli/azure/acr?view=azure-cli-latest#az-acr-login) 명령을 사용하여 인증합니다.

```azurecli
az acr login --name <acrName>
```

`az acr login`을 사용하여 로그인하는 경우 CLI는 [az login](/cli/azure/reference-index#az-login)을 실행할 때 만든 토큰을 사용하여 원활하게 레지스트리로 세션을 인증합니다. 이러한 방식으로 로그인하고 나면 자격 증명이 캐시되고 세션의 후속 `docker` 명령에 사용자 이름 또는 암호가 필요하지 않습니다. 

레지스트리 액세스의 경우 `az acr login`에서 사용 하는 토큰은 **3 시간**동안 유효 하므로 `docker` 명령을 실행 하기 전에 항상 레지스트리에 로그인 하는 것이 좋습니다. 토큰이 만료될 경우 다시 `az acr login` 명령을 사용하여 토큰을 새로 고친 후 다시 인증합니다. 

Azure ID와 함께 `az acr login`을 사용하면 [역할 기반 액세스](../role-based-access-control/role-assignments-portal.md)를 제공합니다. 일부 시나리오의 경우 Azure AD에서 고유한 개별 id를 사용 하 여 레지스트리에 로그인 할 수 있습니다. 교차 서비스 시나리오 또는 개별 액세스를 관리하지 않으려는 작업 그룹의 요구 사항을 처리해야 하는 시나리오에서는 [Azure 리소스에 대한 관리 ID](container-registry-authentication-managed-identity.md)로 로그인할 수도 있습니다.

## <a name="service-principal"></a>서비스 주체

레지스트리에 [서비스 주체](../active-directory/develop/app-objects-and-service-principals.md)를 할당하면 애플리케이션 또는 서비스에서 헤드리스 인증에 이를 사용할 수 있습니다. 서비스 주체는 레지스트리에 [역할 기반 액세스](../role-based-access-control/role-assignments-portal.md)를 허용하며 사용자는 레지스트리에 여러 서비스 주체를 할당할 수 있습니다. 여러 서비스 주체를 사용하면 서로 다른 애플리케이션에 대한 다양한 액세스를 정의할 수 있습니다.

컨테이너 레지스트리에 사용할 수 있는 역할은 다음과 같습니다.

* **AcrPull**: 끌어오기

* **AcrPush**: 끌어오기 및 밀어넣기

* **소유자**: 풀, 푸시, 다른 사용자에게 역할 할당

전체 역할 목록은 [Azure Container Registry 역할 및 권한](container-registry-roles.md)을 참조하세요.

CLI 스크립트에서 Azure container registry를 사용 하 여 인증 하는 서비스 주체를 만들고 서비스 주체 사용에 대 한 지침은 서비스 사용자를 사용 하 [여 인증 Azure Container Registry](container-registry-auth-service-principal.md)을 참조 하세요.

## <a name="admin-account"></a>관리자 계정

각 컨테이너 레지스트리에는 관리 사용자 계정이 포함되어 있으며 기본적으로 사용하지 않도록 설정되어 있습니다. 관리 사용자를 사용하도록 설정하고 Azure Portal에서 또는 Azure CLI나 기타 Azure 도구를 사용하여 해당 자격 증명을 관리할 수 있습니다.

> [!IMPORTANT]
> 관리자 계정은 주로 테스트 용도로 단일 사용자가 레지스트리에 액세스하도록 설계되었습니다. 관리자 계정 자격 증명을 여러 사용자 간에 공유 하지 않는 것이 좋습니다. 관리자 계정으로 인증하는 모든 사용자는 레지스트리에 대한 푸시 및 풀 액세스 권한이 있는 단일 사용자로 나타납니다. 이 계정을 변경하거나 사용하지 않도록 설정하면 해당 자격 증명을 사용하는 모든 사용자의 레지스트리 액세스는 허용되지 않습니다. 헤드리스 시나리오의 경우 사용자 및 서비스 주체는 개별 ID를 사용하는 것이 좋습니다.
>

관리자 계정은 두 개의 암호가 제공되며, 둘 다 다시 생성할 수 있습니다. 두 개의 암호를 사용하면 다른 암호를 다시 생성하는 동안에 하나의 암호를 사용하여 레지스트리에 대한 연결을 유지할 수 있습니다. 관리자 계정을 사용할 수 있으면 레지스트리에 대한 기본 인증 메시지가 표시될 때 사용자 이름과 둘 중 한 가지 암호를 `docker login` 명령에 전달할 수 있습니다. 예:

```
docker login myregistry.azurecr.io 
```

로그인 자격 증명을 관리 하는 모범 사례는 [docker login](https://docs.docker.com/engine/reference/commandline/login/) 명령 참조를 참조 하세요.

기존 레지스트리에 대한 관리 사용자를 사용하도록 설정하려면 Azure CLI에서 [az acr update](/cli/azure/acr?view=azure-cli-latest#az-acr-update) 명령의 `--admin-enabled` 매개 변수를 사용하면 됩니다.

```azurecli
az acr update -n <acrName> --admin-enabled true
```

레지스트리로 이동하여 **설정**에서 **액세스 키**를 선택한 다음 **관리 사용자**에서 **사용**을 선택하면 Azure Portal에서 관리 사용자를 사용하도록 설정할 수 있습니다.

![Azure Portal에서 관리 사용자 UI 사용][auth-portal-01]

## <a name="next-steps"></a>다음 단계

* [Azure CLI를 사용하여 첫 번째 이미지 푸시](container-registry-get-started-azure-cli.md)

<!-- IMAGES -->
[auth-portal-01]: ./media/container-registry-authentication/auth-portal-01.png
