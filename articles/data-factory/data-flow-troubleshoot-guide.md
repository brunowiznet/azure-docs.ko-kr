---
title: 데이터 흐름 문제 해결
description: Azure Data Factory에서 데이터 흐름 문제를 해결 하는 방법에 대해 알아봅니다.
services: data-factory
ms.author: makromer
author: kromerm
manager: anandsub
ms.service: data-factory
ms.topic: troubleshooting
ms.custom: seo-lt-2019
ms.date: 12/19/2019
ms.openlocfilehash: 06746cfc3b39a242c16a6b4f4c95b3c212a9abd5
ms.sourcegitcommit: f4f626d6e92174086c530ed9bf3ccbe058639081
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75443943"
---
# <a name="troubleshoot-azure-data-factory-data-flows"></a>데이터 흐름 Azure Data Factory 문제 해결

이 문서에서는 Azure Data Factory의 데이터 흐름에 대 한 일반적인 문제 해결 방법을 살펴봅니다.

## <a name="common-errors-and-messages"></a>일반적인 오류 및 메시지

### <a name="error-message-df-sys-01-shadeddatabricksorgapachehadoopfsazureazureexception-commicrosoftazurestoragestorageexception-the-specified-container-does-not-exist"></a>오류 메시지: DF-SYS-01: databricks:. n a m e. n a m e. StorageException: 지정 된 컨테이너가 없습니다.

- **증상**: 컨테이너가 없으므로 데이터 미리 보기, 디버그 및 파이프라인 데이터 흐름 실행이 실패 합니다.

- **원인**: 데이터 집합에 저장소에 없는 컨테이너가 포함 된 경우

- **해결**방법: 데이터 집합에서 참조 하는 컨테이너가 있는지 확인 합니다.

### <a name="error-message-df-sys-01-javalangassertionerror-assertion-failed-conflicting-directory-structures-detected-suspicious-paths"></a>오류 메시지: DF-SYS-01: AssertionError: assertion failed: 충돌 하는 디렉터리 구조가 검색 되었습니다. 의심 스러운 경로

- **증상**: Parquet 파일을 사용 하 여 소스 변환에서 와일드 카드를 사용 하는 경우

- **원인**: 와일드 카드 구문이 잘못 되었거나 잘못 되었습니다.

- **해결**방법: 원본 변환 옵션에서 사용 중인 와일드 카드 구문을 확인 합니다.

### <a name="error-message-df-src-002-container-container-name-is-required"></a>오류 메시지: DF-002: ' container ' (Container name)가 필요 합니다.

- **증상**: 컨테이너가 없으므로 데이터 미리 보기, 디버그 및 파이프라인 데이터 흐름 실행이 실패 합니다.

- **원인**: 데이터 집합에 저장소에 없는 컨테이너가 포함 된 경우

- **해결**방법: 데이터 집합에서 참조 하는 컨테이너가 있는지 확인 합니다.

### <a name="error-message-df-uni-001-primarykeyvalue-has-incompatible-types-integertype-and-stringtype"></a>오류 메시지: DF-001: PrimaryKeyValue에 호환 되지 않는 형식 IntegerType 및 StringType이 있습니다.

- **증상**: 컨테이너가 없으므로 데이터 미리 보기, 디버그 및 파이프라인 데이터 흐름 실행이 실패 합니다.

- **원인**: 데이터베이스 싱크에 잘못 된 기본 키 유형을 삽입 하려고 할 때 발생 합니다.

- **해결**방법: 파생 열을 사용 하 여 데이터 흐름의 기본 키에 사용 하는 열을 대상 데이터베이스의 데이터 형식과 일치 시킵니다.

### <a name="error-message-df-sys-01-commicrosoftsqlserverjdbcsqlserverexception-the-tcpip-connection-to-the-host-xxxxxdatabasewindowsnet-port-1433-has-failed-error-xxxxdatabasewindowsnet-verify-the-connection-properties-make-sure-that-an-instance-of-sql-server-is-running-on-the-host-and-accepting-tcpip-connections-at-the-port-make-sure-that-tcp-connections-to-the-port-are-not-blocked-by-a-firewall"></a>오류 메시지: DF-SYS-01: SQLServerException: 호스트 xxxxx.database.windows.net 포트 1433에 대 한 TCP/IP 연결이 실패 했습니다. 오류: "xxxx.database.windows.net. 연결 속성을 확인 합니다. SQL Server 인스턴스가 호스트에서 실행 되 고 포트에서 TCP/IP 연결을 허용 하는지 확인 합니다. 포트에 대 한 TCP 연결이 방화벽에 의해 차단 되지 않는지 확인 하십시오. "

- **증상**: 데이터베이스 원본 또는 싱크를 사용 하 여 데이터를 미리 보거나 파이프라인을 실행할 수 없습니다.

- **원인**: 데이터베이스가 방화벽으로 보호 됩니다.

- **해결**방법: 데이터베이스에 대 한 방화벽 액세스를 엽니다.

### <a name="error-message-df-sys-01-commicrosoftsqlserverjdbcsqlserverexception-there-is-already-an-object-named-xxxxxx-in-the-database"></a>오류 메시지: DF-SYS-01: SQLServerException: 데이터베이스에 이름이 ' xxxxxx ' 인 개체가 이미 있습니다.

- **증상**: 싱크가 테이블을 만들지 못함

- **원인**: 대상 데이터베이스에 원본 또는 데이터 집합에 정의 된 동일한 이름의 기존 테이블 이름이 이미 있습니다.

- **해결**방법: 만들려는 테이블의 이름을 변경 합니다.

