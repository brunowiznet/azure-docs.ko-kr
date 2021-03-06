---
title: (사용되지 않음) Kubernetes용 Azure Container Service 소개
description: Kubernetes용 Azure Container Service를 통해 Azure에서 컨테이너 기반 애플리케이션을 간단히 배포 및 관리할 수 있습니다.
services: container-service
author: gabrtv
manager: jeconnoc
ms.service: container-service
ms.topic: overview
ms.date: 07/21/2017
ms.author: gamonroy
ms.custom: mvc
ms.openlocfilehash: e00ac57cc36b3331cfb847ecedc6c75132cdeb6b
ms.sourcegitcommit: 2469b30e00cbb25efd98e696b7dbf51253767a05
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/06/2018
ms.locfileid: "52999171"
---
# <a name="deprecated-introduction-to-azure-container-service-for-kubernetes"></a>(사용되지 않음) Kubernetes용 Azure Container Service 소개

> [!TIP]
> Azure Kubernetes Service를 사용하는 이 문서의 업데이트된 버전은 [AKS(Azure Kubernetes Service) 개요](../../aks/intro-kubernetes.md)를 참조하세요.

[!INCLUDE [ACS deprecation](../../../includes/container-service-kubernetes-deprecation.md)]

Kubernetes용 Azure Container Service를 사용하면 컨테이너화된 애플리케이션을 실행하는 미리 구성된 가상 머신의 클러스터를 보다 간편하게 만들고 구성하고 관리할 수 있습니다. 이를 통해 기존 기술을 사용하거나 크고 확장된 커뮤니티 전문 지식의 본문을 이용하여 Microsoft Azure의 컨테이너 기반 애플리케이션을 배포하고 관리할 수 있습니다.

Azure Container Service를 사용하면 Kubernetes 및 Docker 이미지 형식을 통해 애플리케이션 이식성을 유지하면서 Azure의 엔터프라이즈급 기능을 활용할 수 있습니다.

## <a name="using-azure-container-service-for-kubernetes"></a>Kubernetes용 Azure Container Service 사용
Azure 컨테이너 서비스를 사용하는 우리의 목표는 현재 우리 고객들 사이에서 인기 있는 오픈 소스 도구 및 기술을 사용하여 컨테이너 호스팅 환경을 제공하는 것입니다. 이를 위해 표준 Kubernetes API 엔드포인트를 공개합니다. 이러한 표준 엔드포인트를 사용하면 Kubernetes 클러스터와 통신할 수 있는 모든 소프트웨어를 활용할 수 있습니다. 예를 들어 [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [helm](https://helm.sh/) 또는 [draft](https://github.com/Azure/draft)를 선택할 수 있습니다.

## <a name="creating-a-kubernetes-cluster-using-azure-container-service"></a>Azure Container Service를 사용하여 Kubernetes 클러스터 만들기
Azure Container Service 사용을 시작하려면 [Azure CLI](container-service-kubernetes-walkthrough.md)를 사용하거나 포털(Marketplace에서 **Azure Container Service** 검색)을 통해 Azure Container Service 클러스터를 배포합니다. Azure Resource Manager 템플릿을 통해 더 많은 제어를 필요로 하는 고급 사용자인 경우 오픈 소스 [acs-engine](https://github.com/Azure/acs-engine) 프로젝트를 사용하여 사용자 지정 Kubernetes 클러스터를 빌드하여 `az` CLI를 통해 배포할 수 있습니다.

### <a name="using-kubernetes"></a>Kubernetes 사용
Kubernetes는 컨테이너화된 응용 프로그램의 배포, 크기 조정 및 관리를 자동화합니다. 여기에는 다음과 같이 풍부한 기능들이 포함되어 있습니다.
* 자동 저장소 적재
* 자동 복구
* 수평적 크기 조정
* 서비스 검색 및 부하 분산
* 자동화된 롤아웃 및 롤백
* 비밀 및 구성 관리
* 스토리지 오케스트레이션
* 일괄 처리 실행

Azure Container Service를 통해 배포된 Kubernetes의 아키텍처 다이어그램:

![Kubernetes를 사용하도록 구성된 Azure Container Service.](media/acs-intro/kubernetes.png)

## <a name="videos"></a>동영상

Azure Container Services의 Kubernetes 지원(Azure Friday, 2017년 1월):

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Kubernetes-Support-in-Azure-Container-Services/player]
>
>

Kubernetes에서 애플리케이션을 개발 및 배포하기 위한 도구(Azure OpenDev, 2017년 6월):

> [!VIDEO https://channel9.msdn.com/Events/AzureOpenDev/June2017/Tools-for-Developing-and-Deploying-Applications-on-Kubernetes/player]
>
>

## <a name="next-steps"></a>다음 단계

[Kubernetes 빠른 시작](container-service-kubernetes-walkthrough.md)을 살펴보고 오늘날 Azure Container Service에 대해 알아봅니다.
