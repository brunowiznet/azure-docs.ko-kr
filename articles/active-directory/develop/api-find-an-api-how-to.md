---
title: 사용자 지정 개발 앱에 대 한 API 찾기 | Microsoft
description: 사용자 지정 개발 Azure AD 애플리케이션에서 특정 API에 액세스하는 데 필요한 권한을 구성하는 방법
services: active-directory
author: rwike77
manager: CelesteDG
ms.assetid: ''
ms.service: active-directory
ms.subservice: app-mgmt
ms.workload: identity
ms.topic: conceptual
ms.date: 06/28/2019
ms.author: ryanwi
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8c2b88ef00a8a40134462fdc285f1e4c3f12a0b0
ms.sourcegitcommit: 5ab4f7a81d04a58f235071240718dfae3f1b370b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/10/2019
ms.locfileid: "74963905"
---
# <a name="how-to-find-a-specific-api-needed-for-a-custom-developed-application"></a>사용자 지정 개발 애플리케이션에 대해 필요한 특정 API를 찾는 방법

API에 액세스하려면 액세스 범위 및 역할을 구성해야 합니다. 클라이언트 애플리케이션에 리소스 애플리케이션 웹 API를 표시하려는 경우 API에 대한 액세스 범위 및 역할을 구성해야 합니다. 클라이언트 애플리케이션에서 웹 API에 액세스하도록 하려면 앱 등록에서 API에 액세스하기 위한 권한을 구성해야 합니다.

## <a name="configuring-a-resource-application-to-expose-web-apis"></a>웹 API를 공개하는 리소스 애플리케이션 구성

웹 API를 표시할 때, 권한을 앱 등록에 추가하면 API가 **API 선택** 목록에 표시됩니다. 액세스 범위를 추가 하려면 [웹 api를 노출 하도록 응용 프로그램 구성](quickstart-configure-app-expose-web-apis.md)에 설명 된 단계를 따르세요.

## <a name="configuring-a-client-application-to-access-web-apis"></a>웹 API에 액세스하는 클라이언트 애플리케이션 구성

앱 등록에 권한을 추가할 때 표시된 웹 API에 **API 액세스 권한을 추가**할 수 있습니다. 웹 Api에 액세스 하려면 [웹 api에 액세스 하도록 클라이언트 응용 프로그램 구성](quickstart-configure-app-access-web-apis.md)에 설명 된 단계를 따르세요.

## <a name="next-steps"></a>다음 단계

- [Azure Active Directory 애플리케이션 매니페스트 이해](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-manifest)