### <a name="error-message-df-sys-01-commicrosoftsqlserverjdbcsqlserverexception-string-or-binary-data-would-be-truncated"></a>오류 메시지: DF-SYS-01: SQLServerException: 문자열 또는 이진 데이터가 잘립니다. 

- **증상**: SQL 싱크에 데이터를 작성할 때 잘림 오류가 발생할 수 있는 파이프라인 실행에서 데이터 흐름이 실패 합니다.

- **원인**: 데이터 흐름의 필드가 sql database의 열에 매핑되는 값을 저장 하기에 충분 하지 않아 sql 드라이버에서이 오류를 throw 합니다.

- **해결**방법: 파생 열에 ```left()```를 사용 하 여 문자열 열의 데이터 길이를 줄이거나 ["error row" 패턴](how-to-data-flow-error-rows.md) 을 구현할 수 있습니다.

### <a name="error-message-since-spark-23-the-queries-from-raw-jsoncsv-files-are-disallowed-when-the-referenced-columns-only-include-the-internal-corrupt-record-column"></a>오류 메시지: Spark 2.3부터 참조 되는 열에만 내부 손상 된 레코드 열이 포함 된 경우 원시 JSON/CSV 파일의 쿼리를 사용할 수 없습니다. 

- **증상**: JSON 원본에서 읽기 실패

- **원인**: 여러 중첩 된 줄에서 단일 문서를 사용 하 여 JSON 소스에서 읽을 때, ADF를 통해 ADF는 새 문서가 시작 되는 위치를 확인할 수 없으며 이전 문서가 종료 됩니다.

- **해결**방법: json 데이터 집합을 사용 하는 원본 변환에서 "json 설정"을 확장 하 고 "단일 문서"를 설정 합니다.

### <a name="error-message-duplicate-columns-found-in-join"></a>오류 메시지: 조인에 중복 된 열이 있습니다.

- **증상**: 조인 변환이 왼쪽 및 오른쪽 모두의 열에서 중복 된 열 이름을 포함 하 고 있습니다.

- **원인**: 조인 중인 스트림에 일반적인 열 이름이 있습니다.

- **해결**방법: 조인 뒤에 선택 변환을 추가 하 고 입력 및 출력 모두에 대해 "중복 열 제거"를 선택 합니다.

### <a name="error-message-possible-cartesian-product"></a>오류 메시지: 가능한 카티션 곱

- **증상**: 조인 또는 조회 변환에서 데이터 흐름 실행 시 가능한 카티션 곱을 검색 했습니다.

- **원인**: 크로스 조인을 사용 하도록 ADF에 명시적으로 지시 하지 않은 경우 데이터 흐름이 실패할 수 있습니다.

- **해결**방법: 사용자 지정 cross join을 사용 하 여 조회 또는 조인 변환을 조인으로 변경 하 고 식 편집기에서 조회 또는 조인 조건을 입력 합니다. 전체 카티션 곱을 명시적으로 생성 하려면 조인 앞에 있는 두 개의 독립 스트림에서 파생 열 변환을 사용 하 여 일치 시킬 가상 키를 만들어야 합니다. 예를 들어 ```SyntheticKey``` 이라는 각 스트림의 파생 열에 새 열을 만들고 ```1```같도록 설정 합니다. 그런 다음 사용자 지정 조인 식으로 ```a.SyntheticKey == b.SyntheticKey```를 사용 합니다.

> [!NOTE]
> 사용자 지정 크로스 조인에서 왼쪽 및 오른쪽 관계의 양쪽에 있는 하나 이상의 열을 포함 해야 합니다. 각 쪽의 열 대신 정적 값을 사용 하 여 크로스 조인을 실행 하면 전체 데이터 집합을 전체 검색 하 여 데이터 흐름이 제대로 수행 되지 않게 됩니다.

## <a name="general-troubleshooting-guidance"></a>일반 문제 해결 지침

1. 데이터 집합 연결의 상태를 확인 합니다. 각 원본 및 싱크 변환에서 사용 중인 각 데이터 집합에 대 한 연결 된 서비스를 방문 하 고 연결을 테스트 합니다.
2. 데이터 흐름 디자이너에서 파일 및 테이블 연결의 상태를 확인 합니다. 디버그를 전환 하 고 원본 변환에서 데이터 미리 보기를 클릭 하 여 데이터에 액세스할 수 있는지 확인 합니다.
3. 모든 항목이 데이터 미리 보기에서 양호 하면 파이프라인 디자이너로 이동 하 여 파이프라인 활동에 데이터 흐름을 배치 합니다. 종단 간 테스트를 위한 파이프라인을 디버깅 합니다.

## <a name="next-steps"></a>다음 단계

문제 해결에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

*  [Data Factory 블로그](https://azure.microsoft.com/blog/tag/azure-data-factory/)
*  [Data Factory 기능 요청](https://feedback.azure.com/forums/270578-data-factory)
*  [Azure 비디오](https://azure.microsoft.com/resources/videos/index/?sort=newest&services=data-factory)
*  [MSDN 포럼](https://social.msdn.microsoft.com/Forums/home?sort=relevancedesc&brandIgnore=True&searchTerm=data+factory)
*  [Data Factory에 대 한 Stack Overflow 포럼](https://stackoverflow.com/questions/tagged/azure-data-factory)
*  [Data Factory에 대 한 Twitter 정보](https://twitter.com/hashtag/DataFactory)
*  [ADF 매핑 데이터 흐름 성능 가이드](concepts-data-flow-performance.md)
