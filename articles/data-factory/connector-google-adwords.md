---
title: Google AdWords에서 데이터 복사
description: Azure Data Factory 파이프라인의 복사 작업을 사용하여 Google 애드워즈에서 지원되는 싱크 데이터 저장소로 데이터를 복사하는 방법에 대해 알아봅니다.
services: data-factory
ms.author: jingwang
author: linda33wj
manager: shwang
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.topic: conceptual
ms.custom: seo-lt-2019
ms.date: 10/25/2019
ms.openlocfilehash: b01dcad71747da6b7aa770e3993cb82892ae55fe
ms.sourcegitcommit: a5ebf5026d9967c4c4f92432698cb1f8651c03bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2019
ms.locfileid: "74929447"
---
# <a name="copy-data-from-google-adwords-using-azure-data-factory"></a>Azure Data Factory를 사용 하 여 Google AdWords에서 데이터 복사

이 문서에서는 Azure Data Factory의 복사 작업을 사용하여 Google 애드워즈에서 데이터를 복사하는 방법에 대해 설명합니다. 이 문서는 복사 작업에 대한 일반적인 개요를 제공하는 [복사 작업 개요](copy-activity-overview.md) 문서를 기반으로 합니다.

## <a name="supported-capabilities"></a>지원되는 기능

이 Google AdWords 커넥터는 다음과 같은 작업에 대해 지원 됩니다.

- [지원 되는 원본/싱크 매트릭스](copy-activity-overview.md) 를 사용 하 여 [복사 작업](copy-activity-overview.md)
- [조회 작업](control-flow-lookup-activity.md)


