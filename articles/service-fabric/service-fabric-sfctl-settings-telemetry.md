---
title: Azure Service Fabric CLI-sfctl 설정 원격 분석
description: Sfctl, Azure Service Fabric 명령줄 인터페이스에 대해 알아봅니다. Sfctl 원격 분석을 구성 하기 위한 명령 목록을 포함 합니다.
author: jeffj6123
ms.topic: reference
ms.date: 9/17/2019
ms.author: jejarry
ms.openlocfilehash: cdb4a44c8f19b31c164e2ba3ea5e16b7a09e743e
ms.sourcegitcommit: f788bc6bc524516f186386376ca6651ce80f334d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/03/2020
ms.locfileid: "75645279"
---
# <a name="sfctl-settings-telemetry"></a>sfctl settings telemetry
이 sfctl 인스턴스에 로컬인 원격 분석 설정을 구성합니다.

sfctl telemetry는 제공된 매개 변수 없이 명령 이름이나 해당 값, sfctl 버전, OS 유형, Python 버전, 명령의 성공 또는 실패, 반환된 오류 메시지를 수집합니다.

## <a name="commands"></a>명령

|명령|Description|
| --- | --- |
| set-telemetry | 원격 분석을 켜거나 끕니다. |

## <a name="sfctl-settings-telemetry-set-telemetry"></a>sfctl settings telemetry set-telemetry
원격 분석을 켜거나 끕니다.

### <a name="arguments"></a>인수

|인수|Description|
| --- | --- |
| --off | 원격 분석을 끕니다. |
| --on | 원격 분석을 켭니다. 이것은 기본값입니다. |

### <a name="global-arguments"></a>전역 인수

|인수|Description|
| --- | --- |
| --debug | 로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다. |
| --help -h | 이 도움말 메시지를 표시하고 종료합니다. |
| --output -o | 출력 형식입니다.  허용되는 값\: json, jsonc, table, tsv.  기본값\: json. |
| --query | JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 http\://jmespath.org/를 참조하세요. |
| --verbose | 로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다. |

### <a name="examples"></a>예시

원격 분석을 끕니다.

```
sfctl settings telemetry set_telemetry --off
```

원격 분석을 켭니다.

```
sfctl settings telemetry set_telemetry --on
```


## <a name="next-steps"></a>다음 단계
- Service Fabric CLI [설정](service-fabric-cli.md)
- [샘플 스크립트](/azure/service-fabric/scripts/sfctl-upgrade-application)를 사용하여 Microsoft Azure Service Fabric CLI를 사용하는 방법에 대해 알아봅니다.