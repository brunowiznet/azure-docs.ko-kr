---
title: Microsoft Authenticator 앱을 사용 하 여 계정 백업 및 복구-Azure AD
description: Microsoft Authenticator 앱을 사용 하 여 백업 된 계정 자격 증명을 백업 및 복구 하는 방법에 대해 알아봅니다.
services: active-directory
author: eross-msft
manager: daveba
ms.subservice: user-help
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 08/22/2019
ms.author: lizross
ms.reviewer: olhaun
ms.collection: M365-identity-device-management
ms.openlocfilehash: 827213c8d243e9d66c58195e1d9400bed9c3e337
ms.sourcegitcommit: 653e9f61b24940561061bd65b2486e232e41ead4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2019
ms.locfileid: "74266996"
---
# <a name="backup-and-recover-account-credentials-using-the-microsoft-authenticator-app"></a>Microsoft Authenticator 앱을 사용 하 여 계정 자격 증명 백업 및 복구

**적용 대상:**

- iOS 장치, 버전 5.7.0 이상이 필요 이상 실행

- Android 장치, 버전 6.6.0 이상 실행

Microsoft Authenticator 앱은 계정 자격 증명과 계정 순서 같은 관련 앱 설정을 클라우드에 백업합니다. 백업 후에는 앱을 사용하여 정보를 새 디바이스에 복구하면 계정이 잠기거나 계정을 다시 만들어야 하는 문제를 피할 수 있습니다.

각 백업 저장소 위치에는 하나의 개인 Microsoft 계정 있어야 하 고, iOS에는 iCloud 계정도 있어야 합니다. 단일 위치에 여러 계정을 저장할 수 있습니다. 예를 들어 개인 계정, 회사 또는 학교 계정, Facebook, Google 등의 개인 계정, Microsoft 계정 개인 계정 등이 있습니다.

> [!IMPORTANT]
> 사용자의 id를 증명 하는 데 필요한 사용자 이름 및 계정 확인 코드를 포함 하는 개인 및 타사 계정 자격 증명만 저장 됩니다. 이메일 또는 파일을 포함하여 계정에 연결된 기타 정보는 저장되지 않습니다. 또한 계정을 어떤 방식으로든, 어떤 제품 또는 서비스에도 연결하거나 공유하지 않습니다. 마지막으로, IT 관리자는 이러한 계정에 대한 정보를 얻을 수 없습니다.

## <a name="back-up-your-account-credentials"></a>계정 자격 증명 백업

자격 증명을 백업 하려면 다음을 수행 해야 합니다.

