---
title: '자습서: NetDocuments와 Azure Active Directory SSO(Single Sign-On) 통합 | Microsoft Docs'
description: Azure Active Directory와 NetDocuments 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: barbkess
ms.assetid: 1a47dc42-1a17-48a2-965e-eca4cfb2f197
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 09/03/2019
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: 71e5e13485c4a10664d98363e8e99bfd3b4f4bcf
ms.sourcegitcommit: f9e81b39693206b824e40d7657d0466246aadd6e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/08/2019
ms.locfileid: "72035712"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-netdocuments"></a>자습서: NetDocuments와 Azure Active Directory SSO(Single Sign-On) 통합

이 자습서에서는 Azure AD(Azure Active Directory)와 NetDocuments를 통합하는 방법을 알아봅니다. Azure AD와 NetDocuments를 통합하면 다음 작업을 수행할 수 있습니다.

* NetDocuments에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.
* 사용자가 해당 Azure AD 계정으로 NetDocuments에 자동으로 로그인되도록 설정할 수 있습니다.
* 단일 중앙 위치인 Azure Portal에서 계정을 관리합니다.

Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 애플리케이션 액세스 및 Single Sign-On이란 무엇인가요?](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)를 참조하세요.

## <a name="prerequisites"></a>필수 조건

시작하려면 다음 항목이 필요합니다.

