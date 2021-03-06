---
title: Azure Multi-factor Auth 공급자-Azure Active Directory
description: Auth 공급자는 언제 Azure MFA에 사용하나요?
services: multi-factor-authentication
ms.service: active-directory
ms.subservice: authentication
ms.topic: conceptual
ms.date: 11/21/2019
ms.author: iainfou
author: iainfoulds
manager: daveba
ms.reviewer: michmcla
ms.collection: M365-identity-device-management
ms.openlocfilehash: 43a620d32fcfa7970dbdb5bee9740cc8f8b33e50
ms.sourcegitcommit: 276c1c79b814ecc9d6c1997d92a93d07aed06b84
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/16/2020
ms.locfileid: "76155132"
---
# <a name="when-to-use-an-azure-multi-factor-authentication-provider"></a>Azure Multi-Factor Authentication 공급자를 사용하는 시기

두 단계 인증은 기본적으로 Azure Active Directory 및 Office 365 사용자가 있는 전역 관리자를 위해 사용할 수 있습니다. 그러나 [고급 기능](howto-mfa-mfasettings.md)을 활용하려는 경우 Azure MFA(Multi-Factor Authentication)의 전체 버전을 구입해야 합니다.

Azure Multi-Factor Auth 공급자는 Azure Multi-Factor Authentication에서 **라이선스가 없는** 사용자에게 제공하는 기능을 활용하는 데 사용됩니다.

> [!NOTE]
> 2018년 9월 1일부터, 새 인증 공급자는 더 이상 생성되지 않을 수 있습니다. 기존 인증 공급자는 계속 사용 되 고 업데이트 될 수 있지만 마이그레이션은 더 이상 가능 하지 않습니다. Multi-Factor Authentication은 Azure AD Premium 라이선스의 기능으로 계속 사용할 수 있게 지원됩니다.

## <a name="caveats-related-to-the-azure-mfa-sdk"></a>Azure MFA SDK와 관련된 제한 사항

SDK는 더 이상 사용되지 않으며 2018년 11월 14일까지만 작동합니다. 해당 시점 이후에는 SDK에 대한 호출에 실패합니다.

## <a name="what-is-an-mfa-provider"></a>MFA 공급자란?

두 가지 유형의 Auth 공급자가 있으며 Azure 구독이 청구되는 방식에 따라 구분합니다. 인증 단위 옵션은 한 달에 테넌트에 대해 수행한 인증 수를 계산합니다. 이 옵션은 가끔씩만 인증하는 여러 사용자가 있는 경우에 가장 적합합니다. 사용자당 옵션은 테넌트에서 한 달 동안 2단계 인증을 수행하는 개인 수를 계산한 것입니다. 이 옵션은 라이선스를 갖고 있지만 라이선스 한도를 초과하여 더 많은 사용자까지 MFA를 확장해야 하는 사용자가 있는 경우 가장 적합합니다.

## <a name="manage-your-mfa-provider"></a>MFA 공급자 관리

MFA 공급자를 만든 후에는 사용 모델(활성화된 사용자별 또는 인증별)을 변경할 수 없습니다.

MFA로 설정된 모든 사용자를 처리할 만큼 충분한 라이선스를 구매한 경우 MFA 공급자를 모두 삭제할 수 있습니다.

하지만 MFA 공급자가 Azure AD 테넌트에 연결되어 있지 않거나 새 MFA 공급자를 다른 Azure AD 테넌트에 연결한 경우 사용자 설정 및 구성 옵션이 전송되지 않습니다. 또한 MFA 공급자를 통해 생성된 활성화 자격 증명을 사용하여 기존 Azure MFA 서버를 다시 활성화해야 합니다. MFA 서버를 MFA 공급자에 연결하기 위해 다시 활성화해도 전화 및 문자 메시지 인증에는 영향을 미치지 않지만 모바일 앱을 다시 활성화할 때까지 모바일 앱 알림이 모든 사용자에 대해 작동 중지됩니다.

### <a name="removing-an-authentication-provider"></a>인증 공급자 제거

> [!CAUTION]
> 인증 공급자를 삭제 하는 경우에는 확인이 필요 하지 않습니다. **삭제** 를 선택 하는 것은 영구적 프로세스입니다.

인증 공급자는 **Azure Portal** > **Azure Active Directory** > **보안** > **MFA** > **공급자**에서 찾을 수 있습니다. 나열 된 공급자를 클릭 하 여 해당 공급자와 관련 된 세부 정보 및 구성을 확인 합니다.

인증 공급자를 제거 하기 전에 공급자에 구성 된 사용자 지정 설정을 기록해 둡니다. 공급자의 일반 MFA 설정으로 마이그레이션해야 하는 설정을 결정 하 고 해당 설정의 마이그레이션을 완료 합니다. 

공급자에 연결 된 **AZURE Mfa 서버** 는 **Azure Portal** > Azure Active Directory에서 생성 된 자격 증명을 사용 하 여 다시 활성화 해야 합니다. > **Security** > **Server 설정** 다시 활성화 하기 전에 사용자 환경에서 Azure MFA 서버의 `\Program Files\Multi-Factor Authentication Server\Data\` 디렉터리에서 다음 파일을 삭제 해야 합니다.

- caCert
- cert
- groupCACert
- groupKey
- groupName
- licenseKey
- pkey

![Azure Portal에서 인증 공급자를 삭제 합니다.](./media/concept-mfa-authprovider/authentication-provider-removal.png)

모든 설정이 마이그레이션 되었음을 확인 한 후에는 **Azure Portal** >  > **Azure Active Directory** > **MFA** > **공급자** 를 찾아 줄임표 ( **...** )를 선택 하 고 **삭제**를 선택할 수 있습니다.

> [!WARNING]
> 인증 공급자를 삭제 하면 해당 공급자와 연결 된 보고 정보가 삭제 됩니다. 공급자를 삭제 하기 전에 작업 보고서를 저장 하는 것이 좋습니다.

> [!NOTE]
> 이전 버전의 Microsoft Authenticator 앱 및 Azure MFA 서버를 사용 하는 사용자는 앱을 다시 등록 해야 할 수 있습니다.

## <a name="next-steps"></a>다음 단계

[Multi-Factor Authentication 설정 구성](howto-mfa-mfasettings.md)