- 복구 계정 역할을 할 개인 [Microsoft 계정](https://account.microsoft.com/account).

- **IOS의** 경우 실제 저장소 위치에 대 한 [iCloud 계정이](https://www.icloud.com/) 있어야 합니다.

### <a name="to-turn-on-cloud-backup-for-ios-devices"></a>IOS 장치에 대 한 클라우드 백업을 켜려면

- iOS 디바이스에서 **설정**을 선택하고, **백업**을 선택한 다음, **iCloud 백업**을 켭니다.

    계정 자격 증명이 iCloud 계정에 백업됩니다.

    ![iCloud 백업 위치 설정을 보여주는 iOS 설정 화면](./media/user-help-auth-app-backup-recovery/backup-and-recovery-turn-on.png)

### <a name="to-turn-on-cloud-backup-for-android-devices"></a>Android 장치에 대 한 클라우드 백업을 켜려면

- Android 장치에서 **설정**을 선택 하 고 **백업**을 선택한 후 **클라우드 백업**을 켭니다.

    계정 자격 증명은 클라우드 계정에 백업 됩니다.

    ![Android 설정 화면, 백업 설정의 위치 표시](./media/user-help-auth-app-backup-recovery/backup-and-recovery-turn-on-android.png)

## <a name="recover-your-account-credentials-on-your-new-device"></a>계정 자격 증명을 새 디바이스에 복구

클라우드 계정에서 계정 자격 증명을 복구할 수는 있지만 먼저 복구 하려는 계정이 Microsoft Authenticator 앱에 존재 하지 않는지 확인 해야 합니다. 예를 들어 개인 Microsoft 계정를 복구 하는 경우 인증 앱에서 아직 개인 Microsoft 계정 설정 하지 않았는지 확인 해야 합니다. 이 확인은 중요 합니다. 따라서 실수로 기존 계정을 덮어쓰거나 지우지 않도록 할 수 있습니다.

### <a name="to-recover-your-information"></a>정보를 복구하려면

1. 모바일 장치에서 Microsoft Authenticator 앱을 열고 화면 아래쪽에서 **복구 시작** 을 선택 합니다.

    ![복구 시작을 클릭하는 위치를 보여주는 Microsoft Authenticator 앱](./media/user-help-auth-app-backup-recovery/backup-and-recovery-begin-recovery.png)

2. 백업 프로세스에서 사용한 것과 동일한 개인 Microsoft 계정을 사용하여 복구 계정에 로그인합니다.

    계정 자격 증명이 새 디바이스에 복구됩니다.

복구를 마친 후 Microsoft Authenticator 앱의 개인 Microsoft 계정 확인 코드가 기존 장치와 새 장치 간에 다를 수 있습니다. 디바이스마다 고유의 자격 증명이 있기 때문에 코드가 다르지만, 연결된 전화를 사용하여 로그인할 때 둘 다 유효하며 정상적으로 작동합니다.

## <a name="recover-additional-accounts-requiring-more-verification"></a>추가 계정을 복구하려면 추가 확인이 필요

개인 또는 회사 또는 학교 계정에 푸시 알림을 사용 하는 경우 정보를 복구 하려면 먼저 추가 확인을 제공 해야 한다는 경고 메시지가 표시 됩니다. 푸시 알림은 사용자의 특정 디바이스에 연결된 자격 증명을 사용해야 하고 어떤 경우에도 네트워크를 통해 전송되지 않으므로 디바이스에 자격 증명을 만들려면 사용자의 신분을 증명해야 합니다.

개인 Microsoft 계정의 경우 대체 이메일 또는 전화 번호와 함께 암호를 입력하여 신분을 증명할 수 있습니다. 회사 또는 학교 계정의 경우 계정 공급자가 제공한 QR 코드를 검사해야 합니다.

### <a name="to-provide-additional-verification-for-personal-accounts"></a>개인 계정에 대한 추가 확인을 제공하려면

1. Microsoft Authenticator 앱의 **계정** 화면에서 복구하려는 계정 옆에 있는 드롭다운 화살표를 선택합니다.

    ![연결된 드롭다운 화살표가 있는 사용 가능한 계정을 보여주는 Microsoft Authenticator 앱](./media/user-help-auth-app-backup-recovery/backup-and-recovery-arrow.png)

2. **복구하려면 로그인**을 선택하고, 암호를 입력한 다음, 추가 확인으로 이메일 주소 또는 전화 번호를 확인합니다.

    ![로그인 정보를 입력할 수 있는 Microsoft Authenticator 앱](./media/user-help-auth-app-backup-recovery/backup-and-recovery-sign-in.png)

### <a name="to-provide-additional-verification-for-work-or-school-accounts"></a>회사 또는 학교 계정에 대한 추가 확인을 제공하려면

1. Microsoft Authenticator 앱의 **계정** 화면에서 복구하려는 계정 옆에 있는 드롭다운 화살표를 선택합니다.

    ![연결된 드롭다운 화살표가 있는 사용 가능한 계정을 보여주는 Microsoft Authenticator 앱](./media/user-help-auth-app-backup-recovery/backup-and-recovery-additional-accts.png)

2. **복구하려면 QR 코드 검사**을 선택한 다음, QR 코드를 검사합니다.

    ![QR 코드를 검사할 수 있는 Microsoft Authenticator 앱](./media/user-help-auth-app-backup-recovery/backup-and-recovery-scan-qr-code.png)

    >[!NOTE]
    >QR 코드 및이 코드를 가져오는 방법에 대 한 자세한 내용은 관리자가 보안 정보를 사용 하도록 설정 되었는지 여부에 따라 [Microsoft Authenticator 앱 시작](https://docs.microsoft.com/azure/active-directory/user-help/user-help-auth-app-download-install) 또는 [인증자 앱을 사용 하도록 보안 정보 설정](https://docs.microsoft.com/azure/active-directory/user-help/security-info-setup-auth-app)을 참조 하세요.
    >
    >Microsoft Authenticator 앱을 처음으로 설정하는 경우 앱에서 카메라에 액세스할 수 있도록 허용할지(iOS) 아니면 앱에서 사진을 촬영하고 비디오를 녹화할 수 있도록 허용할지(Android) 묻는 메시지를 받을 수 있습니다. 인증자 앱이 카메라에 액세스하여 다음 단계에서 QR 코드의 사진을 찍을 수 있도록 **허용**을 선택해야 합니다. 카메라를 허용하지 않는 경우에도 여전히 인증자 앱을 설정할 수 있지만 코드 정보를 수동으로 추가해야 합니다. 코드를 수동으로 추가하는 방법에 대한 자세한 내용은 [수동으로 앱에 계정 추가](user-help-auth-app-add-account-manual.md)를 참조하세요.

## <a name="troubleshoot-backup-and-recovery-problems"></a>백업 및 복구 문제 해결

백업을 사용할 수 없는 몇 가지 이유가 있습니다.

- **운영 체제 변경.** 백업은 iOS 용 iCloud와 Android 용 Microsoft 클라우드 저장소 공급자에 저장 됩니다. 즉, Android 장치와 iOS 장치 간을 전환 하는 경우 백업을 사용할 수 없습니다. 스위치를 설정 하는 경우 Microsoft Authenticator 앱 내에서 수동으로 계정을 다시 만들어야 합니다.

- **네트워크 문제** 네트워크 관련 문제가 발생 하는 경우 네트워크에 연결 되어 있고 계정에 올바르게 로그인 했는지 확인 합니다.

- **계정 문제.** 계정 관련 문제가 발생 하는 경우 계정에 올바르게 로그인 했는지 확인 합니다. IOS의 경우 iPhone과 동일한 사과 Eid 계정을 사용 하 여 iCloud에 로그인 해야 합니다.

- **실수로 삭제.** 이전 디바이스에서 또는 클라우드 스토리지 계정을 관리하는 동안 백업 계정을 삭제했을 가능성이 있습니다. 이 경우 앱 내에서 수동으로 계정을 다시 만들어야 합니다.

- **기존 Microsoft Authenticator 계정.** Microsoft Authenticator 앱에서 이미 계정을 설정한 경우 앱이 백업된 계정을 복구할 수 없습니다. 계정을 복구하지 못하게 하는 이유는 계정 세부 정보를 오래된 정보로 덮어쓰지 않게 방지하기 위함입니다. 이 경우 Authenticator 앱의 기존 계정에서 기존 계정 정보를 모두 제거해야 백업을 복구할 수 있습니다.

- **백업이 만료 되었습니다.** 백업 정보가 만료 된 경우 Microsoft 복구 계정에 다시 로그인 하 여 정보를 새로 고치 라는 메시지가 표시 될 수 있습니다. 복구 계정은 처음에 백업을 저장 하는 데 사용한 개인 Microsoft 계정입니다. 로그인이 필요한 경우 메뉴 또는 작업 모음에 빨간색 점이 표시 됩니다. 빨간색 점을 선택한 후에는 다시 로그인 하 여 정보를 업데이트 하 라는 메시지가 표시 됩니다.

## <a name="next-steps"></a>다음 단계

계정 자격 증명을 백업하고 새 디바이스에 복구했으니, 계속해서 Microsoft Authenticator 앱을 사용하여 ID를 확인할 수 있습니다. 자세한 내용은 [Microsoft Authenticator 앱을 사용 하 여 계정에 로그인](user-help-sign-in.md)을 참조 하세요.

## <a name="related-articles"></a>관련된 문서

- [Microsoft Authenticator 앱 이란?](user-help-auth-app-overview.md)

- [Microsoft Authenticator 앱 FAQ](user-help-auth-app-faq.md)

- [Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/)