* Azure AD 구독 구독이 없는 경우 [체험 계정](https://azure.microsoft.com/free/)을 얻을 수 있습니다.
* NetDocuments SSO(Single Sign-On) 사용 구독

## <a name="scenario-description"></a>시나리오 설명

이 자습서에서는 테스트 환경에서 Azure AD SSO를 구성하고 테스트합니다.

* NetDocuments에서 **SP** 시작 SSO를 지원합니다.

## <a name="adding-netdocuments-from-the-gallery"></a>갤러리에서 NetDocuments 추가

NetDocuments의 Azure AD 통합을 구성하려면 갤러리의 NetDocuments를 관리되는 SaaS 앱 목록에 추가해야 합니다.

1. [Azure Portal](https://portal.azure.com)에 회사 또는 학교 계정, 개인 Microsoft 계정으로 로그인합니다.
1. 왼쪽 탐색 창에서 **Azure Active Directory** 서비스를 선택합니다.
1. **엔터프라이즈 애플리케이션**으로 이동한 다음, **모든 애플리케이션**을 선택합니다.
1. 새 애플리케이션을 추가하려면 **새 애플리케이션**을 선택합니다.
1. **갤러리에서 추가** 섹션의 검색 상자에 **NetDocuments**를 입력합니다.
1. 결과 패널에서 **NetDocuments**를 선택한 다음, 앱을 추가합니다. 앱이 테넌트에 추가될 때까지 잠시 동안 기다려 주세요.

## <a name="configure-and-test-azure-ad-single-sign-on-for-netdocuments"></a>NetDocuments에 대한 Azure AD Single Sign-On 구성 및 테스트

**B.Simon**이라는 테스트 사용자를 사용하여 NetDocuments에서 Azure AD SSO를 구성하고 테스트합니다. SSO가 작동하려면 Azure AD 사용자와 NetDocuments의 관련 사용자 간에 연결 관계를 설정해야 합니다.

NetDocuments에서 Azure AD SSO를 구성하고 테스트하려면 다음 구성 요소를 완료합니다.

1. **[Azure AD SSO 구성](#configure-azure-ad-sso)** - 사용자가 이 기능을 사용할 수 있도록 합니다.
    1. **[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - B.Simon을 사용하여 Azure AD Single Sign-On을 테스트합니다.
    1. **[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - B. Simon이 Azure AD Single Sign-On을 사용할 수 있도록 합니다.
1. **[NetDocuments SSO 구성](#configure-netdocuments-sso)** - 애플리케이션 쪽에서 Single Sign-On 설정을 구성합니다.
    1. **[NetDocuments 테스트 사용자 만들기](#create-netdocuments-test-user)** - B.Simon의 Azure AD 표현과 연결된 해당 사용자를 NetDocuments에 만듭니다.
1. **[SSO 테스트](#test-sso)** - 구성이 작동하는지 여부를 확인합니다.

## <a name="configure-azure-ad-sso"></a>Azure AD SSO 구성

Azure Portal에서 Azure AD SSO를 사용하도록 설정하려면 다음 단계를 수행합니다.

1. [Azure Portal](https://portal.azure.com/)의 **NetDocuments** 애플리케이션 통합 페이지에서 **관리** 섹션을 찾은 다음, **Single Sign-On**을 선택합니다.
1. **Single Sign-On 방법 선택** 페이지에서 **SAML**을 선택합니다.
1. **SAML로 Single Sign-On 설정** 페이지에서 **기본 SAML 구성**에 대한 편집(연필 모양) 아이콘을 클릭하여 설정을 편집합니다.

   ![기본 SAML 구성 편집](common/edit-urls.png)

1. **기본 SAML 구성** 섹션에서 다음 필드에 대한 값을 입력합니다.

    a. **로그온 URL** 텍스트 상자에서 `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<Repository ID>` 패턴을 사용하는 URL을 입력합니다.

    b. **회신 URL** 텍스트 상자에서 `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<Repository ID>` 패턴을 사용하여 URL을 입력합니다.
    
    다. **식별자(엔터티 ID)** 텍스트 상자에서 `http://netdocuments.com/VAULT` 패턴을 사용하는 URL을 입력합니다.

    > [!NOTE]
    > 이러한 값은 실제 값이 아닙니다. 실제 로그온 URL 및 회신 URL로 해당 값을 업데이트합니다. 리포지토리 ID는 **CA-** 로 시작하고 뒤에 NetDocuments 리포지토리와 연결된 8자 코드가 나오는 값입니다. 자세한 내용은 [NetDocuments 페더레이션 ID 지원 문서](https://support.netdocuments.com/hc/en-us/articles/205220410-Federated-Identity-Login)에서 확인할 수 있습니다. 또는 위 정보로 구성하는 데 문제가 있는 경우 [NetDocuments 클라이언트 지원 팀](https://support.netdocuments.com/hc/)에 문의하여 이러한 값을 받을 수 있습니다. Azure Portal의 **기본 SAML 구성** 섹션에 표시된 패턴을 참조할 수도 있습니다.

1. NetDocuments 애플리케이션은 SAML 토큰 특성 구성에 사용자 지정 특성 매핑을 추가해야 하는 특정 형식의 SAML 어설션이 필요합니다. 다음 스크린샷에서는 **nameidentifier**가 **user.userprincipalname**과 매핑되는 기본 특성 목록을 보여줍니다. NetDocuments 애플리케이션에서는 **nameidentifier**가 **employeeid**와 매핑되거나 **nameidentifier**로 조직에 적용 가능한 다른 모든 클레임과 매핑되어야 하므로 **편집** 아이콘을 클릭하고 특성 매핑을 변경하여 특성 매핑을 편집해야 합니다.

    ![이미지](common/edit-attribute.png)

1. **SAML로 Single Sign-On 설정** 페이지의 **SAML 서명 인증서** 섹션에서 **페더레이션 메타데이터 XML**을 찾고, **다운로드**를 선택하여 인증서를 컴퓨터에 다운로드 및 저장합니다.

    ![인증서 다운로드 링크](common/metadataxml.png)

1. **NetDocuments 설정** 섹션에서 요구 사항에 따라 적절한 URL을 복사합니다.

    ![구성 URL 복사](common/copy-configuration-urls.png)

### <a name="create-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기

이 섹션에서는 Azure Portal에서 B.Simon이라는 테스트 사용자를 만듭니다.

1. Azure Portal의 왼쪽 창에서 **Azure Active Directory**, **사용자**, **모든 사용자**를 차례로 선택합니다.
1. 화면 위쪽에서 **새 사용자**를 선택합니다.
1. **사용자** 속성에서 다음 단계를 수행합니다.
   1. **이름** 필드에 `B.Simon`을 입력합니다.  
   1. **사용자 이름** 필드에서 username@companydomain.extension을 입력합니다. 예: `B.Simon@contoso.com`
   1. **암호 표시** 확인란을 선택한 다음, **암호** 상자에 표시된 값을 적어둡니다.
   1. **만들기**를 클릭합니다.

### <a name="assign-the-azure-ad-test-user"></a>Azure AD 테스트 사용자 할당

이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 B.Simon에게 NetDocuments에 대한 액세스 권한을 부여합니다.

1. Azure Portal에서 **엔터프라이즈 애플리케이션**을 선택한 다음, **모든 애플리케이션**을 선택합니다.
1. 애플리케이션 목록에서 **NetDocuments**를 선택합니다.
1. 앱의 개요 페이지에서 **관리** 섹션을 찾고 **사용자 및 그룹**을 선택합니다.

   !["사용자 및 그룹" 링크](common/users-groups-blade.png)

1. **사용자 추가**를 선택한 다음, **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![사용자 추가 링크](common/add-assign-user.png)

1. **사용자 및 그룹** 대화 상자의 사용자 목록에서 **B.Simon**을 선택한 다음, 화면 아래쪽에서 **선택** 단추를 클릭합니다.
1. SAML 어설션에 역할 값이 필요한 경우 **역할 선택** 대화 상자의 목록에서 사용자에 대한 적절한 역할을 선택한 다음, 화면의 아래쪽에 있는 **선택** 단추를 클릭합니다.
1. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.

## <a name="configure-netdocuments-sso"></a>NetDocuments SSO 구성

1. 다른 웹 브라우저 창에서 NetDocuments 회사 사이트에 관리자로 로그인합니다.

2. **관리자**로 이동합니다.

3. **사용자와 그룹 추가 및 제거**를 클릭합니다.
   
    ![리포지토리](./media/netdocuments-tutorial/ic795047.png "리포지토리")

4. **고급 인증 옵션 구성**을 클릭합니다.
    
    ![고급 인증 옵션 구성](./media/netdocuments-tutorial/ic795048.png "고급 인증 옵션 구성")

5. **페더레이션 ID** 대화 상자에서 다음 단계를 수행합니다.
   
    ![페더레이션 ID](./media/netdocuments-tutorial/ic795049.png "페더레이션 ID")
   
    a. **페더레이션 ID 서버 유형**으로 **Active Directory Federation Services**를 선택합니다.
   
    b. **파일 선택**을 클릭하여 Azure Portal에서 다운로드한 메타데이터 파일을 업로드합니다.
   
    다. **확인**을 클릭합니다.

### <a name="create-netdocuments-test-user"></a>NetDocuments 테스트 사용자 만들기

Azure AD 사용자가 NetDocuments에 로그인할 수 있게 하려면 NetDocuments에 프로비저닝해야 합니다.  
NetDocuments의 경우 프로비전은 수동 작업입니다.

**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**

1. **NetDocuments** 회사 사이트에 관리자 권한으로 로그온합니다.

2. 위쪽의 메뉴에서 **관리자**를 클릭합니다.
   
    ![관리자](./media/netdocuments-tutorial/ic795051.png "관리자")

3. **사용자와 그룹 추가 및 제거**를 클릭합니다.
   
    ![리포지토리](./media/netdocuments-tutorial/ic795047.png "리포지토리")

4. **메일 주소** 텍스트 상자에 프로비전하려는 유효한 Azure Active Directory 계정의 이메일 주소를 입력한 다음 **사용자 추가**를 클릭합니다.
   
    ![전자 메일 주소](./media/netdocuments-tutorial/ic795053.png "전자 메일 주소")
   
    >[!NOTE]
    >Azure Active Directory 계정 보유자는 활성화되기 전에 계정을 확인하기 위한 링크를 포함한 이메일을 받습니다. 다른 NetDocuments 사용자 계정 생성 도구 또는 NetDocuments가 제공한 API를 사용하여 Azure Active Directory 사용자 계정을 프로비전할 수 있습니다.

## <a name="test-sso"></a>SSO 테스트 

이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.

액세스 패널에서 NetDocuments 타일을 클릭하면, SSO를 설정한 NetDocuments에 자동으로 로그인되어야 합니다. 액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)를 참조하세요.

## <a name="additional-resources"></a>추가 리소스

- [Azure Active Directory와 SaaS 앱을 통합하는 방법에 대한 자습서 목록](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list)

- [Azure Active Directory를 사용한 애플리케이션 액세스 및 Single Sign-On이란?](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)

- [Azure Active Directory의 조건부 액세스란?](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)

- [Azure AD로 NetDocuments 체험하기](https://aad.portal.azure.com/)