Google 애드워즈에서 지원되는 모든 싱크 데이터 저장소로 데이터를 복사할 수 있습니다. 복사 작업의 원본/싱크로 지원되는 데이터 저장소 목록은 [지원되는 데이터 저장소](copy-activity-overview.md#supported-data-stores-and-formats) 표를 참조하세요.

Azure Data Factory는 연결을 사용하는 기본 제공 드라이버를 제공합니다. 따라서 이 커넥터를 사용하여 드라이버를 수동으로 설치하지 않아도 됩니다.

## <a name="getting-started"></a>시작

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

다음 섹션에서는 Google 애드워즈 커넥터에 한정된 Data Factory 엔터티를 정의하는 데 사용되는 속성에 대해 자세히 설명합니다.

## <a name="linked-service-properties"></a>연결된 서비스 속성

다음은 Google 애드워즈 연결된 서비스에 대해 지원되는 속성입니다.

| 자산 | 설명 | 필수 |
|:--- |:--- |:--- |
| type | 형식 속성은 **GoogleAdWords**로 설정해야 합니다. | yes |
| clientCustomerID | 보고서 데이터를 가져올 AdWords 계정의 클라이언트 고객 ID입니다.  | yes |
| developerToken | AdWords API에 대한 액세스 권한을 부여하는 데 사용하는 관리자 계정과 연관된 개발자 토큰입니다.  이 필드는 SecureString으로 표시하여 ADF에 안전하게 저장할 수도 있고, Azure Key Vault에 암호를 저장하여 ADF 복사 활동에서 데이터 복사를 수행할 때 Key Vault에서 암호를 끌어오도록 할 수도 있습니다. 자세한 내용은 [Key Vault에 자격 증명 저장](store-credentials-in-key-vault.md)에서 확인하세요. | yes |
| authenticationType | 인증에 사용되는 OAuth 2.0 인증 메커니즘입니다. ServiceAuthentication은 자체 호스팅 IR에서만 사용할 수 있습니다. <br/>허용되는 값은 **ServiceAuthentication**, **UserAuthentication**입니다. | yes |
| refreshToken | UserAuthentication을 위한 애드워즈 액세스 권한을 부여하기 위해 Google에서 얻은 새로 고침 토큰입니다. 이 필드는 SecureString으로 표시하여 ADF에 안전하게 저장할 수도 있고, Azure Key Vault에 암호를 저장하여 ADF 복사 활동에서 데이터 복사를 수행할 때 Key Vault에서 암호를 끌어오도록 할 수도 있습니다. 자세한 내용은 [Key Vault에 자격 증명 저장](store-credentials-in-key-vault.md)에서 확인하세요. | 아닙니다. |
| clientId | 새로 고침 토큰을 획득 하는 데 사용 되는 Google 응용 프로그램의 클라이언트 ID입니다. 이 필드는 SecureString으로 표시하여 ADF에 안전하게 저장할 수도 있고, Azure Key Vault에 암호를 저장하여 ADF 복사 활동에서 데이터 복사를 수행할 때 Key Vault에서 암호를 끌어오도록 할 수도 있습니다. 자세한 내용은 [Key Vault에 자격 증명 저장](store-credentials-in-key-vault.md)에서 확인하세요. | 아닙니다. |
| clientSecret | 새로 고침 토큰을 얻는 데 사용되는 Google 애플리케이션의 클라이언트 암호입니다. 이 필드는 SecureString으로 표시하여 ADF에 안전하게 저장할 수도 있고, Azure Key Vault에 암호를 저장하여 ADF 복사 활동에서 데이터 복사를 수행할 때 Key Vault에서 암호를 끌어오도록 할 수도 있습니다. 자세한 내용은 [Key Vault에 자격 증명 저장](store-credentials-in-key-vault.md)에서 확인하세요. | 아닙니다. |
| 이메일 | ServiceAuthentication에 사용되는 서비스 계정 메일 ID이며 자체 호스팅 IR에서만 사용할 수 있습니다.  | 아닙니다. |
| keyFilePath | 서비스 계정 메일 주소를 인증하는 데 사용되는 .p12 키 파일의 전체 경로이며 자체 호스팅 IR에서만 사용할 수 있습니다.  | 아닙니다. |
| trustedCertPath | SSL을 통해 연결할 때 서버를 확인하기 위한 신뢰할 수 있는 CA 인증서를 포함하는 .pem 파일의 전체 경로입니다. 이 속성은 자체 호스팅 IR에서 SSL을 사용하는 경우에만 설정할 수 있습니다. 기본값은 IR과 함께 설치된 cacerts.pem 파일입니다.  | 아닙니다. |
| useSystemTrustStore | 시스템 신뢰 저장소 또는 지정된 PEM 파일의 CA 인증서를 사용할지 여부를 지정합니다. 기본값은 False입니다.  | 아닙니다. |

**예제:**

```json
{
    "name": "GoogleAdWordsLinkedService",
    "properties": {
        "type": "GoogleAdWords",
        "typeProperties": {
            "clientCustomerID" : "<clientCustomerID>",
            "developerToken": {
                "type": "SecureString",
                "value": "<developerToken>"
            },
            "authenticationType" : "ServiceAuthentication",
            "refreshToken": {
                "type": "SecureString",
                "value": "<refreshToken>"
            },
            "clientId": {
                "type": "SecureString",
                "value": "<clientId>"
            },
            "clientSecret": {
                "type": "SecureString",
                "value": "<clientSecret>"
            },
            "email" : "<email>",
            "keyFilePath" : "<keyFilePath>",
            "trustedCertPath" : "<trustedCertPath>",
            "useSystemTrustStore" : true,
        }
    }
}

```

## <a name="dataset-properties"></a>데이터 세트 속성

데이터 세트 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [데이터 세트](concepts-datasets-linked-services.md) 문서를 참조하세요. 이 섹션에서는 Google 애드워즈 데이터 세트에서 지원하는 속성의 목록을 제공합니다.

Google 애드워즈에서 데이터를 복사하려면 데이터 세트의 형식 속성을 **GoogleAdWordsObject**로 설정합니다. 다음과 같은 속성이 지원됩니다.

| 자산 | 설명 | 필수 |
|:--- |:--- |:--- |
| type | 데이터 집합의 type 속성은 **GoogleAdWordsObject** 로 설정 해야 합니다. | yes |
| tableName | 테이블 이름입니다. | 아니요(작업 원본에서 "query"가 지정된 경우) |

**예제**

```json
{
    "name": "GoogleAdWordsDataset",
    "properties": {
        "type": "GoogleAdWordsObject",
        "typeProperties": {},
        "schema": [],
        "linkedServiceName": {
            "referenceName": "<GoogleAdWords linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}

```

## <a name="copy-activity-properties"></a>복사 작업 속성

작업 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [파이프라인](concepts-pipelines-activities.md) 문서를 참조하세요. 이 섹션에서는 Google 애드워즈 원본에서 지원하는 속성의 목록을 제공합니다.

### <a name="google-adwords-as-source"></a>Google 애드워즈를 원본으로

Google 애드워즈에서 데이터를 복사하려면 복사 작업의 원본 형식을 **GoogleAdWordsSource**로 설정합니다. 복사 작업 **source** 섹션에서 다음 속성이 지원됩니다.

| 자산 | 설명 | 필수 |
|:--- |:--- |:--- |
| type | 복사 작업 원본의 형식 속성은 **GoogleAdWordsSource**로 설정해야 합니다. | yes |
| 쿼리 | 사용자 지정 SQL 쿼리를 사용하여 데이터를 읽습니다. 예: `"SELECT * FROM MyTable"`. | 아니요(데이터 세트의 "tableName"이 지정된 경우) |

**예제:**

```json
"activities":[
    {
        "name": "CopyFromGoogleAdWords",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<GoogleAdWords input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "GoogleAdWordsSource",
                "query": "SELECT * FROM MyTable"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="lookup-activity-properties"></a>조회 작업 속성

속성에 대 한 자세한 내용을 보려면 [조회 작업](control-flow-lookup-activity.md)을 확인 하세요.


## <a name="next-steps"></a>다음 단계
Azure Data Factory에서 복사 작업의 원본 및 싱크로 지원되는 데이터 저장소 목록은 [지원되는 데이터 저장소](copy-activity-overview.md#supported-data-stores-and-formats)를 참조하세요.
